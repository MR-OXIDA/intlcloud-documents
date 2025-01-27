Tencent Cloud Cloud Object Storage(COS)의 글로벌 가속 기능은, Tencent의 전체 트래픽을 스케쥴링하는 CLB(Cloud Load Balancer) 시스템을 통해, 사용자의 요청을 스마트 라우팅 및 리졸브하여, 최적의 네트워크 액세스 링크를 선택하고, 요청에 따른 근접 액세스를 구현합니다. 전 세계에 분포한 클라우드 데이터 센터가 전 세계 각지의 사용자의 신속한 버킷 액세스를 구현하여, 액세스 성공률이 높을 뿐만 아니라, 안정적인 비즈니스 환경을 제공하고, 비즈니스 경험을 향상시킵니다. 또한 COS의 글로벌 가속 기능으로 더욱 신속하게 데이터를 업로드 및 다운로드할 수 있습니다.

> !
> - 현재 글로벌 가속 기능은 모든 퍼블릭 클라우드 리전에서 공급 및 지원됩니다.
> - 글로벌 가속은 현재 CI 기능을 지원하지 않습니다.
> - 글로벌 가속 기능을 사용하면, 정보 요청이 Tencent Cloud 내부 네트워크 전용 회선을 통해 가속 전송되기 때문에 요금이 부과됩니다. 자세한 요금 정보는 [제품 가격](https://intl.cloud.tencent.com/pricing/cos)을 참고하십시오.


## 사용 방법

COS 콘솔과 API 등 방식으로 글로벌 가속 기능을 활성화할 수 있습니다.

#### COS 콘솔 사용
COS 콘솔에서 버킷에 필요한 글로벌 가속 기능을 활성화할 수 있습니다. [글로벌 가속 활성화](https://intl.cloud.tencent.com/document/product/436/33406) 콘솔 문서를 참고하십시오.

#### REST API 사용
다음의 API를 통해 글로벌 가속 기능을 직접 활성화할 수 있습니다.

- [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)
- [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)

## 액세스 도메인

글로벌 가속 기능을 활성화한 뒤, 두 가지 도메인으로 COS 내 파일에 액세스할 수 있습니다.

- **버킷 기본 도메인: **형식은 `<BucketName-APPID>.cos.<Region>.myqcloud.com`이며, 자세한 내용은 [리전 및 액세스 도메인](https://intl.cloud.tencent.com/document/product/436/6224)을 참고하십시오.
- **글로벌 가속 도메인: **형식은 `<BucketName-APPID>.cos.accelerate.myqcloud.com`입니다.

예를 들어, 광저우 리전의 버킷 `examplebucket-1250000000`에 글로벌 가속 기능을 활성화한 경우, 베이징에서 해당 버킷으로 파일 `exampleObject.txt`를 업로드할 때 선택할 수 있는 두 가지 업로드 방식이 있습니다.

- **글로벌 가속 도메인으로 액세스**: 업로드할 때 도메인을 `exampleBucket-1250000000.cos.accelerate.myqcloud.com`으로 지정하면 해당 도메인을 통해 객체를 업로드할 경우, COS 서비스는 네트워크 상태에 따라 스마트 리졸브 및 근접 액세스를 실행합니다. 예를 들어, 베이징의 액세스 레이어로 요청을 전달하면, 내부 네트워크의 전용 회선을 거쳐 광저우 스토리지 레이어로 전송되는 과정이 가속으로 이뤄집니다.
- **버킷 기본 도메인으로 액세스**: 업로드 시 도메인을 `examplebucket-125000000.cos.ap-guangzhou.myqcloud.com`으로 지정합니다. 해당 도메인을 통해 객체를 업로드할 때, 요청이 광저우의 액세스 레이어로 바로 전달된 뒤, 다시 광저우 스토리지 레이어로 전송됩니다. 이때 외부 네트워크의 링크가 길기 때문에 전송이 불안정할 수 있습니다.

>! 글로벌 가속 기능은 별도의 요금이 부과되므로 실제 비즈니스 상황을 잘 고려하여 선택하시기 바랍니다.
> 1. 평소 읽기 작업보다 쓰기 작업을 많이 수행하고, 원격지에서 클라우드 데이터 센터로 데이터를 업로드(예: PUT Object, POST Object, Multipart Upload 작업)하는 경우, 글로벌 가속 도메인 사용을 권장합니다.
> 2. 평소 쓰기 작업보다 읽기 작업을 많이 수행하고, 주로 파일을 다운로드(예: GET Objcet 작업)하는 경우, 비용 최적화를 위해, [CDN 가속](https://intl.cloud.tencent.com/document/product/436/18668) 솔루션을 권장합니다.
> 3. 평소 설정이나 파일 인덱스 작업이 많다면, 버킷의 기본 도메인 사용을 권장합니다.
> 4. 동일 리전의 내부 네트워크 환경에서 동일 리전 내 버킷을 액세스하거나 전용 회선으로 액세스할 경우, 버킷의 기본 도메인 사용을 권장합니다.
> 

## 주의 사항

다음은 글로벌 가속 도메인 사용 시 주의사항입니다.

- 글로벌 가속 도메인을 활성화하고 약 15분 후에 적용되므로 잠시 기다려주십시오.
- 글로벌 가속 도메인을 활성화한 뒤 단일 버킷이 가속 도메인으로 액세스하는 최대 대역폭은 전체 네트워크 사용량에 따라 분배됩니다.
- 글로벌 가속 도메인을 활성화하면 가속 도메인에 의한 요청만 가속 효과가 적용되며, 버킷의 기본 도메인은 여전히 정상적으로 사용할 수 있습니다.
- 가속 도메인을 사용하는 경우, 요청 링크가 가속 링크일 때만 가속 요금이 부과됩니다. 예를 들어, 가속 도메인으로 베이징에서 베이징의 버킷으로 데이터를 업로드하면 링크에 대해 가속 기능이 작동하지 않아 요청 관련 요금이 발생하지 않습니다.
- 가속 도메인을 사용하는 경우, HTTP/HTTPS 전송 프로토콜을 지정하여 내부 네트워크의 전용 회선으로 정보 요청을 전송하면 COS에서 데이터 전송 보안을 위한 HTTPS 프로토콜의 채택 여부를 판단합니다.

## 과금 예시

글로벌 가속 도메인으로 데이터를 업로드하거나 버킷에 액세스하면 별도의 가속 요금이 부과되며, 가속 요금은 **일별** 결산됩니다. 관련 과금 항목 및 가격 정보는 [과금 개요](https://intl.cloud.tencent.com/document/product/436/16871)와 [제품 가격](https://intl.cloud.tencent.com/pricing/cos)을 참고하십시오. 다음은 가속 도메인과 버킷 기본 도메인을 사용했을 때의 요금 비교 내역입니다.

**비즈니스 시나리오 1**

주로 비디오 파일을 COS에 업로드하는 시나리오로, 전송 성공률에 대한 요구도가 높습니다. 광저우 리전에 설정된 버킷에 매일 신장과 싱가포르의 사무실로부터 각각 1GB의 비디오 데이터가 업로드됩니다. 이 경우, 30일 간의 요금을 계산하면 다음과 같습니다.

- **가속 도메인**으로 업로드 시 발생하는 업로드 요금: 30 x 1GB x (0.07USD/GB + 0.18USD/GB) = 7.5USD
- **버킷 기본 도메인**으로 업로드 시 발생하는 업로드 요금: 30 x 1GB x (0USD/GB) = 0USD

> ?중국 내의 업로드 가속 요금 단가는 0.07USD/GB이며, 중국 외 지역의 업로드 가속 요금은 0.18USD/GB입니다. 버킷 기본 도메인으로 파일 업로드 시 업로드 트래픽 요금이 발생하지 않습니다.

**비즈니스 시나리오 2**

해외 파일 다운로드 가속 시나리오로, 전송 성공률에 대한 요구도가 높습니다. 버킷은 광저우 리전에 설정되어있으며, 매일 싱가포르 사무실로부터 1GB의 비디오 데이터를 다운로드합니다. 이 경우, 30일 간의 요금을 계산하면 다음과 같습니다.

- 가속 도메인으로 다운로드 시 발생하는 다운로드 가속 트래픽 요금 :30 x 1GB x 0.18USD/GB = 5.4USD
- 가속 도메인으로 다운로드 시 발생하는 공인 네트워크 다운스트림 트래픽 요금:30 x 1GB x 0.1USD/GB = 3USD

총 다운로드 트래픽 요금은 5.4 + 3 = 8.4USD입니다.

>? 해외 다운로드 가속 요금 단가는 0.18USD/GB입니다. 글로벌 가속 도메인으로 파일 다운로드 시 **외부 네트워크 다운스트림 트래픽 비용**과 **글로벌 가속 다운스트림 트래픽 비용**이 청구됩니다.
>



