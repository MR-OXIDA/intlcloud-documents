종량제(후불) 방식은 Cloud Object Storage(COS)의 기본 과금 방식으로 [모든 리전](https://intl.cloud.tencent.com/document/product/436/6224)에서 지원됩니다. 사용자의 스토리지 용량, 요청, 트래픽 등 과금 항목에 따라 과금하며 사용자 계정에서 매일 또는 매월 차감됩됩니다.


## 제품 가격

COS의 종량제 과금 방식에 대한 내용은 [제품 가격](https://intl.cloud.tencent.com/pricing/cos)을 참고하십시오.

## 과금 항목

COS의 다양한 과금 항목과 계산법은 다음과 같습니다.
<table>
   <tr>
      <th>과금 항목</th>
      <th>과금 항목 설명</th>
      <th>과금 계산법</th>
   </tr>
   <tr>
      <td nowrap="nowrap">스토리지 용량 요금</td>
      <td>스토리지 용량에 따라 계산하며, 스토리지 유형별로 상이한 단가가 적용됩니다.</td>
      <td nowrap="nowrap"><li>스토리지 용량 요금 = 스토리지 용량 단가 * 월별 스토리지 용량<br><li>월별 스토리지 용량 = 당월 ‘일일 스토리지 용량’ 합계 / 당월 일수<br><li>일일 스토리지 용량 = 당일 ‘5분당 스토리지 용량’ 합계 / 288(샘플 카운팅)</td>
   </tr>
   <tr>
      <td>요청 요금</td>
      <td>요청 요금은 요청 횟수에 따라 계산하며, 스토리지 유형별로 상이한 요청 단가가 적용됩니다.</td>
      <td nowrap="nowrap">요청 요금 = 요청 1만 회당 단가 * 월 누적 요청 횟수 / 10000</td>
   </tr>
   <tr>
      <td>데이터 검색 요금</td>
      <td>데이터 검색량에 따라 계산하며, 표준IA 스토리지 및 CAS 유형의 다운로드 시 해당 항목이 과금되고, 스토리지 유형별로 상이한 검색 단가가 적용됩니다.</td>
      <td nowrap="nowrap">데이터 검색 과금 = 각 GB 단가 * 월 데이터 검색량</td>
   </tr>
   <tr>
      <td>트래픽 요금</td>
      <td>외부 네트워크 다운스트림 트래픽, CDN Origin-pull 트래픽, 리전 간 복제 트래픽, 글로벌 가속 트래픽을 포함하며, 트래픽 유형별로 상이한 요금이 적용됩니다.</td>
      <td nowrap="nowrap">트래픽 과금 = 각 GB 단가 * 일일 누적 트래픽</td>
   </tr>
   <tr>
      <td rowspan=4>관리 기능 요금</td>
      <td rowspan=4>관리 기능 요금은 사용자가 관리 기능(인벤토리, 인덱스, 배치 프로세스, 객체 태그 등 기능 등)을 활성화하여 사용시 발생하는 비용입니다. 현재 해당 비용은 인벤토리 기능, 인덱스 기능, 배치 프로세스, 객체 태그에 부과됩니다.
      <td nowrap="nowrap">리스트 기능 요금 = 나열된 객체 수/1백만 x 단가</td>
   </tr>
   <tr>
      <td nowrap="nowrap">인덱스 기능 요금 = GB당 단가 x 일 누적 데이터 인덱스 수</td>
   </tr>
   <tr>
			<td nowrap="nowrap">배치 프로세스 요금에는 작업 과금과 객체 처리 요금이 포함됩니다.<br><li>작업 요금 = 생성한 작업 수 * 단가<br><li>객체 처리 요금 = 처리 객체 개수/1만 * 단가</td>
   </tr>
   <tr>
			<td nowrap="nowrap">객체 태그 요금 = 태그 수/1만 * 단가</td>
   </tr>
</table>


> ?과금 항목에 관한 자세한 내용 및 과금 유의 사항은 [과금 항목](https://intl.cloud.tencent.com/zh/document/product/436/33776)문서를 참고하십시오.


## 과금 주기

COS 과금 항목은 월별 과금과 일별 과금 2 종류가 있으며 과금 항목별로 과금 주기가 다릅니다. 자세한 내용은 다음과 같습니다. 

| 과금 항목       | 과금 주기 | 설명                                   |
| ------------ | -------- | -------------------------------------- |
| 스토리지 용량 요금 | 월별 과금 | 매월 1일에 전월에 발생한 요금을 결산합니다.        |
| 요청 요금     | 월별 과금 | 매월 1일에 전월에 발생한 요금을 결산합니다.         |
| 데이터 검색 요금 | 월별 과금 | 매월 1일에 전월에 발생한 요금을 결산합니다.         |
| 트래픽 요금     | 일별 과금 | 매일 전일 00:00 - 23:59:59 동안 발생한 요금을 결산합니다. |
| 관리 기능 요금 | 일별 과금 | 매일 전일 00:00 - 23:59:59 동안 발생한 요금을 결산합니다. |

>?
> 청구서 시스템에 일정 딜레이가 발생할 수 있습니다. 매일 또는 매월 청구서는 당일 8:00 경에 생성됩니다.


## 예시 설명

고객 A는 2019년 3월 1일 COS에서 표준 스토리지 파일 100G를 업로드하고, 3월 15일 외부 네트워크로 데이터 10G를 다운로드했으며, 다른 날에는 추가 사용 내역이 없습니다. 이 경우 고객의 3월 과금 내역은 다음과 같습니다.

- 표준 스토리지 용량 요금: 해당 월의 스토리지 용량은 총 100G로 과금.
- 트래픽 요금: 해당 월의 외부 네트워크 다운스트림 트래픽은 총 10G로 과금.
- 요청 요금: 해당 월 데이터의 업로드 및 다운로드시 발생한 요청 수를 계산해 과금.

