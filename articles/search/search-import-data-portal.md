---
title: "Azure Portal에서 인덱서를 사용하여 Azure Search로 데이터 가져오기 | Microsoft Docs"
description: "Azure Portal에서 Azure Search 데이터 가져오기 마법사를 사용하여 Azure VM에 있는 Azure Blob Storage, Table Storage, SQL Database 및 SQL Server에서 데이터를 크롤링합니다."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 08/29/2016
ms.author: heidist
translationtype: Human Translation
ms.sourcegitcommit: 2ea002938d69ad34aff421fa0eb753e449724a8f
ms.openlocfilehash: 2a0f4c9c5942ee75b9ca4f3924198e8a8ad8ccc7


---
# <a name="import-data-to-azure-search-using-the-portal"></a>포털을 사용하여 Azure 검색으로 데이터 가져오기
Azure Portal에는 Azure Search 대시보드에서 인덱스에 데이터를 로드하기 위한 **데이터 가져오기** 명령이 있습니다. 

  ![명령 모음에서 데이터 가져오기][1]

마법사는 내부적으로 *인덱서*를 구성하고 호출하여 인덱싱 프로세스의 여러 단계를 자동화합니다. 

* 현재 Azure 구독에서 외부 데이터 원본에 연결
* 원본 데이터 구조를 기반으로 하는 인덱스 스키마 자동 생성
* 데이터 원본에서 검색된 행 집합을 기반으로 하는 문서 만들기
* 검색 서비스의 인덱스에 문서 업로드

DocumentDB에서 샘플 데이터를 사용하여 이 워크플로를 시도해 볼 수 있습니다. 지침은 [Azure Portal에서 Azure Search 시작](search-get-started-portal.md) 을 방문하세요.

## <a name="data-sources-supported-by-the-import-data-wizard"></a>데이터 가져오기 마법사에서 지원하는 데이터 원본
데이터 가져오기 마법사에서는 다음 데이터 원본을 지원합니다. 

* Azure SQL 데이터베이스
* Azure VM에서 SQL Server 관계형 데이터
* Azure DocumentDB
* Azure Blob Storage(미리 보기 상태)
* Azure Table Storage(미리 보기 상태)

일반 데이터 집합은 필수 입력입니다. 단일 테이블, 데이터베이스 뷰 또는 동등한 데이터 구조에서만 가져올 수 있습니다. 마법사를 실행하기 전에 이 데이터 구조를 만들어야 합니다.

인덱서 중 몇 가지는 미리 보기 상태입니다. 즉, 인덱서 정의가 미리 보기 버전의 API에서 지원됩니다. 자세한 내용과 링크는 [인덱서 개요](search-indexer-overview.md)를 참조하세요.

## <a name="connect-to-your-data"></a>데이터에 연결
1. [Azure Portal](https://portal.azure.com) 에 로그인하여 서비스 대시보드를 엽니다. 표시줄에서 **검색 서비스** 를 클릭하면 현재 구독에서 기존 서비스를 보여 줄 수 있습니다. 
2. 명령 모음에서 **데이터 가져오기** 를 클릭하여 데이터 블레이드 가져오기를 엽니다.  
3. **데이터에 연결** 을 클릭하여 인덱서에 의해 사용되는 데이터 원본 정의를 지정합니다. 구독 내 데이터 원본의 경우 마법사는 일반적으로 연결 정보를 감지하고 참고하여 전체 구성 요구 사항을 최소화할 수 있습니다.

|  |  |
| --- | --- |
| **기존 데이터 원본** |검색 서비스에 정의된 인덱서가 이미 있는 경우 다른 가져오기에 기존 데이터 원본 정의를 선택할 수 있습니다. |
| **Azure SQL 데이터베이스** |읽기 권한이 포함된 데이터베이스 사용자에 대한 서비스 이름, 자격 증명 및 데이터베이스 이름은 페이지에 또는 ADO.NET 연결 문자열을 통해 지정될 수 있습니다. 연결 문자열 옵션을 선택하여 속성을 보거나 사용자 지정합니다. <br/><br/>행 집합을 제공하는 테이블 또는 보기는 페이지에 지정되어야 합니다. 연결에 성공한 후에 이 옵션이 나타나면 선택할 수 있는 드롭다운 목록을 제공합니다. |
| **Azure VM에서 SQL Server** |정규화된 서비스 이름, 사용자 ID와 암호 및 데이터베이스를 연결 문자열로 지정합니다. 이 데이터 원본을 사용하려면 연결을 암호화하는 로컬 저장소에 미리 인증서를 설치해야 합니다. <br/><br/>행 집합을 제공하는 테이블 또는 보기는 페이지에 지정되어야 합니다. 연결에 성공한 후에 이 옵션이 나타나면 선택할 수 있는 드롭다운 목록을 제공합니다. |
| **DocumentDB** |요구 사항은 계정, 데이터베이스 및 컬렉션을 포함합니다. 컬렉션의 모든 문서는 인덱스에 포함됩니다. 쿼리를 정의하여 집합을 평면화하거나 필터링하고 또는 후속 데이터 새로 고침 작업을 위해 변경된 문서를 감지할 수 있습니다. |
| **Azure Blob Storage** |요구 사항은 저장소 계정 및 컨테이너를 포함합니다. 필요에 따라 그룹화 목적으로 Blob 이름이 가상 명명 규칙을 따르는 경우 이름의 가상 디렉터리 부분을 컨테이너의 폴더로 지정할 수 있습니다. 자세한 내용은 [Blob Storage 인덱싱(미리 보기)](search-howto-indexing-azure-blob-storage.md) 를 참조하세요. |
| **Azure 테이블 저장소** |요구 사항은 저장소 계정 및 테이블 이름을 포함합니다. 필요에 따라 쿼리를 지정하여 테이블의 하위 집합을 검색할 수 있습니다. 자세한 내용은 [Table Storage 인덱싱(미리 보기)](search-howto-indexing-azure-tables.md) 를 참조하세요. |

## <a name="customize-target-index"></a>대상 인덱스 사용자 지정
임시 인덱스는 일반적으로 데이터 집합에서 유추됩니다. 필드를 추가, 편집 또는 삭제하여 스키마를 완료합니다. 또한 필드 수준에서 특성을 설정하여 해당 후속 검색 동작을 결정합니다.

1. **대상 인덱스 사용자 지정**에서 각 문서를 고유하게 식별하는 데 사용한 이름 및 **키**를 지정합니다. 키는 문자열이어야 합니다. 필드 값에 공백이나 대시가 포함되는 경우 **데이터 가져오기** 에서 고급 옵션을 설정하여 이러한 문자에 대한 유효성 검사를 표시하지 않도록 합니다.
2. 나머지 필드를 검토하고 수정합니다. 필드 이름 및 형식은 일반적으로 채워집니다. 데이터 형식을 변경할 수 있습니다.
3. 다음과 같이 각 필드에 대한 인덱스 특성을 설정합니다.
   
   * 검색 가능은 검색 결과에 필드를 반환합니다.
   * 필터링 가능을 선택하면 필드를 필터 식에서 참조할 수 있습니다.
   * 정렬 가능을 선택하면 필드를 정렬에 사용할 수 있습니다.
   * 패싯 가능을 통해 필드를 패싯 탐색에 사용할 수 있습니다.
   * 검색 가능을 통해 전체 텍스트를 검색할 수 있습니다.
4. 필드 수준에서 언어 분석기를 지정 하려는 경우 **분석기** 탭을 클릭합니다. 언어 분석기만이 이번에 지정될 수 있습니다. 사용자 지정 분석기 또는 키워드, 패턴, 등과 같은 비언어 분석기를 사용하려면 코드가 필요합니다.
   
   * **검색 가능** 을 클릭하여 필드에서 전체 텍스트 검색을 지정하고 분석기 드롭 다운 목록을 사용하도록 설정합니다.
   * 원하는 분석기를 선택합니다. 자세한 내용은 [여러 언어의 문서에 대한 인덱스 만들기](search-language-support.md) 를 참조하세요.
5. **확인기** 를 클릭하여 선택한 필드에 미리 입력 쿼리 제안을 사용할 수 있도록 합니다.

## <a name="import-your-data"></a>데이터 가져오기
1. **데이터 가져오기**에 인덱서의 이름을 입력합니다. 데이터 가져오기 마법사의 제품이 인덱서라는 점에 유의하세요. 나중에 이 항목을 보거나 편집하려는 경우 마법사를 다시 실행하여 포털에서 해당 항목을 선택합니다. 
2. 일정을 지정하며, 이는 서비스가 프로비전되는 지역 표준 시간대를 기반으로 합니다.
3. 고급 옵션을 설정하여 문서를 삭제할 경우 인덱싱을 계속할 수 있는지에 대한 임계값을 지정합니다. 또한 **키** 필드에 공백 및 슬래시를 포함하도록 허용되는지를 지정할 수 있습니다.  

## <a name="edit-an-existing-indexer"></a>기존 인덱서 편집
서비스 대시보드에서 인덱서 타일을 두 번 클릭하여 구독에 대해 생성된 모든 인덱서 목록을 슬라이드 아웃합니다. 인덱서 중 하나를 두 번 클릭하여 실행하거나 편집하거나 삭제합니다. 인덱스를 기존의 다른 인덱스로 대체하고 데이터 원본을 변경하며 인덱싱 중에 오류 임계값에 대한 옵션을 설정할 수 있습니다.

## <a name="edit-an-existing-index"></a>기존 인덱스 편집
Azure 검색에서 인덱스에 대한 구조적 업데이트를 위해서는 해당 인덱스를 다시 빌드해야 하며 이 과정은 인덱스 삭제, 인덱스 다시 생성, 데이터 다시 로드로 구성됩니다. 구조적 업데이트에는 데이터 형식을 변경하고 필드 이름을 바꾸거나 삭제하는 과정이 포함됩니다.

다시 빌드가 필요하지 않는 편집에는 새 필드 추가, 점수 매기기 프로필 변경, 확인기 변경 또는 언어 분석기 변경이 포함됩니다. 자세한 내용은 [인덱스 업데이트](https://msdn.microsoft.com/library/azure/dn800964.aspx) 를 참조하세요.

## <a name="next-step"></a>다음 단계
인덱서에 대해 자세히 알아보려면 다음 링크를 검토합니다.

* [Azure SQL Database 인덱싱](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [DocumentDB 인덱싱](../documentdb/documentdb-search-indexer.md)
* [Blob Storage 인덱싱(미리 보기)](search-howto-indexing-azure-blob-storage.md)
* [Table Storage 인덱싱(미리 보기)](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png




<!--HONumber=Nov16_HO2-->


