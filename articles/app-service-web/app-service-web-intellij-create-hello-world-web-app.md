---
title: IntelliJ에서 Azure용 Hello World 웹앱 만들기 | Microsoft Docs
description: 이 자습서에서는 IntelliJ용 Azure 도구 키트를 사용하여 Azure용 Hello World 웹앱을 만드는 방법을 보여 줍니다.
services: app-service\web
documentationcenter: java
author: selvasingh
manager: wpickett
editor: ''

ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/11/2016
ms.author: asirveda;robmcm

---
# IntelliJ에서 Azure용 Hello World 웹앱 만들기
이 자습서에서는 [IntelliJ용 Azure 도구 키트]를 사용하여 기본 Hello World 응용 프로그램을 만들고 Azure에 웹앱으로 배포하는 방법을 보여 줍니다. 기본 JSP 예제는 편의를 위해 표시되지만 Azure 배포가 관련되는 한 아주 유사한 단계는 Java 서블릿에 적합합니다.

이 자습서를 완료한 경우 웹 브라우저에서 응용 프로그램을 보면 다음 그림과 같이 표시됩니다.

![][01]

## 필수 조건
* JDK(Java 개발자 키트), v 1.8 이상.
* IntelliJ IDEA Ultimate Edition. <https://www.jetbrains.com/idea/download/index.html>에서 다운로드할 수 있습니다.
* Java 기반 웹 서버 또는 응용 프로그램 서버의 배포(예: Apache Tomcat 또는 Jetty)
* Azure 구독(<https://azure.microsoft.com/free/> 또는 <http://azure.microsoft.com/pricing/purchase-options/>에서 구입할 수 있음)
* IntelliJ용 Azure 도구 키트. 자세한 내용은 [IntelliJ용 Azure 도구 키트 설치]를 참조하세요.

## Hello World 응용 프로그램을 만들려면
먼저 java 프로젝트를 만듭니다.

1. IntelliJ를 시작하고 메뉴에서 **File**을 클릭한 후 **New**를 클릭하고 **Project**를 클릭합니다.
   
   ![][02]
2. New Project 대화 상자에서 **Java**를 선택하고 **Web Application**을 선택한 후 **Next**를 클릭합니다.
   
   ![][03a]
   
   SDK가 할당되지 않은 상태로 계속 진행할지 묻는 메시지가 표시되면 **예**를 클릭합니다.
   
   ![][03b]
3. 이 자습서의 목적에 따라 프로젝트의 이름을 **Java-Web-App-On-Azure**로 지정하고 **Finish**를 클릭합니다.
   
   ![][04]
4. IntelliJ의 Project Explorer 보기 내에서 **Java-Web-App-On-Azure**를 확장한 다음 **web**을 확장하고 **index.jsp**를 두 번 클릭합니다.
   
   ![][05]
5. Eclipse에서 index.jsp 파일이 열리면 기존 `<body>` 요소 내에 **Hello World!**를 동적으로 표시하도록 텍스트를 추가합니다. 업데이트된 `<body>` 콘텐츠는 다음 예제와 유사하게 표시됩니다.
   
   `<body><b><% out.println("Hello World!"); %></b></body>`
6. index.jsp를 저장합니다.

## Azure 웹앱 컨테이너에 응용 프로그램을 배포하려면
몇 가지 방법으로 Azure에 Java 웹 응용 프로그램을 배포할 수 있습니다. 이 자습서에서는 가장 간단한 방법 중 하나를 설명합니다. 즉, 특별한 프로젝트 형식이나 추가 도구 없이 Azure 웹앱 컨테이너에 응용 프로그램을 배포하는 방법을 설명합니다. JDK 및 웹 컨테이너 소프트웨어는 Azure에서 제공되므로 별도로 업로드할 필요가 없습니다. Java 웹앱만 있으면 됩니다. 따라서 응용 프로그램 게시 프로세스에 걸리는 시간이 몇 분이 아니라 몇 초입니다.

1. IntelliJ의 Project Explorer에서 **Java-Web-App-On-Azure** 프로젝트를 마우스 오른쪽 단추로 클릭합니다. 상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.
   
   ![][06]
2. IntelliJ에서 Azure에 로그인하지 않은 경우 Azure 계정으로 로그인하라는 메시지가 표시됩니다.
   
   ![][07]
   
   참고: Azure 계정이 여러 개 있으면 로그인 프로세스 중에 일부 메시지가 동일한 것이더라도 두 번 이상 표시될 수 있습니다. 이 경우 로그인 지침에 따라 계속 진행합니다.
3. Azure 계정에 성공적으로 로그인하면 **구독 관리** 대화 상자에는 자격 증명과 연결된 구독 목록이 표시됩니다. 여러 구독이 나열된 경우 특정 하위 집합만 사용하려면 선택적으로 사용할 구독을 선택 취소할 수 있습니다. 구독을 선택했으면 **닫기**를 클릭합니다.
   
   ![][08]
4. **Azure 웹앱 컨테이너에 배포** 대화 상자가 나타나는 경우 이전에 만든 웹앱 컨테이너가 표시됩니다. 컨테이너를 만들지 않은 경우에는 목록이 비어 있습니다.
   
   ![][09]
5. 이전에 Azure 웹앱 컨테이너를 만들지 않은 경우 또는 응용 프로그램을 새 컨테이너에 게시하려는 경우 다음 단계를 사용합니다. 그렇지 않으면 기존 웹앱 컨테이너를 선택하고 아래의 6단계로 건너뜁니다.
   
   1. **+**를 클릭합니다.
      
        ![][10]
   2. 다음 몇 개 단계에서 사용되는 **새 웹앱 컨테이너** 대화 상자가 표시됩니다.
      
        ![][11]
   3. 웹앱 컨테이너에 **DNS 레이블**을 입력합니다. 이는 Azure에서 웹 응용 프로그램에 대한 호스트 URL의 리프 DNS 레이블을 형성합니다. 참고: 이름은 사용 가능해야 하며, Azure 웹앱 명명 요구 사항을 준수해야 합니다.
   4. **Web Container**(웹 컨테이너) 드롭다운 메뉴에서 응용 프로그램에 적절한 소프트웨어를 선택합니다.
      
        현재, Tomcat 8, Tomcat 7, Jetty 9 중에서 선택할 수 있습니다. 선택한 소프트웨어의 최근 배포는 Azure에서 제공되며, Oracle에서 만들고 Azure에서 제공되는 JDK 8의 최근 배포에서 실행됩니다.
   5. **Subscription**(구독) 드롭다운 메뉴에서 이 배포에 사용할 구독을 선택합니다.
   6. **Resource Group**(리소스 그룹) 드롭다운 메뉴에서 웹앱을 연결할 리소스 그룹을 선택합니다.
      
        참고: Azure 리소스 그룹을 사용하여 함께 삭제할 수 있도록 관련된 리소스를 그룹화할 수 있습니다.
      
        기존 리소스 그룹(있는 경우)을 선택하고 아래 g 단계로 건너뛰거나 이들 단계를 통해 새 리소스 그룹을 만들 수 있습니다.
      
      * **New...**(새로 만들기...)를 클릭합니다.
      * **New Resource Group**(새 리소스 그룹) 대화 상자가 표시됩니다.
        
            ![][12]
      * **Name**(이름) 텍스트 상자에서 새 리소스 그룹의 이름을 지정합니다.
      * **Region**(지역) 드롭다운 메뉴에서 리소스 그룹에 적절한 Azure 데이터 센터 위치를 선택합니다.
      * **확인**을 클릭합니다.
   7. **App Service Plan**(앱 서비스 계획) 드롭다운 메뉴에 선택한 리소스 그룹과 연결된 앱 서비스 계획이 나열됩니다.
      
        참고: 앱 서비스 계획은 웹 앱, 가격 책정 계층 및 계산 인스턴스 크기의 위치와 같은 정보를 지정합니다. 하나의 앱 서비스 계획은 여러 개의 웹 앱에 대해 사용될 수 있기 때문에 특정 웹 앱 배포와는 별도로 관리됩니다.
      
        기존 앱 서비스 계획(있는 경우)을 선택하고 아래 h 단계로 건너뛰거나 이들 단계를 통해 새 앱 서비스 계획을 만들 수 있습니다.
      
      * **New...**(새로 만들기...)를 클릭합니다.
      * **New App Service Plan**(새 앱 서비스 계획) 대화 상자가 표시됩니다.
        
            ![][13]
      * **Name**(이름) 텍스트 상자에서 새 앱 서비스 계획의 이름을 지정합니다.
      * **Location**(위치) 드롭다운 메뉴에서 계획에 적절한 Azure 데이터 센터 위치를 선택합니다.
      * **Pricing Tier**(가격 책정 계층) 드롭다운 메뉴에서 계획에 적절한 가격 책정을 선택합니다. 테스트 목적으로 **Free**를 선택할 수 있습니다.
      * **인스턴스 크기**(Instance Size) 드롭다운 메뉴에서 계획에 적절한 인스턴스 크기를 선택합니다. 테스트 목적으로 **Small**을 선택할 수 있습니다.
   8. 위 단계를 모두 완료한 경우 New Web App Container 대화 상자가 다음 그림과 유사하게 표시됩니다.
      
        ![][14]
   9. **확인**을 클릭하여 새 웹앱 컨테이너 만들기를 완료합니다.
      
        웹 앱 컨테이너의 목록이 새로 고쳐지도록 몇 초 간 기다리고 나면 새로 만든 웹 앱 컨테이너를 목록에서 선택할 수 있게 됩니다.
6. 이제 Azure에 대한 웹앱의 초기 배포를 완료할 준비가 되었습니다. **확인**을 클릭하여 Java 응용 프로그램을 선택한 웹앱 컨테이너에 배포합니다.
   
    ![][15]
   
    참고: 기본적으로 응용 프로그램은 응용 프로그램 서버의 하위 디렉터리로 배포됩니다. 루트 응용 프로그램으로 배포하려면 **확인**을 클릭하기 전에 **루트에 배포** 확인란을 선택합니다.
7. 이제 웹앱의 배포 상태를 나타내는 **Azure Activity Log** 보기를 확인합니다.
   
    ![][16]
   
    Azure에 웹앱을 배포하는 프로세스는 몇 초 내에 완료됩니다. 응용 프로그램이 준비되면 **Status** 열에 **Published**라는 링크가 표시됩니다. 이 링크를 클릭하여 배포된 웹앱의 홈페이지로 이동하거나, 다음 섹션의 단계를 사용하여 해당 웹앱으로 이동할 수 있습니다.

## Azure에서 웹앱 검색
Azure에서 웹앱을 검색하려면 **Azure 탐색기** 보기를 사용할 수 있습니다.

**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tools Windows**, **Service Explorer**를 차례로 클릭합니다. 이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.

**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 중지합니다.

1. **Azure** 노드를 확장합니다.
2. **웹앱** 노드를 확장합니다.
3. 원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.
4. 상황에 맞는 메뉴가 나타나면 **브라우저에서 열기**를 클릭합니다.
   
    ![][17]

## 웹앱 업데이트
실행 중인 기존 Azure 웹앱을 빠르고 쉽게 업데이트할 수 있으며, 두 가지 업데이트 옵션이 있습니다.

* 기존 Java 웹앱의 배포를 업데이트할 수 있습니다.
* 동일한 웹앱 컨테이너에 추가 Java 응용 프로그램을 게시할 수 있습니다.

두 경우 모두 프로세스는 동일하며 몇 초만 소요됩니다.

1. IntelliJ Project Explorer에서 업데이트하거나 기존 웹앱 컨테이너에 추가할 Java 응용 프로그램을 마우스 오른쪽 단추로 클릭합니다.
2. 상황에 맞는 메뉴가 나타나면 **Azure**를 선택한 다음 **Azure 웹앱으로 게시...**를 선택합니다.
3. 이전에 이미 로그인했으므로 기존 웹앱 컨테이너 목록이 표시됩니다. Java 응용 프로그램을 게시하거나 다시 게시할 컨테이너를 선택하고 **확인**을 클릭합니다.

몇 초 후 **Azure 동작 로그** 보기에 업데이트된 배포가 **게시됨**으로 표시되고, 웹 브라우저에서 업데이트된 응용 프로그램을 확인할 수 있습니다.

## 기존 웹앱 시작 또는 중지
기존 Azure 웹앱 컨테이너(여기에 배포된 모든 Java 응용 프로그램 포함)를 시작 또는 중지하려면 **Azure 탐색기** 보기를 사용하면 됩니다.

**Azure 탐색기** 보기가 열려 있지 않은 경우 IntelliJ에서 **View** 메뉴를 클릭한 다음 **Tools Windows**, **Service Explorer**를 차례로 클릭합니다. 이전에 로그인하지 않은 경우 로그인하라는 메시지가 나타납니다.

**Azure 탐색기** 보기가 표시되면 다음 단계에 따라 웹앱을 시작하거나 중지합니다.

1. **Azure** 노드를 확장합니다.
2. **웹앱** 노드를 확장합니다.
3. 원하는 웹앱을 마우스 오른쪽 단추로 클릭합니다.
4. 상황에 맞는 메뉴가 나타나면 **시작** 또는 **중지**를 클릭합니다. 메뉴 선택 항목은 상황별로 변경되므로 실행 중인 웹앱만 중지하고, 현재 실행되고 있지 않은 웹앱만 시작할 수 있습니다.
   
    ![][18]

## 다음 단계
Java IDE용 Azure 도구 키트에 대한 자세한 내용은 다음 링크를 참조하세요.

* [Eclipse용 Azure 도구 키트]
  * [Eclipse용 Azure 도구 키트 설치]
  * [Eclipse에서 Azure용 Hello World 웹앱 만들기]
  * [Eclipse용 Azure 도구 키트의 새로운 기능]
* [IntelliJ용 Azure 도구 키트]
  * [IntelliJ용 Azure 도구 키트 설치]
  * *IntelliJ에서 Azure용 Hello World 웹앱 만들기(이 문서)*
  * [IntelliJ용 Azure 도구 키트의 새로운 기능]

Java와 함께 Azure를 사용하는 방법에 대한 자세한 내용은 [Azure Java 개발자 센터]를 참조하세요.

Azure 웹앱 만들기에 대한 자세한 내용은 [웹앱 개요]를 참조하세요.

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[Eclipse용 Azure 도구 키트]: ../azure-toolkit-for-eclipse.md
[IntelliJ용 Azure 도구 키트]: ../azure-toolkit-for-intellij.md
[Eclipse에서 Azure용 Hello World 웹앱 만들기]: ./app-service-web-eclipse-create-hello-world-web-app.md
[Create a Hello World Web App for Azure in IntelliJ]: ./app-service-web-intellij-create-hello-world-web-app.md
[Eclipse용 Azure 도구 키트 설치]: ../azure-toolkit-for-eclipse-installation.md
[IntelliJ용 Azure 도구 키트 설치]: ../azure-toolkit-for-intellij-installation.md
[Eclipse용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-eclipse-whats-new.md
[IntelliJ용 Azure 도구 키트의 새로운 기능]: ../azure-toolkit-for-intellij-whats-new.md

[Azure Java 개발자 센터]: https://azure.microsoft.com/develop/java/
[웹앱 개요]: ./app-service-web-overview.md

<!-- IMG List -->

[01]: ./media/app-service-web-intellij-create-hello-world-web-app/01-Web-Page.png
[02]: ./media/app-service-web-intellij-create-hello-world-web-app/02-File-New-Project.png
[03a]: ./media/app-service-web-intellij-create-hello-world-web-app/03-New-Project-Dialog.png
[03b]: ./media/app-service-web-intellij-create-hello-world-web-app/03-No-SDK-Specified.png
[04]: ./media/app-service-web-intellij-create-hello-world-web-app/04-New-Project-Dialog.png
[05]: ./media/app-service-web-intellij-create-hello-world-web-app/05-Open-Index-Page.png
[06]: ./media/app-service-web-intellij-create-hello-world-web-app/06-Azure-Publish-Context-Menu.png
[07]: ./media/app-service-web-intellij-create-hello-world-web-app/07-Azure-Log-In-Dialog.png
[08]: ./media/app-service-web-intellij-create-hello-world-web-app/08-Manage-Subscriptions.png
[09]: ./media/app-service-web-intellij-create-hello-world-web-app/09-App-Containers.png
[10]: ./media/app-service-web-intellij-create-hello-world-web-app/10-Add-App-Container.png
[11]: ./media/app-service-web-intellij-create-hello-world-web-app/11-New-App-Container.png
[12]: ./media/app-service-web-intellij-create-hello-world-web-app/12-New-Resource-Group.png
[13]: ./media/app-service-web-intellij-create-hello-world-web-app/13-New-App-Service-Plan.png
[14]: ./media/app-service-web-intellij-create-hello-world-web-app/14-New-App-Container.png
[15]: ./media/app-service-web-intellij-create-hello-world-web-app/15-Deploy-To-Azure.png
[16]: ./media/app-service-web-intellij-create-hello-world-web-app/16-Progress-Indicator.png
[17]: ./media/app-service-web-intellij-create-hello-world-web-app/17-Browse-Web-App.png
[18]: ./media/app-service-web-intellij-create-hello-world-web-app/18-Stop-Web-App.png

<!---HONumber=AcomDC_0817_2016-->
