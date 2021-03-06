---
title: 범용 Windows 앱에서 Azure Blob 저장소에 이미지 업로드 | Microsoft Docs
description: .NET 백엔드 모바일 서비스를 사용하여 Azure Blob 저장소에 이미지를 업로드하고 범용 Windows 앱에서 이미지에 액세스하는 방법 알아보기
documentationcenter: windows
author: ggailey777
services: mobile-services,storage
manager: dwrede
editor: ''

ms.service: mobile-services
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 07/21/2016
ms.author: glenga

---
# 모바일 서비스를 사용하여 Azure 저장소에 이미지 업로드
[!INCLUDE [mobile-service-note-mobile-apps](../../includes/mobile-services-note-mobile-apps.md)]

&nbsp;

[!INCLUDE [mobile-services-selector-upload-data-blob-storage](../../includes/mobile-services-selector-upload-data-blob-storage.md)]

## 개요
이 항목에서는 Azure 모바일 서비스를 사용하여, 사용자가 만든 이미지를 앱에서 Azure 저장소에 업로드하고 저장하는 방법에 대해 설명합니다. 모바일 서비스에서는 SQL 데이터베이스를 사용하여 데이터를 저장합니다. 그러나 Azure Blob 저장소 서비스에는 Blob(Binary Large Object) 데이터를 저장하는 것이 좀 더 효율적입니다.

클라이언트 앱에서는 Blob 저장소 서비스에 데이터를 안전하게 업로드하는 데 필요한 자격 증명을 안전하게 배포할 수 없습니다. 대신 이러한 자격 증명을 모바일 서비스에 저장하고, 이를 통해 새로운 이미지 업로드에 사용되는 SAS(공유 액세스 서명)를 생성해야 합니다. 만료 기간이 짧은(이 경우 5분) 자격 증명인 SAS는 모바일 서비스에 의해 클라이언트 앱으로 안전하게 반환됩니다. 그러면 앱은 이 임시 자격 증명을 사용하여 이미지를 업로드합니다. 이 예제에서 Blob 서비스의 다운로드 파일은 공개 파일입니다.

이 자습서에서는 모바일 서비스에서 생성한 SAS를 사용하여 사진을 찍고 이미지를 Azure에 업로드하는 기능을 모바일 서비스 퀵 스타트 앱에 추가합니다.

## 필수 조건
이 자습서를 사용하려면 다음이 필요합니다.

* Microsoft Visual Studio 2013 Update 3 이상 버전
* [Azure 저장소 계정](../storage/storage-create-storage-account.md)
* 컴퓨터에 연결되는 카메라 또는 기타 이미지 캡처 장치

이 자습서는 모바일 서비스 quickstart를 기반으로 합니다. 이 자습서를 시작하기 전에 먼저 [모바일 서비스 시작하기]를 완료해야 합니다.

[!INCLUDE [mobile-services-dotnet-backend-configure-blob-storage](../../includes/mobile-services-dotnet-backend-configure-blob-storage.md)]

[!INCLUDE [mobile-services-windows-universal-dotnet-upload-to-blob-storage](../../includes/mobile-services-windows-universal-dotnet-upload-to-blob-storage.md)]

## 다음 단계
이제 모바일 서비스를 Blob 서비스와 통합하여 이미지를 안전하게 업로드할 수 있게 되었으므로 몇 가지 기타 백엔드 서비스 및 통합 항목을 확인해보십시오.

* [모바일 서비스에서 백 엔드 작업 예약](mobile-services-dotnet-backend-schedule-recurring-tasks.md)
  
     모바일 서비스 작업 스케줄러 기능을 사용하여, 예약된 시간에 실행되는 서버 스크립트 코드를 정의하는 방법에 대해 알아보십시오.
* [모바일 서비스 .NET 방법 개념 참조](mobile-services-dotnet-how-to-use-client-library.md)
  
     모바일 서비스를 .NET과 함께 사용하는 방법에 대해 알아보십시오.

<!-- Anchors. -->
[Install the Storage Client library]: #install-storage-client
[Update the client app to capture images]: #add-select-images
[Install the storage client in the mobile service project]: #storage-client-server
[Update the TodoItem definition in the data model]: #update-data-model
[Update the table controller to generate an SAS]: #update-scripts
[Upload images to test the app]: #test
[Next Steps]: #next-steps

<!-- Images. -->

<!-- URLs. -->
[모바일 서비스 시작하기]: mobile-services-windows-store-dotnet-get-started.md
[How To Create a Storage Account]: ../storage/storage-create-storage-account.md
[Azure Storage Client library for Store apps]: http://go.microsoft.com/fwlink/p/?LinkId=276866

<!---HONumber=AcomDC_0727_2016-->