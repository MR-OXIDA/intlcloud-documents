## 기능 소개
MySQL 데이터의 SQL 실행 단계는 주로 분석, 준비, 최적화 및 실행의 4단계로 구성됩니다. 실행 플랜 캐싱 기능은 prepare statement 모드에서 작동합니다. prepare statement 모드는 execute 중 구문 분석 및 준비의 두 단계를 생략합니다. 실행 플랜은 성능을 더욱 향상시키기 위해 최적화 단계도 생략합니다.

MySQL 8.0 20210830 버전은 (UK&PK) 점검에 대해서만 작동됩니다. 이후 버전은 더 많은 기능이 제공될 예정입니다.

## 지원 버전
커널 버전 MySQL 8.0 20210830 이상

## 적용 시나리오
클라우드 상의 단기 쿼리가 많으며, prepare statement 모드를 사용하면 애플리케이션 성능이 향상됩니다. 구체적인 성능 향상 정도는 서비스 마다 다릅니다.

## 성능 영향
- (UK&PK) 점검 SQL의 경우 딜레이 성능이 20%-30% 증가하고 처리량 성능이 20%-30% 증가합니다(sysbench의 point_select.lua 테스트).
- 메모리 오버헤드 관련, 플랜 캐시를 활성화하면 메모리 사용량이 향상됩니다.

## 사용 설명
새로 추가된 cdb_plan_cache 스위치는 플랜 캐시 활성화 여부를 제어하고, 새로 추가된 cdb_plan_cache_stats 스위치는 관찰 캐시 히트 상태를 제어합니다. 상기 매개변수는 tencentroot 수준입니다.

| 매개변수 이름         | 상태 | 유형 | 기본값  | 매개변수 값 범위 | 설명                              |
| -------------- | ---- | ---- | ----- | ---------- | --------------------------------- |
| cdb_plan_cache | yes  | bool | false | true/false | tencentroot 스위치, 플랜 캐시 활성화 여부 |

플랜 캐시 히트 상태를 볼 수 있는 `show cdb_plan_cache` 명령이 추가되었습니다. 필드 의미는 다음과 같습니다.

| 필드 이름 | 설명                                                         |
| ------ | ------------------------------------------------------------ |
| sql    | SQL 명령. ?가 있는 SQL 명령입니다. 이는 이 SQL의 실행 플랜이 캐시되었음을 의미합니다. |
| mode   | SQL 캐시 모드. 현재 prepare 모드만 지원됩니다.                           |
| hit    | 이 THD의 히트 횟수                                            |

cdb_plan_cache_stats가 활성화된 경우, 정보 기록에 해당하며 성능에 영향을 미칩니다.

## 관련 상태 설명
show profile을 통해 SQL 실행의 각 단계의 상태를 조회할 때, SQL 히트 플랜 캐시를 실행하면 optimizing, statistics, preparing 상태가 생략됩니다.

