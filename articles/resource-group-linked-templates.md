---
title: Resource Manager와 연결된 템플릿 | Microsoft Docs
description: Azure Resource Manager 템플릿에서 연결된 템플릿을 사용하여 모듈식 템플릿 솔루션을 만드는 방법을 설명합니다. 매개 변수 값을 전달하고 매개 변수 파일 및 동적으로 생성된 URL을 지정하는 방법을 보여 줍니다.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn

ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/02/2016
ms.author: tomfitz

---
# Azure Resource Manager에서 연결된 템플릿 사용
하나의 Azure Resource Manager 템플릿 내에서 다른 템플릿에 연결하여 배포를 특정 용도의 템플릿 집합으로 분해할 수 있습니다. 응용 프로그램을 여러 코드 클래스로 분해하는 경우처럼 이러한 분해는 테스트, 다시 사용 및 가독성 측면에서 이점을 제공합니다.

주 템플릿의 매개 변수를 연결된 템플릿에 전달할 수 있으며 이러한 매개 변수는 호출하는 템플릿이 노출하는 매개 변수 또는 변수에 직접 매핑될 수 있습니다. 또한 연결된 템플릿은 원본 템플릿에 출력 변수를 다시 전달할 수 있으므로 템플릿 간에 양방향 데이터 교환이 가능해집니다.

## 템플릿에 연결
연결된 템플릿을 가리키는 주 템플릿 내에 배포 리소스를 추가하여 두 템플릿 간에 링크를 만듭니다. **templateLink** 속성을 연결된 템플릿의 URI로 설정합니다. 템플릿에 직접 값을 지정하거나 매개 변수 파일에 연결하여 매개 변수 값을 연결된 템플릿에 제공할 수 있습니다. 다음 예제에서는 **parameters** 속성을 사용하여 매개 변수 값을 직접 지정합니다.

    "resources": [ 
      { 
         "apiVersion": "2015-01-01", 
         "name": "linkedTemplate", 
         "type": "Microsoft.Resources/deployments", 
         "properties": { 
           "mode": "incremental", 
           "templateLink": {
              "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
              "contentVersion": "1.0.0.0"
           }, 
           "parameters": { 
              "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
           } 
         } 
      } 
    ] 

Resource Manager 서비스는 연결된 템플릿에 액세스할 수 있어야 합니다. 로컬 파일 또는 연결된 템플릿에 대해 로컬 네트워크에만 사용할 수 있는 파일을 지정할 수 없습니다. **http** 또는 **https** 중 하나를 포함하는 URI 값만 제공할 수 있습니다. 한 가지 옵션은 연결된 템플릿을 저장소 계정에 배치하고 다음 예제와 같이 해당 항목의 URI를 사용하는 것입니다.

    "templateLink": {
        "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
        "contentVersion": "1.0.0.0",
    }

연결된 템플릿은 외부에서 사용할 수 있어야 하지만 일반에 공개할 필요는 없습니다. 저장소 계정 소유자만 액세스할 수 있는 개인 저장소 계정에 템플릿을 추가할 수 있습니다. 그런 다음 배포하는 동안 액세스할 수 있도록 공유 액세스 서명(SAS) 토큰을 만듭니다. 링크된 템플릿 URI에 SAS 토큰을 추가합니다. 저장소 계정에서 템플릿을 설정하고 SAS 토큰을 생성하는 절차는 [Resource Manager 템플릿과 Azure PowerShell로 리소스 배포](resource-group-template-deploy.md) 또는 [Resource Manager 템플릿과 Azure CLI로 리소스 배포](resource-group-template-deploy-cli.md)를 참조하세요.

다음 예제는 다른 템플릿에 연결되는 상위 템플릿을 보여줍니다. 연결된 템플릿은 매개 변수로 전달된 SAS 토큰으로 액세스합니다.

    "parameters": {
        "sasToken": { "type": "securestring" }
    },
    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "linkedTemplate",
            "type": "Microsoft.Resources/deployments",
            "properties": {
              "mode": "incremental",
              "templateLink": {
                "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
                "contentVersion": "1.0.0.0"
              }
            }
        }
    ],

토큰이 보안 문자열로 전달되었지만 SAS 토큰을 포함한 링크된 템플릿 URI가 해당 리소스 그룹의 배포 작업에 로그됩니다. 노출을 최소화하려면 토큰에 만료 날짜를 설정합니다.

## 매개 변수 파일에 연결
다음 예제는 **parametersLink** 속성을 사용하여 매개 변수 파일에 연결합니다.

    "resources": [ 
      { 
         "apiVersion": "2015-01-01", 
         "name": "linkedTemplate", 
         "type": "Microsoft.Resources/deployments", 
         "properties": { 
           "mode": "incremental", 
           "templateLink": {
              "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
              "contentVersion":"1.0.0.0"
           }, 
           "parametersLink": { 
              "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
              "contentVersion":"1.0.0.0"
           } 
         } 
      } 
    ] 

연결된 매개 변수 파일의 URI 값은 로컬 파일일 수 없으며 **http** 또는 **https** 중 하나를 포함해야 합니다. 매개 변수 파일은 SAS 토큰으로 액세스를 제한할 수 있습니다.

## 변수를 사용하여 템플릿 연결
앞의 예제에서는 템플릿 링크에 대한 하드 코딩된 URL 값을 보여 주었습니다. 이 방법은 간단한 템플릿에는 적용될 수 있지만 대규모 모듈식 템플릿 집합으로 작업하는 경우에는 가능하지 않습니다. 대신, 주 템플릿에 대한 기본 URL을 보관하는 정적 변수를 만든 다음 해당 기본 URL에서 연결된 템플릿에 대한 URL을 동적으로 만들 수 있습니다. 이 방식의 경우 주 템플릿에서만 정적 변수를 변경하면 되므로 템플릿을 쉽게 이동하거나 분기할 수 있다는 장점이 있습니다. 주 템플릿은 분해된 템플릿 전체에서 올바른 URI를 전달합니다.

다음 예제에서는 기본 URL을 사용하여 연결된 템플릿에 대한 두 개의 URL을 만드는 방법을 보여 줍니다(**sharedTemplateUrl** 및 **vmTemplate**).

    "variables": {
        "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
        "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
        "tshirtSizeSmall": {
            "vmSize": "Standard_A1",
            "diskSize": 1023,
            "vmTemplate": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]",
            "vmCount": 2,
            "slaveCount": 1,
            "storage": {
                "name": "[parameters('storageAccountNamePrefix')]",
                "count": 1,
                "pool": "db",
                "map": [0,0],
                "jumpbox": 0
            }
        }
    }

또한 [deployment()](resource-group-template-functions.md#deployment)를 사용하여 현재 템플릿에 대한 기본 URL을 가져올 수 있으며 동일한 위치에 있는 다른 템플릿에 대한 URL를 가져올 수 있습니다. 이 방법은 템플릿 위치가 변경되거나(아마도 버전 관리로 인해) 템플릿 파일에서 URL 하드 코딩을 방지하려는 경우 유용합니다.

    "variables": {
        "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
    }

## 조건부로 템플릿에 연결
연결된 템플릿의 URI를 생성하는 데 사용되는 매개 변수 값을 전달하여 다른 템플릿에 연결할 수 있습니다. 이 방법은 배포하는 동안 사용할 연결된 템플릿을 지정해야 하는 경우에 효과적으로 작동합니다. 예를 들어 기존 저장소 계정에 사용할 하나의 템플릿을 지정하고 새 저장소 계정에 사용할 다른 템플릿을 지정할 수 있습니다.

다음 예제는 저장소 계정 이름에 대한 매개 변수 및 저장소 계정이 신규 또는 기존인지 여부를 지정할 매개 변수를 보여 줍니다.

    "parameters": {
        "storageAccountName": {
            "type": "String"
        },
        "newOrExisting": {
            "type": "String",
            "allowedValues": [
                "new",
                "existing"
            ]
        }
    },

신규 또는 기존 매개 변수 값을 포함하는 템플릿 URI에 대한 변수를 만듭니다.

    "variables": {
        "templatelink": "[concat('https://raw.githubusercontent.com/exampleuser/templates/master/',parameters('newOrExisting'),'StorageAccount.json')]"
    },

배포 리소스에 대한 변수 값을 제공합니다.

    "resources": [
        {
            "apiVersion": "2015-01-01",
            "name": "linkedTemplate",
            "type": "Microsoft.Resources/deployments",
            "properties": {
                "mode": "incremental",
                "templateLink": {
                    "uri": "[variables('templatelink')]",
                    "contentVersion": "1.0.0.0"
                },
                "parameters": {
                    "StorageAccountName": {
                        "value": "[parameters('storageAccountName')]"
                    }
                }
            }
        }
    ],

URI는 **existingStorageAccount.json** 또는 **newStorageAccount.json**이라는 템플릿으로 확인됩니다. 이러한 URI에 대한 템플릿을 만듭니다.

다음 예제는 **existingStorageAccount.json** 템플릿을 보여 줍니다.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "storageAccountName": {
          "type": "String"
        }
      },
      "variables": {},
      "resources": [],
      "outputs": {
        "storageAccountInfo": {
          "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')),providers('Microsoft.Storage', 'storageAccounts').apiVersions[0])]",
          "type" : "object"
        }
      }
    }

다음 예제는 **newStorageAccount.json** 템플릿을 보여 줍니다. 기존 저장소 계정 템플릿과 같이 저장소 계정 개체는 출력으로 돌아갑니다. 마스터 템플릿은 연결된 템플릿을 사용하여 작동합니다.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "storageAccountName": {
          "type": "string"
        }
      },
      "resources": [
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[parameters('StorageAccountName')]",
          "apiVersion": "2016-01-01",
          "location": "[resourceGroup().location]",
          "sku": {
            "name": "Standard_LRS"
          },
          "kind": "Storage",
          "properties": {
          }
        }
      ],
      "outputs": {
        "storageAccountInfo": {
          "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('StorageAccountName')),providers('Microsoft.Storage', 'storageAccounts').apiVersions[0])]",
          "type" : "object"
        }
      }
    }

## 전체 예제
다음 예제 템플릿은 이 문서의 여러 가지 개념을 설명하기 위해 링크된 템플릿의 단순화된 배열을 보여줍니다. 이 예제는 템플릿이 공용 액세스가 꺼진 저장소 계정에 있는 동일한 컨테이너에 추가되었다고 가정합니다. 링크된 템플릿은 **출력** 섹션의 기본 템플릿에 값을 다시 전달합니다.

**parent.json** 파일은 다음과 같이 구성됩니다.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "containerSasToken": { "type": "string" }
      },
      "resources": [
        {
          "apiVersion": "2015-01-01",
          "name": "linkedTemplate",
          "type": "Microsoft.Resources/deployments",
          "properties": {
            "mode": "incremental",
            "templateLink": {
              "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
              "contentVersion": "1.0.0.0"
            }
          }
        }
      ],
      "outputs": {
        "result": {
          "type": "object",
          "value": "[reference('linkedTemplate').outputs.result]"
        }
      }
    }

**helloworld.json** 파일은 다음과 같이 구성됩니다.

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "variables": {},
      "resources": [],
      "outputs": {
        "result": {
            "value": "Hello World",
            "type" : "string"
        }
      }
    }

PowerShell에서는 컨테이너용 토큰을 얻고 다음을 사용하여 템플릿을 배포합니다.

    Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
    $token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
    New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ("https://storagecontosotemplates.blob.core.windows.net/templates/parent.json" + $token) -containerSasToken $token

Azure CLI에서는 컨테이너용 토큰을 얻고 다음 코드를 사용하여 템플릿을 배포합니다. 현재는 SAS 토큰을 포함한 템플릿 URI를 사용할 때 배포에 이름을 지정해야 합니다.

    expiretime=$(date -I'minutes' --date "+30 minutes")  
    azure storage container sas create --container templates --permissions r --expiry $expiretime --json | jq ".sas" -r
    azure group deployment create -g ExampleGroup --template-uri "https://storagecontosotemplates.blob.core.windows.net/templates/parent.json?{token}" -n tokendeploy  

SAS 토큰을 매개 변수로 제공하라는 메시지가 나타납니다. **?**로 토큰을 삽입해야 합니다.

## 다음 단계
* 리소스 배포 순서를 정의하는 방법을 알아보려면 [Azure Resource Manager 템플릿에서 종속성 정의](resource-group-define-dependencies.md)를 참조하세요.
* 하나의 리소스를 정의하되 해당 리소스의 여러 인스턴스를 만드는 방법을 알아보려면 [Azure Resource Manager에서 리소스의 여러 인스턴스 만들기](resource-group-create-multiple.md)를 참조하세요.

<!---HONumber=AcomDC_0907_2016-->