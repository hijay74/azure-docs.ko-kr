---
title: '스트림 분석: 입력 및 출력에 대한 로그인 자격 증명 회전 | Microsoft Docs'
description: 스트림 분석 입력 및 출력에 대한 자격 증명을 업데이트 하는 방법에 대해 알아봅니다.
keywords: 로그인 자격 증명
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun

ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 09/26/2016
ms.author: jeffstok

---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a>스트림 분석 작업에서 입력 및 출력을 위한 로그인 자격 증명 회전
## <a name="abstract"></a>요약
오늘날 Azure 스트림 분석은 작업이 실행되는 동안에 입/출력 시 자격 증명을 대체할 수 없습니다.

Azure 스트림 분석은 마지막 출력에서 작업 재시작을 지원하지만, 작업의 중지 및 시작과 로그인 자격 증명 회전 사이의 간격을 최소화하기 위해 전체 프로세스를 공유합니다.

## <a name="part-1---prepare-the-new-set-of-credentials:"></a>1부-새로운 자격 증명 집합을 준비합니다.
이 부분은 다음 입력/출력에 적용할 수 있습니다.

* Blob 저장소
* 이벤트 허브(영문)
* SQL 데이터베이스
* 테이블 저장소

다른 입력/출력의 경우 2부를 진행합니다.

### <a name="blob-storage/table-storage"></a>Blob 저장소/테이블 저장소
1. Azure 관리 포털에서 Storage 확장명으로 이동합니다.  
   ![graphic1][graphic1]
2. 사용자 작업에서 사용되는 Storage를 찾아 이동합니다.  
   ![graphic2][graphic2]
3. 액세스 키 관리 명령을 클릭합니다.  
   ![graphic3][graphic3]
4. 기본 액세스 키 및 보조 액세스 키 사이에서 **작업에서 사용되지 않는 키를 선택합니다**.
5. 히트 다시 생성:   
   ![graphic4][graphic4]
6. 새로 생성된 키를 복사합니다.  
   ![graphic5][graphic5]
7. 2부를 계속합니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
1. Azure 관리 포털에서 Service Bus 확장명으로 이동합니다.  
   ![graphic6][graphic6]
2. 작업에서 사용하는 Service Bus 네임스페이스를 찾아 이동합니다.  
   ![graphic7][graphic7]
3. 작업이 서비스 버스 네임스페이스에서 공유 액세스 정책을 사용하는 경우 6단계로 이동합니다.  
4. Event Hubs 탭으로 이동합니다.  
   ![graphic8][graphic8]
5. 사용자 작업에서 사용되는 Event Hubs를 찾아 이동합니다.  
   ![graphic9][graphic9]
6. 구성 탭으로 이동합니다.  
   ![graphic10][graphic10]
7. 정책 이름 드롭다운 목록에서 작업에서 사용되는 공유 액세스 정책을 찾습니다.  
   ![graphic11][graphic11]
8. 기본 키와 보조 키 사이에서 **작업에서 사용되지 않는 키를 선택합니다**.  
9. 히트 다시 생성:   
   ![graphic12][graphic12]
10. 새로 생성된 키를 복사합니다.  
    ![graphic13][graphic13]
11. 2부를 계속합니다.  

### <a name="sql-database"></a>SQL 데이터베이스
> [!NOTE]
> 참고: SQL 데이터베이스 서비스에 연결해야 합니다. Azure 관리 포털에서 관리 환경을 사용하여 이를 수행하는 방법을 보여줄 수 있지만 SQL Server Management Studio와 같은 일부 클라이언트측 도구를 함께 사용하 여 선택할 수 있습니다.
> 
> 

1. Azure 관리 포털에서 SQL Database 확장명으로 이동합니다.  
   ![graphic14][graphic14]
2. 작업에서 사용되는 SQL Database를 찾아 동일한 줄에 있는 **서버 링크를 클릭합니다.**  
   ![graphic15][graphic15]
3. 관리 명령을 클릭합니다.  
   ![graphic16][graphic16]
4. 데이터베이스 마스터 유형:   
   ![graphic17][graphic17]
5. 사용자 이름, 암호를 입력하고 로그를 클릭합니다.  
   ![graphic18][graphic18]
6. 새 쿼리를 클릭합니다.  
   ![graphic19][graphic19]
7. <login_name>을 사용자 이름으로 교체하고 <enterStrongPasswordHere>를 새 암호로 교체하여 다음 쿼리를 입력합니다.  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. 실행을 클릭합니다.  
   ![graphic20][graphic20]
9. 2단계로 돌아가서 데이터베이스를 클릭합니다.  
   ![graphic21][graphic21]
10. 관리 명령을 클릭합니다.  
    ![graphic22][graphic22]
11. 사용자 이름, 암호를 입력하고 로그를 클릭합니다.  
    ![graphic23][graphic23]
12. 새 쿼리를 클릭합니다.  
    ![graphic24][graphic24]
13. 이 데이터베이스의 컨텍스트에서 이 로그인을 식별할 이름으로 <user_name>을 대체하고(예를 들어, <login_name>에 대해 동일한 값을 제공할 수 있음) 및 새 사용자 이름으로 <login_name>을 대체하는 다음 쿼리에 입력합니다.  
    `CREATE USER <user_name> FROM LOGIN <login_name>`
14. 실행을 클릭합니다.  
    ![graphic25][graphic25]
15. 이제 원래 사용자가 가졌던 동일한 역할과 권한을 새로운 사용자에게 제공해야 합니다.
16. 2부를 계속합니다.

## <a name="part-2:-stopping-the-stream-analytics-job"></a>2부: 스트림 분석 작업 중지
1. Azure 관리 포털에서 Stream Analytics 확장으로 이동합니다.  
   ![graphic26][graphic26]
2. 작업을 찾아 이동합니다.  
   ![graphic27][graphic27]
3. 입력 또는 출력의 자격 증명을 회전하는 지 여부에 따라 입력 탭이나 출력 탭으로 이동합니다.  
   ![graphic28][graphic28]
4. 중지 명령을 클릭하고  
   ![graphic29][graphic29] 작업이 중지되었는지 확인합니다. 작업이 중지될 때까지 기다립니다.
5. 자격 증명을 회전할 입/출력을 찾아 이동합니다.  
   ![graphic30][graphic30]
6. 3부로 이동합니다.

## <a name="part-3:-editing-the-credentials-on-the-stream-analytics-job"></a>3 부: 스트림 분석 작업에서 자격 증명 편집
### <a name="blob-storage/table-storage"></a>Blob 저장소/테이블 저장소
1. Storage 계정 키 필드를 찾아 새로 생성된 키를 붙여넣습니다.  
   ![graphic31][graphic31]
2. 저장 명령을 클릭하고 변경 내용 저장을 확인합니다.  
   ![graphic32][graphic32]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
4. 4부로 이동합니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
1. Event Hubs 정책 키 필드를 찾아 새로 생성된 키를 붙여넣습니다.  
   ![graphic33][graphic33]
2. 저장 명령을 클릭하고 변경 내용 저장을 확인합니다.  
   ![graphic34][graphic34]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
4. 4부로 이동합니다.

### <a name="power-bi"></a>Power BI
1. 권한 부여 갱신을 클릭합니다.  
2. ![graphic35][graphic35]
3. 다음 확인 메시지가 나타납니다.  
4. ![graphic36][graphic36]
5. 저장 명령을 클릭하고 변경 내용 저장을 확인합니다.  
   ![graphic37][graphic37]
6. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.
7. 4부로 이동합니다.

### <a name="sql-database"></a>SQL 데이터베이스
1. 사용자 이름 및 암호 필드를 찾아 새로 만든 자격 증명 집합을 붙여넣습니다.  
   ![graphic38][graphic38]
2. 저장 명령을 클릭하고 변경 내용 저장을 확인합니다.  
   ![graphic39][graphic39]
3. 변경 내용을 저장할 때 연결 테스트가 자동으로 시작되며 성공적으로 통과했는지 확인합니다.  
4. 4부로 이동합니다.

## <a name="part-4:-starting-your-job-from-last-stopped-time"></a>4부: 마지막 중지된 시간에서 해당 작업 시작
1. 입/출력에서 다른 부분으로 이동합니다.  
   ![graphic40][graphic40]
2. 시작 명령을 클릭합니다.  
   ![graphic41][graphic41]
3. 마지막 중지 시간을 선택하고 확인을 클릭합니다.  
   ![graphic42][graphic42]
4. 5부로 이동합니다.  

## <a name="part-5:-removing-the-old-set-of-credentials"></a>5부: 이전 자격 증명 집합 제거
이 부분은 다음 입력/출력에 적용할 수 있습니다.

* Blob 저장소
* 이벤트 허브(영문)
* SQL 데이터베이스
* 테이블 저장소

### <a name="blob-storage/table-storage"></a>Blob 저장소/테이블 저장소
이제 사용되지 않은 액세스 키를 갱신하 도록 이전에 작업에서 사용한 액세스 키에 대해 1부를 반복합니다.

### <a name="event-hubs"></a>이벤트 허브(영문)
이제 사용되지 않은 키를 갱신하도록 이전에 작업에서 사용한 키에 대해 1부를 반복합니다.

### <a name="sql-database"></a>SQL 데이터베이스
1. 1부 7단계의 쿼리 창으로 돌아가서 <previous_login_name>을 이전에 사용자가 작업에 사용한 사용자 이름으로 바꾸고 다음 쿼리를 입력합니다.  
   `DROP LOGIN <previous_login_name>`  
2. 실행을 클릭합니다.  
   ![graphic43][graphic43]  

다음 확인 메시지가 나타나야 합니다. 

    Command(s) completed successfully.

## <a name="get-help"></a>도움말 보기
추가 지원이 필요할 경우 [Azure 스트림 분석 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)

## <a name="next-steps"></a>다음 단계
* [Azure 스트림 분석 소개](stream-analytics-introduction.md)
* [Azure 스트림 분석 사용 시작](stream-analytics-get-started.md)
* [Azure 스트림 분석 작업 규모 지정](stream-analytics-scale-jobs.md)
* [Azure 스트림 분석 쿼리 언어 참조](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 스트림 분석 관리 REST API 참조](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png




<!--HONumber=Oct16_HO2-->


