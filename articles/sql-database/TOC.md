# 개요
## [SQL Database 정의](sql-database-technical-overview.md)
## [SQL Database FAQ](sql-database-faq.md)
## 기능
### [서비스 계층](sql-database-service-tiers.md)
### [데이터베이스 트랜잭션 단위](sql-database-what-is-a-dtu.md)
### [DTU 벤치마크 개요](sql-database-benchmark-overview.md)
### [관리 도구](sql-database-manage-overview.md)
## 고려 사항 및 제한 사항
### [VM의 SQL Database 및 SQL](sql-database-paas-vs-sql-server-iaas.md)
### [T-SQL 차이점](sql-database-transact-sql-information.md)
### [리소스 한도](sql-database-resource-limits.md)
### [일반적인 제한 사항](sql-database-general-limitations.md)
### [보안 지침](sql-database-security-guidelines.md)

## 이점
### [학습 및 적응](sql-database-learn-and-adapt.md)
### [즉석에서 확장](sql-database-scale-on-the-fly.md)
### [다중 테넌트 앱 빌드](sql-database-build-multi-tenant-apps.md)
### [보안 및 보호](sql-database-helps-secures-and-protects.md)
### [사용자 환경에서 작동](sql-database-works-in-your-environment.md)

## 시나리오

### 서버, 풀, 데이터베이스 및 방화벽
#### [Elastic Database 풀을 사용하는 경우](sql-database-elastic-pool-guidance.md)
#### [Elastic Database 풀](sql-database-elastic-pool.md)
#### [자동화](sql-database-manage-automation.md)

### 데이터베이스 확장
#### [개요](sql-database-elastic-scale-introduction.md)
#### [확장성 있는 클라우드 데이터베이스 빌드](sql-database-elastic-database-client-library.md)
#### [데이터베이스 간 작업](sql-database-elastic-jobs-overview.md)
#### [탄력적 데이터베이스 도구 용어집](sql-database-elastic-scale-glossary.md)
#### [FAQ](sql-database-elastic-scale-faq.md)

### 액세스 및 사용 권한
#### [개요](sql-database-security.md)
#### [Azure SQL Database에 대한 Azure Security Center](../security-center/security-center-sql-database.md?toc=%2fazure%2fsql-database%2ftoc.json)
#### [SQL 보안 센터](https://msdn.microsoft.com/library/azure/bb510589)

### 비즈니스 연속성
#### [개요](sql-database-business-continuity.md)
#### [데이터베이스 백업](sql-database-automated-backups.md)
#### [백업을 사용한 데이터베이스 복구](sql-database-recovery-using-backups.md)
#### [재해 복구에 대한 인증 요구 사항](sql-database-geo-replication-security-config.md)
#### [비즈니스 연속성 디자인 시나리오](sql-database-designing-cloud-solutions-for-disaster-recovery.md)
#### [탄력적 풀을 사용한 재해 복구 전략](sql-database-disaster-recovery-strategies-for-applications-with-elastic-pool.md)
#### [롤링 업그레이드](sql-database-manage-application-rolling-upgrade.md)

### [데이터베이스 개발](sql-database-develop-overview.md)
### [SQL Server 데이터베이스 마이그레이션](sql-database-cloud-migrate.md)

## 고객 구현
### [Daxko/CSI 소프트웨어](sql-database-implementation-daxko.md)
### [GEP](sql-database-implementation-gep.md)
### [SnelStart](sql-database-implementation-snelstart.md)
### [Umbraco](sql-database-implementation-umbraco.md)


# 시작
## [솔루션 빠른 시작](sql-database-solution-quick-starts.md)
## SQL Database 만들기
### [Azure 포털](sql-database-get-started.md)
### [C#](sql-database-get-started-csharp.md)
### [PowerShell](sql-database-get-started-powershell.md)
## 규모가 확장된 데이터베이스 만들기 및 관리
### [탄력적 확장](sql-database-elastic-scale-get-started.md)
### [탄력적 작업](sql-database-elastic-jobs-getting-started.md)
### [크로스 데이터베이스 보고서](sql-database-elastic-query-getting-started.md)
### [크로스 데이터베이스 쿼리](sql-database-elastic-query-getting-started-vertical.md)
## 데이터베이스 모니터링 및 튜닝
### [SQL Database 관리자 개요](sql-database-advisor.md)
### [Azure Portal의 워크로드 정보](sql-database-performance.md)
## [액세스 및 사용 권한 만들기 및 관리](sql-database-get-started-security.md)
## [메모리 내 최적화](sql-database-in-memory.md)
## [데이터 동기화](sql-database-get-started-sql-data-sync.md)

# 방법

## 만들기 및 관리
### 서버 및 데이터베이스
#### [단일 데이터베이스](sql-database-manage-portal.md)
#### [Azure 포털](sql-database-get-started.md)
#### [C#](sql-database-get-started-csharp.md)
#### [PowerShell](sql-database-manage-powershell.md)
#### [SQL Server Management Studio](sql-database-manage-azure-ssms.md)
### 탄력적 데이터베이스 풀
#### [Azure 포털](sql-database-elastic-pool-create-portal.md)
#### [PowerShell](sql-database-elastic-pool-create-powershell.md)
#### [C#](sql-database-elastic-pool-create-csharp.md)
#### [T-SQL](sql-database-elastic-pool-manage-tsql.md)
### 분할된 데이터베이스
#### [분할된 데이터베이스 맵 관리자 사용](sql-database-elastic-scale-shard-map-management.md)
#### [분할 병합 보안 구성](sql-database-elastic-scale-split-merge-security-configuration.md)
#### [Dapper 작업](sql-database-elastic-scale-working-with-dapper.md)
#### [엔터티 프레임워크 사용](sql-database-elastic-scale-use-entity-framework-applications-visual-studio.md)
#### [데이터 종속 라우팅](sql-database-elastic-scale-data-dependent-routing.md)
#### [다중 테넌트 행 수준 보안](sql-database-elastic-tools-multi-tenant-row-level-security.md)
#### [자격 증명 관리](sql-database-elastic-scale-manage-credentials.md)
#### [분할/병합 서비스 배포](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
#### [분할된 데이터베이스 추가](sql-database-elastic-scale-add-a-shard.md)
#### [RecoveryManager 클래스를 사용하여 분할된 데이터베이스 맵 문제 해결](sql-database-elastic-database-recovery-manager.md)
###  인증
#### [Azure AD 인증](sql-database-aad-authentication.md)
#### [Multi-Factor Authentication](sql-database-ssms-mfa-authentication.md)
### 방화벽 규칙
#### [Azure Portal](sql-database-configure-firewall-settings.md)
#### [PowerShell](sql-database-configure-firewall-settings-powershell.md)
#### [REST API](sql-database-configure-firewall-settings-rest.md)
#### [T-SQL](sql-database-configure-firewall-settings-tsql.md)
### 작업
#### [서비스 설치](sql-database-elastic-jobs-service-installation.md)
#### [Azure Portal](sql-database-elastic-jobs-create-and-manage.md)
#### [PowerShell](sql-database-elastic-jobs-powershell.md)
#### [클라이언트 라이브러리 업그레이드](sql-database-elastic-scale-upgrade-client-library.md)
### [로그인](sql-database-manage-logins.md)

## 개발
### [개요](https://msdn.microsoft.com/library/mt763826.aspx)
### [연결 라이브러리](sql-database-libraries.md)
### 시나리오
#### [다중 테넌트 SaaS 응용 프로그램](sql-database-design-patterns-multi-tenancy-saas-applications.md)
#### [JSON 데이터](sql-database-json-features.md)
#### [임시 테이블](sql-database-temporal-tables.md)
#### [보존 정책](sql-database-temporal-tables-retention-policy.md)
### 응용 프로그램 연결
#### [.NET](sql-database-develop-dotnet-simple.md)
#### [Java](sql-database-develop-java-simple.md)
#### [Node.JS](sql-database-develop-nodejs-simple.md)
#### [PHP](sql-database-develop-php-simple.md)
#### [Python](sql-database-develop-python-simple.md)
#### [Ruby](sql-database-develop-ruby-simple.md)
#### [Excel](sql-database-connect-excel.md)
#### [Visual Studio](sql-database-connect-query.md)

### [데이터베이스 만들기](sql-database-get-started-powershell.md)
### 탄력적 풀 관리
#### [PowerShell](sql-database-elastic-pool-manage-powershell.md)
#### [C#](sql-database-elastic-pool-manage-csharp.md)
### [응용 프로그램 인증을 위한 필수 값 가져오기](sql-database-client-id-keys.md)
### [ADO.NET 4.5에 대해 1433 이외의 포트 사용](sql-database-develop-direct-route-ports-adonet-v12.md)
### [오류 메시지 작업](sql-database-develop-error-messages.md)
### [일괄 처리 사용](sql-database-use-batching-to-improve-performance.md)

### 참조
#### [.NET(개념)](https://msdn.microsoft.com/library/kb9s9ks0.aspx)
#### [.NET(API 참조)](https://msdn.microsoft.com/library/system.data.sqlclient.aspx)
#### [Entity Framework](https://www.nuget.org/packages/EntityFramework/)
#### [Azure SDK(다운로드)](https://www.visualstudio.com/vs/azure-tools/)
#### [Azure SDK(설명서)](../dotnet-sdk.md)
#### [PowerShell 서비스 관리 cmdlet](https://msdn.microsoft.com/library/azure/dn546723.aspx)
#### REST
##### [REST(리소스 관리)](https://msdn.microsoft.com/library/azure/mt420159)
##### [REST(서비스 관리)](https://msdn.microsoft.com/library/azure/dn505719.aspx)

## 위협 감지
### [위협 감지](sql-database-threat-detection-get-started.md)
### [방화벽](sql-database-firewall-configure.md)

## 데이터 암호화
### [상시 암호화 개요](sql-database-always-encrypted.md)
### [상시 암호화 Azure Key Vault](sql-database-always-encrypted-azure-key-vault.md)
### [투명한 데이터 암호화](https://msdn.microsoft.com/library/azure/dn948096)
### [열 암호화](https://msdn.microsoft.com/library/azure/ms179331)

## 데이터 마스킹
### [동적 데이터 마스킹](sql-database-dynamic-data-masking-get-started-portal.md)
### [하위 수준 클라이언트](sql-database-auditing-and-dynamic-data-masking-downlevel-clients.md)

## 마이그레이션
### 호환성 확인
#### [SQL 패키지 유틸리티](sql-database-cloud-migrate-determine-compatibility-sqlpackage.md)
#### [SQL Server Management Studio](sql-database-cloud-migrate-determine-compatibility-ssms.md)
### 호환성 문제 해결
#### [SQL Server Data Tools](sql-database-cloud-migrate-fix-compatibility-issues-ssdt.md)
#### [SQL Server Management Studio](sql-database-cloud-migrate-fix-compatibility-issues-ssms.md)
#### [SQL Azure 마이그레이션 마법사](sql-database-cloud-migrate-fix-compatibility-issues.md)
### [SQL Server Management Studio 마이그레이션 마법사 사용](sql-database-cloud-migrate-compatible-using-ssms-migration-wizard.md)
### [트랜잭션 복제 사용](sql-database-cloud-migrate-compatible-using-transactional-replication.md)
### [기존 확장된 데이터베이스를 확장하도록 마이그레이션](sql-database-elastic-convert-to-use-elastic-tools.md)

## 모니터링 및 튜닝
### [단일 데이터베이스](sql-database-performance-guidance.md)
### [Query Performance Insight](sql-database-query-performance.md)
### [SQL Database 관리자](sql-database-advisor-portal.md)
### [데이터베이스 성능](sql-database-single-database-monitor.md)
### [DMV](sql-database-monitoring-with-dmvs.md)
### [호환성 수준](sql-database-compatibility-level-query-performance-130.md)
### [이벤트 감사](sql-database-auditing-get-started.md)
### [분할된 맵 관리자에 대한 성능 카운터](sql-database-elastic-database-perf-counters.md)
### [성능 튜닝 팁](sql-database-troubleshoot-performance.md)
### 서비스 계층 및 성능 수준 변경
#### [Azure Portal](sql-database-scale-up.md)
#### [PowerShell](sql-database-scale-up-powershell.md)
### 메모리 내 OLTP
#### [메모리 내 OLTP 채택](sql-database-in-memory-oltp-migration.md)
#### [메모리 내 OLTP 저장소 모니터링](sql-database-in-memory-oltp-monitoring.md)
### 쿼리 저장소
#### [쿼리 저장소를 사용한 성능 모니터링](https://msdn.microsoft.com/library/dn817826.aspx)
#### [쿼리 저장소 사용 시나리오](https://msdn.microsoft.com/library/mt614796.aspx)
#### [쿼리 저장소 작동](sql-database-operate-query-store.md)
### 확장 이벤트
#### [확장 이벤트](sql-database-xevent-db-diff-from-svr.md)
#### [이벤트 파일 대상 코드](sql-database-xevent-code-event-file.md)
#### [링 버퍼 대상 코드](sql-database-xevent-code-ring-buffer.md)

## 데이터 이동
### [SQL 데이터베이스 복사](sql-database-copy.md)
#### [Azure 포털](sql-database-copy-portal.md)
#### [PowerShell](sql-database-copy-powershell.md)
#### [T-SQL](sql-database-copy-transact-sql.md)
### 데이터베이스를 BACPAC 파일로 내보내기
#### [Azure Portal](sql-database-export.md)
#### [SQL Server Management Studio](sql-database-cloud-migrate-compatible-export-bacpac-ssms.md)
#### [SQL 패키지 유틸리티](sql-database-cloud-migrate-compatible-export-bacpac-sqlpackage.md)
#### [PowerShell](sql-database-export-powershell.md)
### 데이터베이스를 BACPAC 파일에서 가져오기
#### [Azure Portal](sql-database-import.md)
#### [PowerShell](sql-database-import-powershell.md)
#### [SQL Server Management Studio](sql-database-cloud-migrate-compatible-import-bacpac-ssms.md)
#### [SQL 패키지 유틸리티](sql-database-cloud-migrate-compatible-import-bacpac-sqlpackage.md)
### [BCP를 사용하여 CSV 파일에서 로드](sql-database-load-from-csv-with-bcp.md)
### [확장된 클라우드 데이터베이스 간 데이터 이동](sql-database-elastic-scale-overview-split-and-merge.md)

## 쿼리
### [SQL Server Management Studio](sql-database-connect-query-ssms.md)
### [다중 분할된 데이터베이스 쿼리](sql-database-elastic-scale-multishard-querying.md)
### 데이터베이스 간 쿼리
#### [개요](sql-database-elastic-query-overview.md)
#### [서로 다른 스키마를 사용하여 크로스 데이터베이스 쿼리](sql-database-elastic-query-vertical-partitioning.md)
#### [크로스 데이터베이스 보고](sql-database-elastic-query-horizontal-partitioning.md)
#### [클라우드 데이터베이스의 분산 트랜잭션](sql-database-elastic-transactions-overview.md)

## 복원
### 삭제된 데이터베이스 복원
#### [Azure Portal](sql-database-restore-deleted-database-portal.md)
#### [PowerShell](sql-database-restore-deleted-database-powershell.md)
### 특정 시점 복원
#### [Azure Portal](sql-database-point-in-time-restore-portal.md)
#### [PowerShell](sql-database-point-in-time-restore-powershell.md)
### 지역 복원
#### [Azure Portal](sql-database-geo-restore-portal.md)
#### [PowerShell](sql-database-geo-restore-powershell.md)
#### [단일 테이블](sql-database-cloud-migrate-restore-single-table-azure-backup.md)
### [데이터 센터 가동 중단에서 복구](sql-database-disaster-recovery.md)
### [재해 복구 훈련 수행](sql-database-disaster-recovery-drills.md)

## 복제
### [활성 지역 복제 개요](sql-database-geo-replication-overview.md)
### 구성
#### [PowerShell](sql-database-geo-replication-powershell.md)
#### [T-SQL](sql-database-geo-replication-transact-sql.md)
### 장애 조치(Failover)
#### [Azure Portal](sql-database-geo-replication-failover-portal.md)
#### [PowerShell](sql-database-geo-replication-failover-powershell.md)
#### [T-SQL](sql-database-geo-replication-failover-transact-sql.md)

## 문제 해결
### [연결 문제](sql-database-troubleshoot-common-connection-issues.md)
### [일시적인 연결 오류](sql-database-troubleshoot-connection.md)
### [진단 및 방지](sql-database-connectivity-issues.md)
### [권한](sql-database-troubleshoot-permissions.md)
### [데이터베이스 이동](sql-database-troubleshoot-moving-data.md)

# 참조
## [PowerShell](/powershell/azureps-cmdlets-docs/)
## [PowerShell 클래식](/powershell/servicemanagement/)
## [Java](/java/api/)
## [.NET](/dotnet/api/)
## [T-SQL](https://msdn.microsoft.com/library/azure/bb510741.aspx)
## [Azure SQL Database Cmdlet](https://msdn.microsoft.com/library/azure/mt574084(v=azure.300\).aspx)
## [SQL Server Cmdlet](https://msdn.microsoft.com/library/mt740629.aspx)
## [REST (영문)](/rest/api/sql/)

## SQL Database 관리 라이브러리
### [SQL Database 관리 라이브러리 참조](https://msdn.microsoft.com/library/azure/mt349017.aspx)
### [SQL Database 관리 라이브러리 패키지 가져오기](https://www.nuget.org/packages/Microsoft.Azure.Management.Sql)
## [SQL Server 드라이버](https://msdn.microsoft.com/library/mt654049.aspx)
### [ADO.NET](https://msdn.microsoft.com/library/mt657768.aspx)
### [JDBC](https://msdn.microsoft.com/library/mt484311.aspx)
### [Node.JS](https://msdn.microsoft.com/library/mt652093.aspx)
### [ODBC](https://msdn.microsoft.com/library/mt654048.aspx)
### [PHP](https://msdn.microsoft.com/library/dn865013.aspx)
### [Python](https://msdn.microsoft.com/library/mt652092.aspx)
### [Ruby](https://msdn.microsoft.com/library/mt691981.aspx)

# 리소스
## [가격 책정](https://azure.microsoft.com/pricing/details/sql-database/)
## [서비스 업데이트](https://azure.microsoft.com/updates/?service=sql-database)
## [SQL Server 도구](https://msdn.microsoft.com/library/mt238365.aspx)
## [SSMS(SQL Server Management Studio)](https://msdn.microsoft.com/library/mt238290.aspx)
## [SSDT(SQL Server Data Tools)](https://msdn.microsoft.com/library/mt204009.aspx)
## [BCP](https://msdn.microsoft.com/library/ms162802.aspx)
## [SQLCMD](https://msdn.microsoft.com/library/ms162773.aspx)
## [SqlPackage](https://msdn.microsoft.com/hh550080.aspx)
## [포럼](https://social.msdn.microsoft.com/Forums/home?forum=ssdsgetstarted)
## [비디오](https://azure.microsoft.com/documentation/videos/index/?services=sql-database)


<!--HONumber=Nov16_HO2-->


