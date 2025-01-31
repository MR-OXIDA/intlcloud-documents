![](https://main.qcloudimg.com/raw/db29f65a777b1e445b5c9c7e0e694457.png)
재생 시 랙을 발생시키는 주된 요인은 다음과 같이 세 가지가 있습니다.

- **원인1: 너무 낮은 푸시 스트리밍 프레임 레이트**
호스트의 휴대폰 성능이 떨어지거나 CPU 점유율이 높은 백그라운드 프로그램이 실행중인 경우, 비디오 프레임 레이트가 크게 저하될 수 있습니다. 일반적으로 비디오 스트리밍의 FPS가 15프레임/초 이상이어야 원활한 시청이 가능합니다. FPS가 10프레임 이하일 경우, **너무 낮은 프레임 레이트**라고 볼 수 있으며 **모든 시청자**에게 랙이 발생하게 됩니다. 단, 호스트의 화면 자체가 거의 변화가 없거나, 정적인 화면 또는 PPT 재생 등의 시나리오인 경우에는 프레임 레이트의 영향을 받지 않습니다.
- **원인 2: 업로드 정체**
호스트의 휴대폰은 푸시 스트리밍 시 계속해서 멀티미디어 데이터를 생성합니다. 하지만 휴대폰의 네트워크 업로드 속도가 너무 느릴 경우에는 생성된 멀티미디어 데이터가 호스트의 휴대폰에 쌓여 업로드되지 않으며, 업로드 정체가 발생해 **모든 시청자**에게 랙이 발생하게 됩니다.

 **중국 내 ISP**가 제공하는 광대역 인터넷 패키지의 다운로드 속도는 이미 10Mbps, 20Mbps을 넘어 100Mbps, 200Mbps까지 도달했습니다. 하지만 업로드 속도는 비교적 낮게 제한되어 있어 많은 소도시들의 경우 업스트림 속도가 최대 512Kbps에 불과합니다(초당 최대 64KB 데이터 업로드 가능).
 **Wi-Fi 접속**은 IEEE 802.11에 규정된 반송파 감지 다중 접속/충돌 예방(CSMA/CA) 표준을 따릅니다. 즉, 하나의 Wi-Fi 핫스팟은 동시에 오직 하나의 휴대폰과 통신할 수 있으며, 다른 휴대폰이 핫스팟과 통신하려면 먼저 통신이 가능할지 탐지하거나 문의해야 합니다. 따라서 하나의 Wi-Fi 핫스팟을 사용하는 사람이 많아질수록 속도는 느려집니다. 동시에 Wi-Fi 신호는 건축물의 벽면에 막히고 간섭을 받습니다. 그러나 중국의 일반 가정에서 공사를 할 때 각 방에서 Wi-Fi 신호가 약해지는 문제를 고려하는 경우가 매우 드물고, 호스트 본인도 자신이 라이브 방송을 하는 방이 공유기로부터 몇 개의 벽 너머에 있는지 알 수 없습니다.
- **원인 3: 다운스트림 문제**
시청자의 다운로드 대역폭이 충분하지 못하거나 네트워크 변동이 큰 경우입니다. 예를 들어 라이브 방송 스트림의 비트 레이트가 2Mbps일 때 초당 2M 비트의 데이터 스트림이 다운로드되는데 시청자의 대역폭이 부족할 경우에는 재생 시 랙이 발생할 수 있습니다. 다운스트림 문제는 현재 네트워크에 있는 시청자에게만 영향을 미칩니다.

[](id:deal0)
## SDK 상태 알림 정보 조회
푸시 스트리밍 시, Tencent Cloud MLVB SDK는 상태 피드백 메커니즘을 제공하여 2초 마다 내부의 각 종 상태의 매개변수를 피드백합니다. [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html)리스너를 등록한 후，onStatisticsUpdate 함수를 콜백하면 관련 상태 정보를 볼 수 있습니다. V2TXLivePusherStatistics 관련 상태 설명은 다음과 같습니다. 

|  푸시 스트리밍 상태                   |  의미 설명                    |
| :------------------------  |  :------------------------ |
|   appCpu     |현재 App의 CPU 사용률(％)|
|systemCpu     | 현재 시스템의 CPU 사용률(％)|
|width     | 비디오 폭 |
|height | 비디오 높이 |
|fps | 프레임 레이트 (fps) |
|audioBitrate    | 오디오 비트 레이트(Kbps) |
|videoBitrate  |비디오 비트 레이트(Kbps) |

[](id:deal1)
## 너무 낮은 프레임 레이트 문제 해결
### 1. 너무 낮은 프레임 레이트인지 판단
MLVB SDK V2TXLivePusherObserver의 [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be)콜백 중의 **V2TXLivePusherStatistics.fps** 상태 데이터를 통해 현재 푸시 스트리밍의 비디오 프레임 레이트를 확인할 수 있습니다. 일반적으로 초당 15프레임 이상이어야 원활한 시청이 가능하며 FPS가 10프레임 이하일 경우 시청 시 랙을 확연히 느낄 수 있습니다. 

### 2. 맞춤형 최적화 솔루션
- **2.1 appCpu 및 systemCpu 크기 모니터링**
MLVB SDK V2TXLivePusherObserver의  [onStatisticsUpdate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#af01be7a0bf0ed619cce63f49959ea8be) 콜백 중의 **V2TXLivePusherStatistics.appCpu** 와 **V2TXLivePusherStatistics.systemCpu** 상태 데이터를 통해**현재 푸시 스트리밍 SDK의 CPU 점유 상황**과**현재 시스템의 CPU 점유 상황**을 알 수 있습니다. 현재 시스템의 전체 CPU 사용률이 80%를 초과하면 비디오의 수집과 인코딩 모두 영향을 받으며 정상 작용이 불가능합니다. CPU 사용률이 100%에 도달하면 호스트부터 랙이 걸리기 때문에 원활한 시청을 할 수 없습니다.

- **2.2 CPU 사용자 확인**
라이브 방송 App에서 푸시 스트리밍 SDK뿐만 아니라 댓글 자막, 움직이는 아이콘, 텍스트 메시지 등도 불가피하게 CPU를 소모할 수 있습니다. 푸시 스트리밍 SDK의 CPU 점유 상황만을 테스트하려면 [툴 패키지 DEMO](https://intl.cloud.tencent.com/document/product/1071/38147)를 사용해 모니터링하고 평가하십시오.

- **2.3 과도한 고해상도 설정 지양**
해상도가 높을수록 반드시 화질이 선명한 것은 아닙니다. 해상도가 높으면 비트 레이트도 높아야 합니다.  비트 레이트가 낮은데 해상도만 높으면 높은 비트 레이트에 해상도를 낮게 설정할 때보다 화질이 떨어질 수 있습니다. 또한 평균 5인치 정도의 휴대폰 화면에서는 1280 x 720와 960 x 540의 해상도 차이를 느끼기 어려우며 PC에서 풀 스크린으로 시청해야만 명확한 차이를 느낄 수 있습니다. 해상도를 높게 설정하면 SDK의 CPU 사용률이 눈에 띄게 증가하기 때문에 일반적인 상황에서는 MLVB SDK에서 V2TXLivePusher의 [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02)를 **고화질**로 설정할 것을 권장합니다. 과도하게 높은 해상도를 설정하면 원하는 효과를 낼 수 없습니다.

[](id:deal2)
## 업로드 정체 문제 해결
통계에 따르면 비디오 클라우드 고객의 라이브 룸 랙 문제의 80% 이상은 호스트의 업로드 정체로 인한 것입니다.

### 1. 호스트에게 자동 알림
해상도가 중요한 시나리오에서는 적합한 UI 인터랙티브를 통해 호스트에게 **“네트워크 상태가 좋지 않습니다. Wi-Fi 벽 통과로 인한 수신율 감도가 저하될 수 있으니 공유기에 가까이 가십시오.”**와 같은 알림을 표시해 주는 것이 가장 좋습니다.
MLVB SDK의 푸시 스트리밍 기능 문서의**이벤트 처리**에 관한 소개를 참고하여 실행할 수 있습니다. App이 단시간 내에 연속으로 MLVB SDK의 여러 [V2TXLIVE_WARNING_NETWORK_BUSY](https://cloud.tencent.com/document/product/454/17246#.E8.AD.A6.E5.91.8A.E4.BA.8B.E4.BB.B6)이벤트를 받을 경우 호스트에게 현재 네트워크 상태를 확인하라고 알려주는 방법을 권장합니다. 호스트 본인은 비디오를 통해 업스트림 정체 상황을 감지할 수 없기 때문에 시청자나 App의 알림을 통해 상황을 알 수 밖에 없습니다.

### 2. 적합한 인코딩 설정 
권장하는 인코딩 설정은 다음과 같습니다(자세한 내용은 [화면 품질 설정](https://intl.cloud.tencent.com/document/product/1071/41861) 참고). V2TXLivePusher 내의 [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02)인터페이스에서 설정할 수 있습니다. 

|응용 시나리오 |resolution |resolutionMode |
| :------------------------  |  :------------------------ | :------------------------ |
|쇼 라이브 방송 |<li/>V2TXLiveVideoResolution960x540<li/>V2TXLiveVideoResolution1280x720 |가로 모드 또는 세로 모드 |
|모바일 게임 라이브 방송 |V2TXLiveVideoResolution1280x720 |가로 모드 또는 세로 모드 |
|마이크 연결(메인 화면) |V2TXLiveVideoResolution640x360 |가로 모드 또는 세로 모드 |
|마이크 연결(소형 화면) |V2TXLiveVideoResolution480x360 |가로 모드 또는 세로 모드 |
|블루레이 라이브 방송 |V2TXLiveVideoResolution1920x1080 |가로 모드 또는 세로 모드 |

[](id:deal3)
## 플레이어 최적화
![](https://main.qcloudimg.com/raw/c2c88d9bbf8f72c77eb778d7f2d5e993.png)

### 1. 랙과 딜레이
위 이미지와 같이 다운스트림 네트워크에 변동이 있거나 다운스트림 대역폭의 연결이 끊길 경우 재생 중 **데이터 공백기**(이 기간 동안 App은 재생할 수 있는 멀티미디어 데이터를 획득할 수 없음)가 발생합니다. 시청자의 비디오 랙을 최소화하기 위해서는 App이 충분한 비디오 데이터를 캐싱해 이 '공백기'를 무사히 넘겨야 합니다. 하지만 App 캐시가 너무 많은 멀티미디어 데이터는 **긴 딜레이**라는 새로운 문제를 만듭니다. 이는 인터랙션에 대한 요구치가 높은 시나리오에는 최악의 상황으로, 딜레이를 수정하고 컨트롤하지 않으면 랙으로 인한 딜레이로 재생 시간이 길수록 딜레이 시간이 길어지는 **누적 효과**가 발생합니다. 이 때, 딜레이 수정이 잘 되었는지 여부는 플레이어의 성능을 판단하는 주요 지표입니다. 그렇기 때문에 **딜레이와 원활한 재생의 균형**을 잘 잡아야 합니다. 저지연성에 너무 치중하면 미약한 네트워크 변동에도 재생 시 뚜렷한 랙이 발생할 수 있습니다. 반대로 원활한 재생에 너무 치중하면 긴 딜레이가 발생할 수 있습니다. (전형적인 사례: HLS(m3u8)가 20~30초의 딜레이로 원활한 재생을 구현)

### 2. 맞춤형 최적화 솔루션
Tencent Cloud MLVB SDK는 사용자가 트래픽 제어 프로세스에 관한 많은 지식 없이도 재생을 최적화할 수 있도록 여러 버전을 개선해 자동 조절 기술을 최적화했으며,이를 바탕으로 세 가지[딜레이 제어 솔루션](https://intl.cloud.tencent.com/document/product/1071/38160)을 출시했습니다. V2TXLivePlayer 의 [setCacheParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePlayer__android.html#a8a4f8f8e220a6e4aa2a04ca3e866efcb)를 통해 설정할 수 있습니다. 

-  **자동 모드**: 주요 시나리오에 대해 잘 모를 경우 이 모드를 선택하십시오.
>? 해당 모드에서 플레이어는 현재 네트워크 상황에 따라 딜레이를 자동으로 조절하여(기본적으로 1s~5s 구간 내에서 자동으로 딜레이 길이를 조절하며, setCacheParams에서 기본값 수정 가능), 원활한 상황에서 시청자와 호스트의 딜레이를 최소화하여 양질의 인터랙션을 선사합니다.

-  **고속 모드**: 주로 **쇼 라이브 방송** 등 양방향성이 높고 짧은 딜레이가 요구되는 시나리오에 적합합니다.
>? 고속 모드 설정 방법은 **minTime = maxTime = 1s**이며, 자동 모드와 고속 모드의 차이는 maxTime에 있습니다(고속 모드는 maxTime이 낮은 반면 자동 모드는 maxTime 비교적 높음). SDK 내부의 자동 조절 기술을 통해 효율성을 높인 것으로, 랙이 걸리지 않은 상황에서 자동으로 딜레이 길이를 수정할 수 있는데 maxTime은 바로 이 조절 속도에 반응합니다. 즉 maxTime 값이 클수록，조절 속도는 느려지며, 랙이 걸릴 확률도 낮아지는 것입니다. 

-  **원활 모드**: **게임 라이브 방송** 등 비트 레이트가 높은 고화질 시나리오에 주로 사용됩니다.
>?
>- 해당 모드에서 플레이어의 프로세스 정책은 Adobe Flash 커널의 캐시 정책과 유사합니다. 비디오에 랙이 발생하면 버퍼가 가득 찰 때까지 loading 상태에 진입하며, 이후 방어할 수 없는 네트워크 변동이 발생할 때까지 playing 상태를 유지합니다. 기본적으로 버퍼 시간은 5초이며, setCacheParams에서 수정할 수 있습니다.
>- 딜레이에 대한 요구가 높지 않은 시나리오에서는 이와 같이 약간의 딜레이를 허용함으로써 랙 발생 확률을 줄이는 단순한 모드가 더 안정적입니다.
