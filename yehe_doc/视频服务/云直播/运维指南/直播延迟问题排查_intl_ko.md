일반적으로 RTMP 프로토콜 푸시 스트리밍을 사용하여 FLV 프로토콜로 재생할 경우 2~3초의 딜레이가 발생합니다. 딜레이 시간이 너무 긴 것은 정상적인 상황이 아닙니다. 라이브 방송 딜레이 시간이 너무 긴 경우 다음 절차에 따라 문제를 해결하시기 바랍니다.

### 1단계: 재생 프로토콜 확인

재생 프로토콜로 HLS(m3u8) 프로토콜을 사용할 경우 딜레이가 너무 길다고 느껴지는 것은 정상적인 현상입니다. HLS 프로토콜은 Apple이 출시한 대단위 TS 멀티 파트 기반 스트림 미디어 프로토콜입니다. 멀티 파트별 딜레이 시간은 일반적으로 5초 이상이며 멀티 파트 수는 보통 3~4개이므로, 총 딜레이 시간은 10~30초 정도입니다.

반드시 HLS(m3u8) 프로토콜을 사용해야 할 경우, 딜레이를 단축하기 위해서는 멀티 파트 수를 적절하게 줄이거나 멀티 파트별 시간을 줄이는 방법밖에 없습니다. 그러나 랙 지표에 미칠 수 있는 영향에 대해 종합적인 고려가 필요한 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category) 또는 Tencent Cloud 기술 지원 엔지니어에게 문의하여 조정할 수 있습니다.

### 2단계: 플레이어 설정 확인

Tencent Cloud MLVB SDK의 플레이어는 고속, 원활, 자동의 3가지 모드를 지원합니다. 설정에 대한 자세한 내용은 [딜레이 조절](https://intl.cloud.tencent.com/document/product/1071/38160)을 참조하십시오.

- **고속 모드:** 대다수 시나리오의 딜레이를 2~3초 이내로 보장합니다. 뷰티쇼 시나리오에 적합합니다.
- **원활 모드:** 대다수 시나리오의 딜레이가 5초 이내입니다. 딜레이에 민감하지 않지만 끊김 없는 화면이 중요한 게임 라이브 방송과 같은 시나리오에 적합합니다.

### 3단계: 최대한 클라이언트에서 워터마크 삽입
Tencent Cloud CSS는 클라우드에서의 워터마크 삽입을 지원합니다. 그러나 워터마크 삽입 시 1~2초 정도 추가적인 딜레이가 발생하므로, Tencent Cloud MLVB SDK를 사용하는 경우 직접 호스트의 App에서 워터마크를 삽입하도록 선택할 수 있습니다. 클라우드에서 삽입할 필요가 없기 때문에 워터마크 삽입으로 인한 딜레이가 감소합니다.

### 4단계: 3rd party 푸시 스트리밍 플레이어 사용
Tencent Cloud 통합 솔루션을 사용할 경우에만 이상적인 효과를 얻을 수 있습니다. 3rd party 푸시 스트리밍 소프트웨어를 사용하는 경우 Tencent Cloud MLVB SDK의 [푸시 스트리밍 Demo](https://intl.cloud.tencent.com/document/product/1071/38147)와 비교한 후, 3rd party 푸시 스트리밍 플레이어의 인코딩 캐시로 인해 긴 딜레이가 발생할 가능성을 제거하는 것을 권장합니다. 많은 3rd party 푸시 스트리밍 재생기에서 강제로 무한 버퍼 방식을 사용하여 업스트림 대역폭 부족 문제를 해결하기 때문입니다.

### 5단계: OBS 설정 확인
OBS 푸시 스트리밍 사용 시 재생 딜레이가 비교적 긴 경우, [OBS 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31569)의 설명에 따라 해당 매개변수를 설정하고, 키 프레임 간격을 1초 또는 2초로 설정합니다.

### 6단계: LEB 액세스
위와 같은 조치에도 딜레이에 대한 요구사항이 충족되지 않는 경우 Tencent Cloud LEB에 액세스할 수 있습니다. LEB는 LVB 대비 딜레이가 훨씬 낮고 밀리초 단위의 고성능 라이브 방송 시청 경험을 제공합니다. 자세한 내용은 [LEB](https://intl.cloud.tencent.com/document/product/267/41030) 문서 소개를 참조하십시오.
