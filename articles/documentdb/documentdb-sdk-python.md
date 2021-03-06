---
title: DocumentDB Python API 및 SDK | Microsoft Docs
description: 릴리스 날짜, 사용 중지 날짜 및 DocumentDB Python SDK의 각 버전 간의 변경 내용을 포함하는 Python API 및 SDK에 대한 모든 것을 알아봅니다.
services: documentdb
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun

ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2016
ms.author: rnagpal

---
# DocumentDB API 및 SDK
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Node.JS](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST (영문)](https://go.microsoft.com/fwlink/?LinkId=402413)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

## DocumentDB Python API 및 SDK
<table>

<tr><td>**SDK 다운로드**</td><td>[PyPI](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td>**API 설명서**</td><td>[Python API 참조 설명서](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td>**SDK 설치 지침**</td><td>[Python SDK 설치 지침](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td>**SDK에 참여해 보세요.**</td><td>[GitHub](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td>**시작**</td><td>[Python SDK 시작](documentdb-python-application.md)</td></tr>

<tr><td>**현재 지원되는 플랫폼**</td><td>[Python 2.7](https://www.python.org/download/releases/2.7/)</td></tr>
</table></br>

## 릴리스 정보
### <a name="1.9.0"/>[1\.9.0](https://pypi.python.org/pypi/pydocumentdb/1.9.0)
* 제한된 요청에 대한 재시도 정책 지원이 추가되었습니다. (제한된 요청은 오류 코드 429, 요청 속도가 너무 크다는 예외를 수신합니다.) 기본적으로 오류 코드 429가 발생하면 DocumentDB는 각 요청을 9번 다시 시도하며 응답 헤더에서 retryAfter 시간을 적용합니다. 이제 다시 시도 간의 서버에서 반환한 retryAfter 시간을 무시하려는 경우 고정된 다시 시도 간격 시간은 ConnectionPolicy 개체에서 RetryOptions 속성의 일부로 설정될 수 있습니다. DocumentDB는 제한된 요청 각각에 대해 30초 동안 대기하고(다시 시도 횟수와 관계 없이) 오류 코드 429를 포함하는 응답을 반환합니다. 이 시간도 ConnectionPolicy 개체에 있는 RetryOptions 속성에서 재정의할 수 있습니다.
* 이제 DocumentDB는 x-ms-throttle-retry-count 및 x-ms-throttle-retry-wait-time-ms를 다시 시도 사이에 요청이 대기한 스로틀 다시 시도 수 및 누적 시간을 표시하는 모든 요청의 응답 헤더로 반환합니다.
* document\_client 클래스에 노출된 RetryPolicy 클래스 및 해당 속성(retry\_policy)을 제거하고 대신 일부 기본 다시 시도 옵션을 재정의하는 데 사용할 수 있는 ConnectionPolicy 클래스의 RetryOptions 속성을 노출하는 RetryOptions 클래스를 지정했습니다.

### <a name="1.8.0"/>[1\.8.0](https://pypi.python.org/pypi/pydocumentdb/1.8.0)
* 다중 지역 데이터베이스 계정에 대한 지원이 추가되었습니다.

### <a name="1.7.0"/>[1\.7.0](https://pypi.python.org/pypi/pydocumentdb/1.7.0)
* 문서의 TTL(Time to Live) 기능에 대한 지원이 추가되었습니다.

### <a name="1.6.1"/>[1\.6.1](https://pypi.python.org/pypi/pydocumentdb/1.6.1)
* partitionkey 경로에 특수 문자를 허용하는 서버 쪽 분할과 관련된 버그 수정입니다.

### <a name="1.6.0"/>[1\.6.0](https://pypi.python.org/pypi/pydocumentdb/1.6.0)
* [분할된 컬렉션](documentdb-partition-data.md) 및 [사용자 정의 성능 수준](documentdb-performance-levels.md)이 구현되었습니다.

### <a name="1.5.0"/>[1\.5.0](https://pypi.python.org/pypi/pydocumentdb/1.5.0)
* 여러 파티션 간의 응용 프로그램 분할을 지원하기 위해 해시 및 범위 파티션 해결 프로그램을 추가합니다.

### <a name="1.4.2"/>[1\.4.2](https://pypi.python.org/pypi/pydocumentdb/1.4.2)
* Upsert를 구현합니다. 새로운 UpsertXXX 메서드가 Upsert 기능을 지원하기 위해 추가되었습니다.
* ID 기반 라우팅을 구현합니다. 공용 API 변경 없이 모두 내부에서 변경됩니다.

### <a name="1.2.0"/>[1\.2.0](https://pypi.python.org/pypi/pydocumentdb/1.2.0)
* 지리 공간 인덱스를 지원합니다.
* 모든 리소스에 대한 ID 속성의 유효성을 검사합니다. 리소스에 대한 ID는 ?, /, #, \\, 문자를 포함하거나 공백으로 끝날 수 없습니다.
* ResourceResponse에 새 헤더 "인덱스 변환 진행"을 추가합니다.

### <a name="1.1.0"/>[1\.1.0](https://pypi.python.org/pypi/pydocumentdb/1.1.0)
* V2 인덱싱 정책을 구현합니다.

### <a name="1.0.1"/>[1\.0.1](https://pypi.python.org/pypi/pydocumentdb/1.0.1)
* 프록시 연결을 지원합니다

### <a name="1.0.0"/>[1\.0.0](https://pypi.python.org/pypi/pydocumentdb/1.0.0)
* GA SDK.

## 릴리스 및 사용 중지 날짜
Microsoft는 매끄럽게 최신/지원 버전으로 전환할 수 있도록 적어도 SDK 사용 중지 **12개월** 전에 알림을 제공합니다.

새로운 기능 및 최적화는 현재 SDK에만 추가되어 있으며, 따라서 항상 최신 SDK 버전으로 가능한 한 빨리 업그레이드할 것을 권장합니다.

사용 중지된 SDK를 사용한 DocumentDB에 대한 요청은 서비스로부터 거부됩니다.

> [!WARNING]
> **1.0.0** 이전 버전의 Python에 대한 모든 버전의 Azure DocumentDB SDK는 **2016년 2월 29일**에 사용 중지됩니다.
> 
> 

<br/>

| 버전 | 릴리스 날짜 | 사용 중지 날짜 |
| --- | --- | --- |
| [1.9.0](#1.9.0) |2016년 7월 7일 |--- |
| [1.8.0](#1.8.0) |2016년 7월 14일 |--- |
| [1.7.0](#1.7.0) |2016년 4월 26일 |--- |
| [1.6.1](#1.6.1) |2016년 4월 8일 |--- |
| [1.6.0](#1.6.0) |2016년 3월 29일 |--- |
| [1.5.0](#1.5.0) |2016년 1월 3일 |--- |
| [1\.4.2](#1.4.2) |2015년 10월 6일 |-- |
| [1\.4.1](#1.4.1) |2015년 10월 6일 |-- |
| [1\.2.0](#1.2.0) |2015년 8월 6일 |-- |
| [1\.1.0](#1.1.0) |2015년 7월 9일 |-- |
| [1\.0.1](#1.0.1) |2015년 5월 25일 |-- |
| [1\.0.0](#1.0.0) |2015년 4월 7일 |-- |
| 0.9.4-prelease |2015년 1월 14일 |2016년 2월 29일 |
| 0.9.3-prelease |2014년 12월 9일 |2016년 2월 29일 |
| 0.9.2-prelease |2014년 11월 25일 |2016년 2월 29일 |
| 0.9.1-prelease |2014년 9월 23일 |2016년 2월 29일 |
| 0.9.0-prelease |2014년 8월 21일 |2016년 2월 29일 |

## FAQ
[!INCLUDE [documentdb-sdk-faq](../../includes/documentdb-sdk-faq.md)]

## 참고 항목
DocumentDB에 대해 자세히 알아보려면 [Microsoft Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) 서비스 페이지를 참조하세요.

<!---HONumber=AcomDC_0810_2016-->
