---
title: Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결 | Microsoft Docs
description: 관리자가 기업 네트워크에 도메인이 가입되도록 장치를 활성화하는 그룹 정책을 구성할 수 있는 방법에 대해 설명합니다.
services: active-directory
documentationcenter: ''
author: femila
manager: swadhwa
editor: ''
tags: azure-classic-portal

ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: femila

---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a>Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결
도메인 가입은 조직에서 15년이 넘도록 작업하기 위해 장치를 연결해 온 일반적인 방식입니다. 사용자가 Windows Server Active Directory(Active Directory) 회사 또는 학교 계정을 사용하여 장치에 로그인할 수 있도록 설정했으며 IT에서 이러한 장치를 완전히 관리할 수 있도록 했습니다. 조직에서는 일반적으로 사용자에 게 장치를 프로비전하는 이미징 메서드에 의존하고 이를 관리하는 데 System Center 구성 관리자(SCCM) 또는 그룹 정책을 사용합니다.

Windows 10에서 도메인 가입을 사용하면 장치를 Azure AD(Azure Active Directory)에 연결한 후 다음과 같은 이점이 있습니다.

* 어디에서나 Azure AD 리소스에 SSO(single Sign-On)
* 회사 또는 학교 계정을 사용하여 엔터프라이즈 Windows 스토어에 액세스(Microsoft 계정 필요 없음)
* 회사 또는 학교 계정을 사용하여 장치 간 사용자 설정의 엔터프라이즈 규격 로밍(Microsoft 계정 필요 없음)
* Microsoft Passport 및 Windows Hello를 사용하는 회사 또는 학교 계정에 대한 강력한 인증 및 손쉬운 로그인
* 조직 장치의 그룹 정책 설정을 준수하는 장치 액세스 할 수 있도록 제한하는 기능

## <a name="prerequisites"></a>필수 조건
도메인 가입이 계속 유용합니다. 그러나 SSO에 대한 Azure AD 혜택을 얻고 회사 또는 학교 계정으로 설정을 로밍하고 회사 또는 학교 계정으로 Windows 스토어에 액세스하려면 다음이 필요합니다.

* Azure AD 구독
* Azure AD에 온-프레미스 디렉터리를 확장하는 Azure AD Connect
* Azure AD에 도메인 가입 장치를 연결하도록 설정한 정책
* 장치에 Windows 10 빌드(빌드 10551 또는 이후 버전)

또한 Microsoft Passport for Work 및 Windows Hello를 사용하도록 하려면 다음과 같은 사항도 필요합니다.

* 사용자 인증서를 발급하기 위한 PKI(공개 키 인프라)입니다.
* Technical Preview용 System Center Configuration Manager 버전 1509. 자세한 내용은 [Microsoft System Center Configuration Manager Technical Preview](https://technet.microsoft.com/library/dn965439.aspx#BKMK_TP3Update) 및 [System Center Configuration Manager 팀 블로그](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)를 참조하세요. Microsoft Passport 키 기반의 사용자 인증서를 배포하려는 데 필요합니다.

PKI 배포 요구 사항에 대한 대안으로 다음을 수행할 수 있습니다.

* Windows Server 2016 Active Directory 도메인 서비스와 몇 가지 도메인 컨트롤러를 보유합니다.

조건부 액세스를 활성화하려면 추가 배포 없이 ‘도메인 가입된’ 장치에 대한 액세스를 허용하는 그룹 정책 설정을 만들 수 있습니다. 장치의 규정 준수에 따른 액세스 제어를 관리하려면 다음이 필요합니다.

* Passport 시나리오를 위한 Technical Preview용 System Center Configuration Manager 버전 1509

## <a name="deployment-instructions"></a>배포 지침
### <a name="step-1:-deploy-azure-active-directory-connect"></a>1단계: Azure Active Directory Connect 배포
Azure AD Connect를 사용하면 컴퓨터 온-프레미스를 클라우드에서 장치 개체로 프로비전할 수 있습니다. Azure AD Connect를 배포하려면 [Azure Active Directory와 온-프레미스 ID 통합](active-directory-aadconnect.md#install-azure-ad-connect)문서에서 "Azure AD Connect 설치"를 참조하세요.

* [Azure AD Connect를 위한 사용자 지정 설치](active-directory-aadconnect-get-started-custom.md)(Express 설치 아님)를 수행한 경우 이 단계 뒷부분에 있는 **온-프레미스 Active Directory에 서비스 연결점 만들기**절차를 따라야 합니다.
* Azure AD Connect를 설치하기 전에 Azure AD를 사용하여 페더레이션된 구성이 있는 경우(예: 이전에 AD FS(Active Directory Federation Services)를 배포한 경우) 이 단계 뒷부분에 있는 **AD FS 클레임 규칙 구성** 을 따라야 합니다.

#### <a name="create-a-service-connection-point-in-on-premises-active-directory"></a>온-프레미스 Active Directory에 서비스 연결점 만들기
도메인에 가입된 장치는 Azure 장치 등록 서비스를 사용하여 자동 등록할 경우 Azure AD 테넌트 정보를 검색하는 데 이 서비스 연결점을 사용합니다.

Azure AD Connect 서버에서 다음 PowerShell 명령을 실행합니다.

    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;


cmdlet $aadAdminCred = Get-Credential을 실행하는 경우 Get-Credential 팝업이 표시될 때 입력되는 자격 증명의 사용자 이름에 대한 형식 *user@example.com* 을 사용합니다.

cmdlet Initialize-ADSyncDomainJoinedComputerSync...를 실행하는 경우 [*커넥터 계정 이름*]을 Active Directory Connector 계정으로 사용하는 도메인 계정으로 바꿉니다.

#### <a name="configure-ad-fs-claim-rules"></a>AD FS 클레임 규칙 구성
AD FS 클레임 규칙을 구성하면 Azure 장치 등록 서비스를 사용하여 컴퓨터를 즉시 등록할 수 있습니다. 이를 위해서 컴퓨터가 AD FS를 통해 Kerberos/NTLM을 사용하여 인증하도록 허용합니다. 이 단계 없이 컴퓨터는 지연된 방식으로 Azure AD를 가져옵니다(Azure AD Connect 동기화의 시간에 종속됨).

> [!NOTE]
> 페더레이션 서버 온-프레미스인 AD FS가 없는 경우 클레임 규칙을 만드는 공급업체의 지침을 따릅니다.
> 
> 

AD FS 서버(또는 AD FS 서버에 연결된 세션)에서 다음 PowerShell 명령을 실행합니다.

      <#----------------------------------------------------------------------
     |   Modify the Azure AD Relying Party to include the claims needed
     |   for DomainJoin++. The rules include:
     |   -ObjectGuid
     |   -AccountType
     |   -ObjectSid
     +---------------------------------------------------------------------#>

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules

    $rule1 = '@RuleName = "Issue object GUID"
          c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "515$", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"] &&
          c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"]
          => issue(store = "Active Directory", types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), query = ";objectguid;{0}", param = c2.Value);'

    $rule2 = '@RuleName = "Issue account type for domain joined computers"
          c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "515$", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"]
          => issue(Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", Value = "DJ");'

    $rule3 = '@RuleName = "Pass through primary SID"
          c1:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value =~ "515$", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"] &&
          c2:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"]
          => issue(claim = c2);'

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString

> [!NOTE]
> Windows 10 컴퓨터는 AD FS에서 호스트된 활성 WS-Trust 끝점에 Windows 통합 인증을 사용하여 인증합니다. 이 끝점을 사용할 수 있어야 합니다. 또한 웹 인증 프록시를 사용하는 경우 이 끝점이 프록시를 통해 게시되어야 합니다. adfs/services/trust/13/windowstransport를 선택하여 이 작업을 수행할 수 있습니다. AD FS 관리 콘솔의 **서비스** > **끝점**에 사용하도록 설정된 것으로 표시되어야 합니다.
> 
> 

### <a name="step-2:-configure-automatic-device-registration-via-group-policy-in-active-directory"></a>2단계: Active Directory에서 그룹 정책을 통해 자동 장치 등록 구성
Active Directory의 그룹 정책을 사용하여 Windows 10 도메인 가입 장치를 Azure AD에 자동으로 등록하도록 구성할 수 있습니다.

> [!NOTE]
> 장치 자동 등록을 설정하는 방법에 대한 최신 지침은 [Azure Active Directory를 사용하여 Windows 도메인 가입 장치의 자동 등록을 설정하는 방법](active-directory-conditional-access-automatic-device-registration-setup.md)을 참조하세요.
> 
> 이 그룹 정책 템플릿은 Windows 10에서 이름이 변경되었습니다. Windows 10 컴퓨터로부터 그룹 정책 도구를 실행하는 경우 정책은 다음과 같이 표시됩니다. <br>
> **도메인에 가입된 컴퓨터를 장치로 등록**<br>
> 이 정책은 다음 위치에 있습니다.<br>
> ***컴퓨터 구성/정책/관리 템플릿/Windows 구성 요소/장치 등록***
> 
> 

## <a name="additional-information"></a>추가 정보
* [엔터프라이즈를 위한 Windows 10: 작업에 장치를 사용하는 방법](active-directory-azureadjoin-windows10-devices-overview.md)
* [Azure Active Directory 조인을 통해 클라우드 기능을 Windows 10 장치로 확장](active-directory-azureadjoin-user-upgrade.md)
* [Azure AD 조인에 대한 사용 시나리오에 대해 알아보기](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Windows 10 환경용 Azure AD에 도메인 가입된 장치 연결](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD 조인 설정](active-directory-azureadjoin-setup.md)

<!--HONumber=Oct16_HO2-->


