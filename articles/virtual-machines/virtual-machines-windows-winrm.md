---
title: Azure Resource Manager에서 가상 컴퓨터에 대한 WinRM 액세스 설정 | Microsoft Docs
description: Azure Resource Manager에서 사용할 WinRM 액세스를 설정하는 방법
services: virtual-machines-windows
documentationcenter: ''
author: singhkays
manager: timlt
editor: ''
tags: azure-resource-manager

ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/16/2016
ms.author: singhkay

---
# Azure Resource Manager에서 가상 컴퓨터에 대한 WinRM 액세스 설정
## Azure 서비스 관리 및 Azure Resource Manager의 WinRM
[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

클래식 배포 모델

* Azure Resource Manager의 개요를 보려면 이 [문서](../resource-group-overview.md)를 참조하세요.
* Azure 서비스 관리 및 Azure Resource Manager 간의 차이점에 대해서는 이 [문서](../resource-manager-deployment-model.md)를 참조하세요.

두 스택 간에 WinRM 구성을 설정할 때의 주요 차이점은 VM에 인증서가 설치되는 방법에 있습니다. Azure Resource Manager 스택에서 인증서는 주요 자격 증명 모음 리소스 공급자가 관리하는 리소스로 모델링됩니다. 따라서 사용자는 VM에서 인증서를 사용하기 위해 먼저 본인의 인증서를 제공한 후 주요 자격 증명 모음에 업로드해야 합니다.

다음은 WinRM 연결을 사용하여 VM을 설정하는 데 필요한 단계입니다.

1. 주요 자격 증명 모음 만들기
2. 자체 서명된 인증서 만들기
3. 자체 서명된 인증서를 주요 자격 증명 모음에 업로드
4. 주요 자격 증명 모음에 자체 서명된 인증서에 대한 URL 가져오기
5. VM을 만드는 동안 자체 서명된 인증서 URL 참조

## 1단계: 주요 자격 증명 모음 만들기
아래 명령을 사용하여 주요 자격 증명 모음을 만들 수 있습니다.

```
New-AzureRmKeyVault -VaultName "<vault-name>" -ResourceGroupName "<rg-name>" -Location "<vault-location>" -EnabledForDeployment -EnabledForTemplateDeployment
```

## 2단계: 자체 서명된 인증서 만들기
이 PowerShell 스크립트를 사용하여 자체 서명된 인증서를 만들 수 있습니다.

```
$certificateName = "somename"

$thumbprint = (New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My -KeySpec KeyExchange).Thumbprint

$cert = (Get-ChildItem -Path cert:\CurrentUser\My\$thumbprint)

$password = Read-Host -Prompt "Please enter the certificate password." -AsSecureString

Export-PfxCertificate -Cert $cert -FilePath ".\$certificateName.pfx" -Password $password
```

## 3단계: 주요 자격 증명 모음에 자체 서명된 인증서 업로드
1단계에서 만든 주요 자격 증명 모음에 인증서를 업로드하기 전에 먼저 Microsoft.Compute 리소스 공급자가 이해할 수 있는 형식으로 변환해야 합니다. 아래 PowerShell 스크립트를 사용하면 그러한 형식으로 변환할 수 있습니다.

```
$fileName = "<Path to the .pfx file>"
$fileContentBytes = Get-Content $fileName -Encoding Byte
$fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

$jsonObject = @"
{
  "data": "$filecontentencoded",
  "dataType" :"pfx",
  "password": "<password>"
}
"@

$jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
$jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

$secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText –Force
Set-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>" -SecretValue $secret
```

## 4단계: 주요 자격 증명 모음에 자체 서명된 인증서에 대한 URL 가져오기
Microsoft.Compute 리소스 공급자는 VM을 프로비전하는 동안 주요 자격 증명 모음 내에 포함된 암호에 대한 URL이 필요합니다. 이룰 통해 Microsoft.Compute 리소스 공급자는 암호를 다운로드하고 VM에서 해당 인증서를 만들 수 있습니다.

> [!NOTE]
> 암호의 URL에는 버전도 포함되어야 합니다. URL 예제는 https://contosovault.vault.azure.net:443/secrets/contososecret/01h9db0df2cd4300a20ence585a6s7ve와 같습니다.
> 
> 

#### 템플릿
아래 코드를 사용하여 템플릿의 URL에 대한 링크를 가져올 수 있습니다.

    "certificateUrl": "[reference(resourceId(resourceGroup().name, 'Microsoft.KeyVault/vaults/secrets', '<vault-name>', '<secret-name>'), '2015-06-01').secretUriWithVersion]"

#### PowerShell
아래의 PowerShell 명령을 사용하여 이 URL을 가져올 수 있습니다.

    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id

## 5단계: VM을 만드는 동안 자체 서명된 인증서 URL 참조
#### Azure 리소스 관리자 템플릿
템플릿을 통해 VM을 만드는 동안 인증서가 아래와 같이 암호 섹션 및 winRM 섹션에서 참조됩니다.

    "osProfile": {
          ...
          "secrets": [
            {
              "sourceVault": {
                "id": "<resource id of the Key Vault containing the secret>"
              },
              "vaultCertificates": [
                {
                  "certificateUrl": "<URL for the certificate you got in Step 4>",
                  "certificateStore": "<Name of the certificate store on the VM>"
                }
              ]
            }
          ],
          "windowsConfiguration": {
            ...
            "winRM": {
              "listeners": [
                {
                  "protocol": "http"
                },
                {
                  "protocol": "https",
                  "certificateUrl": "<URL for the certificate you got in Step 4>"
                }
              ]
            },
            ...
          }
        },

위 항목에 대한 샘플 템플릿은 [201-vm-winrm-keyvault-windows](https://azure.microsoft.com/documentation/templates/201-vm-winrm-keyvault-windows)에 나와 있습니다.

이 템플릿의 소스 코드는 [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-winrm-keyvault-windows)에 나와 있습니다.

#### PowerShell
    $vm = New-AzureRmVMConfig -VMName "<VM name>" -VMSize "<VM Size>"
    $credential = Get-Credential
    $secretURL = (Get-AzureKeyVaultSecret -VaultName "<vault name>" -Name "<secret name>").Id
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName "<Computer Name>" -Credential $credential -WinRMHttp -WinRMHttps -WinRMCertificateUrl $secretURL
    $sourceVaultId = (Get-AzureRmKeyVault -ResourceGroupName "<Resource Group name>" -VaultName "<Vault Name>").ResourceId
    $CertificateStore = "My"
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore $CertificateStore -CertificateUrl $secretURL

## 6단계: VM에 연결
VM에 연결하려면 먼저 컴퓨터가 WinRM 원격 관리에 맞게 구성되어 있는지 확인해야 합니다. 관리자 권한으로 PowerShell을 시작하고 아래 명령을 실행하여 제대로 설정되었는지 확인합니다.

    Enable-PSRemoting -Force

> [!NOTE]
> 위 작업이 제대로 수행되지 않으면 WinRM 서비스가 실행되고 있는지 확인해야 합니다. 이 작업은 `Get-Service WinRM`을 사용하여 수행할 수 있습니다.
> 
> 

설정이 끝나면 아래 명령을 사용하여 VM에 연결할 수 있습니다.

    Enter-PSSession -ConnectionUri https://<public-ip-dns-of-the-vm>:5986 -Credential $cred -SessionOption (New-PSSessionOption -SkipCACheck -SkipCNCheck -SkipRevocationCheck) -Authentication Negotiate

<!---HONumber=AcomDC_0824_2016-->