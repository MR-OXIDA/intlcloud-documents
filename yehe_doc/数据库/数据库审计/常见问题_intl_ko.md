
### 감사는 어떻게 비용을 책정하나요?
- 데이터베이스 감사 (금융 리전 제외)는 감사 로그 저장 용량에 따라 과금하며 단가는 0.00220588USD/GB/시간입니다.
- 과금 단위는 1시간이며 1시간 이하는 모두 1시간으로 과금합니다. 
금융 리전의 TencentDB for MySQL 감사 정책 추가 기능은 일시 중지되지만 기존 정책은 계속 사용할 수 있습니다. 금융 리전 감사 정책 기능은 최적화 작업 이후, 상용화 과금 방식이 적용될 예정이며, 구체적인 적용 시간은 콘솔 공지나 팝업 정보를 참고해 주시기 바랍니다.

### 활성화된 감사 기능은 어떻게 비활성화 하나요?
[콘솔](https://console.cloud.tencent.com/dls/mysql/policy)에 로그인하고, 감사 정책 페이지에서 [서비스 설정] 클릭 후, [서비스 비활성화] 선택하시면 됩니다. 
서비스 비활성화 후, 해당 인스턴스에 적용되던 감사 정책, 로그, 파일은 삭제되며 복구가 불가능합니다. 로그와 파일을 미리 저장하시기 바랍니다. 

### 감사 데이터는 얼마 동안 보관할 수 있나요?
감사 데이터는 30일~5년까지 보관할 수 있습니다. [콘솔] (https://console.cloud.tencent.com/dls/mysql/policy)에서 감사 기능을 활성화할 때, 보관 기간을 설정할 수 있으며 활성화 후에는 감사 정책 페이지에서 [서비스 설정]을 클릭하여 수정할 수 있습니다 
