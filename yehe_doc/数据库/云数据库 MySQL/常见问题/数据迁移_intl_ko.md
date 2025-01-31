
### 로컬에 있는 SQL 파일을 어떻게 MySQL 데이터베이스에 가져오나요?
>?TencentDB for MySQL 2노드와 3노드 인스턴스만 SQL 파일 가져오기 기능을 지원합니다.
>
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb) 로그인 후 인스턴스 ID를 클릭하여 관리 페이지로 이동합니다.
2. **데이터베이스 관리** > **데이터베이스 목록** > **데이터 가져오기**를 선택합니다. 가져올 파일과 대상 데이터베이스를 선택하고 확인을 클릭하여 데이터를 가져옵니다.
>?
>- 시스템 테이블 손상으로 데이터베이스를 가져올 수 없는 상황을 방지하기 위해, 시스템 테이블의 데이터를 가져오지 마십시오(예: mysql.user 테이블). 
>- 증분 데이터 가져오기만 지원합니다. 데이터베이스 내 폐기된 데이터가 있는 경우, 데이터를 삭제한 후 가져오기를 실행하십시오.
>- 단일 파일은 10GB를 초과할 수 없으며 파일 이름에는 영어, 숫자, 언더바만 사용할 수 있습니다.
>
![](https://main.qcloudimg.com/raw/a8854e74caebb9c69d831dc1583c10c0.png)
자세한 내용은 [SQL 파일 가져오기](https://intl.cloud.tencent.com/document/product/236/8466)를 참고하십시오.

### 데이터베이스 데이터는 어떻게 내보내나요?
- 백업 데이터를 내보내기하려면 [콘솔](https://console.cloud.tencent.com/cdb)에서 인스턴스 ID를 클릭해 관리 탭으로 이동한 후, **백업 복구** 탭을 선택해 다운로드하십시오.
- 실시간 데이터 내보내기가 필요한 경우, [읽기 전용 인스턴스](https://intl.cloud.tencent.com/document/product/236/7270)를 구매하여 인스턴스를 연결한 후 mysqldump 툴을 사용해 실시간 데이터를 획득할 수 있습니다.

### 기존 데이터베이스가 대략 7GB 정도인 경우 가장 빠르게 TencentDB for MySQL에 마이그레이션하는 방법은 무엇인가요?
[데이터 마이그레이션](https://intl.cloud.tencent.com/zh/document/product/571/34103) 기능을 사용하여, 마이그레이션할 데이터베이스를 연결하고 데이터 동기화할 것을 권장합니다. 

### 동일 지역 내 이중 백업을 위해 2개의 인스턴스를 실시간으로 데이터 동기화할 수 있습니까?
콘솔에서 [재해 복구 인스턴스](https://intl.cloud.tencent.com/document/product/236/7272)를 구매하여 구현 가능합니다.

