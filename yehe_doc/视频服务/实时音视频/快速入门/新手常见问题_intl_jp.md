
<h3 id="UserSig">UserSigとは。</h3>

UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計されたセキュリティ保護された署名です。
現在、TRTC、IMおよびMLVBなどのサービスには、すべてこの一連のセキュリティ保護メカニズムが採用されています。これらのサービスを使用する場合、対応するSDKの初期化またはログイン関数において、SDKAppID、UserIDおよびUserSigという3つの重要情報を提供する必要があります。
このうちSDKAppIDはお客様のアプリケーションの識別に、UserIDはユーザーの識別に使用されます。UserSigは、** HMAC SHA256 **暗号化アルゴリズムによって算出される最初の2つをもとに計算されたセキュリティ署名です。攻撃者がUserSigを偽造できない限り、クラウドサービスのトラフィックを盗用することはできません。
UserSigの計算原理を次の図に示します。SDKAppID、UserID、ExpireTimeなどの重要情報をハッシュ化・暗号化することがUserSigの本質です。
```Cpp
//UserSigの計算式。このうちsecretkeyは、usersigを算出するための暗号化鍵です。

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```


[](id:que2)
### TRTCではルームを同時にいくつ作成できますか。
4,294,967,294室のルームの同時併存をサポートします。ルームの累計数は無制限です。


[](id:que3)
### TRTCの遅延はどのくらいですか。
グローバルなエンドツーエンドの平均遅延は300ms未満です。


[](id:que4)
### TRTCはPCでの画面共有をサポートしていますか。
サポートしています。次のドキュメントをご参照ください。
- [画面共有(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [画面共有(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [画面共有(Web)](https://intl.cloud.tencent.com/document/product/647/37336)

画面共有インターフェースの詳細は[Windows（C++）API](https://intl.cloud.tencent.com/document/product/647/35131)またはWindows（C#）APIをご参照ください。そのほか、[Electronインターフェース](https://intl.cloud.tencent.com/document/product/647/35141)もお使いいただけます。


[](id:que5)
### TRTCはどのプラットフォームをサポートしますか。
サポートしているプラットフォームは、iOS、Android、Windows(C++)、Windows(C#)、Mac、Web、Electronです。詳細については、[プラットフォームのサポート](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

[](id:que6)

### TRTCは最大何人の同時通話をサポートできますか。
- 通話モードでは、1ルームあたり最大300人の同時接続、最大50人のカメラまたはマイクの同時使用をサポートしています。
- ライブストリーミングモードでは、1ルームあたり視聴者10万人のオンライン視聴と、キャスター50人のカメラまたはマイクの使用をサポートしています。


[](id:que7)
###  TRTCはライブストリーミングのシーン類のアプリケーションをどのように実現しますか。
TRTCは、特にオンラインライブストリーミングのシーン向けに、10万人向けの低遅延ライブストリーミングソリューションをリリースしました。これにより、キャスターとマイク接続したキャスター間の最小遅延が200ms、通常の視聴者の遅延が1秒以内になるだけでなく、脆弱なネットワークに極めて高い耐性を持つこととなり、モバイル端末の複雑なネットワーク環境に対応します。
具体的な操作ガイドについては、[ライブストリーミングクイックスタート](https://intl.cloud.tencent.com/document/product/647/35107)をご参照ください。



[](id:que8)
### TRTCライブストリーミングはどのようなロールをサポートしていますか。ロールの違いは何ですか。
ライブストリーミングのシーン（TRTCAppSceneLIVEとTRTCAppSceneVoiceChatRoom）は、TRTCRoleAnchor（キャスター）とTRTCRoleAudience（視聴者）という2つのロールをサポートしています。違いとしては、キャスターのロールはオーディオ・ビデオデータのアップロードとダウンロードを同時に行うことができますが、視聴者のロールは他人のデータのダウンロードと再生のみをサポートしていることです。switchRole()を呼び出すことにより、ロールを切り替えることができます。


[](id:que9)
### TRTCルームは、キックアウト、発言の禁止、ミュートをサポートしていますか。  
サポートしています。
- 簡単なシグナリング操作の場合、TRTCのカスタムシグナルインターフェースsendCustomCmdMsgを使用できます。開発者が対応する制御シグナリングをカスタマイズして、制御シグナリングを受信した通話者が対応する操作を実行すればOKです。例えば、キックアウトとは、追い出しシグナリングを定義することであり、この信号を受信したユーザーは自動的に退室します。
- より完全な操作ロジックを実行する必要がある場合は、開発者が[IM](https://intl.cloud.tencent.com/document/product/1047)を使用して関連のロジックを実行し、TRTCルームとIMグループとのマッピングを行い、IMグループでカスタムメッセージを送受信して、対応する操作を実行することをお勧めします。


[](id:que10)
### TRTCオーディオ・ビデオストリームは、CDNを介したプルストリームによる視聴をサポートしていますか。 
サポートしています。詳細については、[CDN relayed live streamingの実装](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。


[](id:que11)
### iOS端末はSwiftの統合をサポートしていますか。
サポートしています。サードパーティライブラリのフローにそのまま従ってSDKを統合すればOKです。また、[Demoクイックスタート(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)も参照することができます。


[](id:que12)
### デスクトップブラウザSDKはどのブラウザをサポートしていますか。  
現在、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザおよびモバイル版Safariブラウザのサポート状態は比較的万全です。その他のプラットフォーム（Androidプラットフォームのブラウザなど）のサポート状態はまだ不十分です。詳細については、[サポートするプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。
ブラウザで[WebRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTC機能を完全にサポートしているかテストすることができます。


[](id:que13)
### デスクトップブラウザSDKログのエラーメッセージのうち、NotFoundError、NotAllowedError、NotReadableError、OverConstrainedError及びAbortErrorは、それぞれどういう意味ですか。


| エラー名 | 説明 | 推奨する対処方法 |
|---------|---------|---------|
| NotFoundError | リクエストを満たすパラメータのメディアタイプ（オーディオ、ビデオ、画面共有を含む）が見つかりません。<br>例えば、PCにカメラがないのに、ブラウザにビデオストリームを取得するようリクエストがあった場合、このエラーが発生します。| ユーザーが通話を開始する前に、通話に必要なカメラやマイクなどのデバイスを確認することをお勧めします。カメラがなく、音声通話を行う必要がある場合は、[TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)で、マイクのみをキャプチャするように指定できます。 |
| NotAllowedError|ユーザーが、現在のブラウザ・インスタンスのオーディオ、ビデオおよび画面共有へのアクセスのリクエストを拒否しました。| ユーザーに対し、カメラ/マイクへのアクセス権限を付与しないと、オーディオビデオ通話を行うことができません、というプロンプトが表示されます。|
| NotReadableError  | 権限が付与されたユーザーが対応するデバイスを使用していますが、OS上のいずれかのハードウェア、ブラウザまたはWebページの階層に発生したエラーのため、デバイスにアクセスできません。  | ブラウザのエラーメッセージに従って処理すると、ユーザーに対し、「現在カメラ/マイクにアクセスできません。他のアプリケーションがカメラ/マイクへのアクセスをリクエストしていないことを確認してから、もう一度お試しください」というプロンプトが表示されます。|
| OverConstrainedError|   cameraId/microphoneIdのパラメータの値が無効です。 |  cameraId/microphoneIdの渡された値が正しく有効であることを確認してください。|
| AbortError  | 何らかの理由により、デバイスを使用できません。| - |


詳細については、[initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)をご参照ください。


[](id:que14)
### デスクトップブラウザSDKがデバイス（カメラ/マイク）リストを正常に取得できるかどうか確認するにはどうすればいいですか。
1. ブラウザがデバイスを正常に使用できるかどうかチェックします。
ページ上でコンソールを直接開き、`navigator.mediaDevices.enumerateDevices()`と入力して、デバイスリストを取得できるかどうか確認します。
 - デバイスが正常に取得された場合、Promiseが返されます。中にはMediaDeviceInfoオブジェクトの配列があり、配列内の各オブジェクトは使用可能なメディアデバイスに対応しています。
 - 列挙が失敗した場合、Promiseはrejectedを返します。これは、ブラウザがデバイスを認識していないことを示しているので、ブラウザまたはデバイスをチェックする必要があります。
2. デバイスリストを取得できる場合は、`navigator.mediaDevices.getUserMedia({ audio: true, video: true })` と入力して、MediaStreamオブジェクトが正常に返されるかどうか確認します。正常に返されない場合、ブラウザがデータを取得していないことを示しているので、ブラウザの設定をチェックする必要があります。




[](id:que17)
### LVB、ILVB、TRTCおよびRelayed live streamingの違いと関係性は何ですか。
- **LVB**（キーワード：一対多、RTMP/HLS/HTTP-FLV、CDN）
 LVBは、プッシュ端末、再生端末およびライブストリーミングクラウドサービスに分かれます。クラウドサービスはCDNを使用してライブストリームを配信します。プッシュには一般的な標準プロトコルRTMPが使用されます。CDNによって配信された場合、再生するときには通常、RTMP、HTTP-FLVまたはHLS（H5サポート）を選択して視聴することができます。
- **ILV**（キーワード：マイク接続、PK）
 ILVBは、業務形式の1種で、キャスターと視聴者の間のインタラクティブなマイク接続や、キャスターとキャスターの間のインタラクティブなPKを行うライブストリーミングのタイプの1つです。
- **TRTC**（キーワード：マルチプレイヤーインタラクション、UDPプライベートプロトコル、低遅延）
 TRTCの主なユースケースは、オーディオとビデオのインタラクションと低遅延のライブストリーミングです。UDPベースのプライベートプロトコルを使用し、ディレイは100ミリ秒まで引き下げることができます。典型的なシーンは、QQ電話、Tencent Meeting、大規模セミナーなどです。TRTCはプラットフォーム全体をカバーし、iOS/Android/Windowsに加えて、WebRTCの相互運用性、クラウドミクスストリーミングという方法で、CDNへの画面のRelayed live streamingもサポートします。
-**Relayed live streaming**（キーワード：クラウドミクスストリーミング、RTCバイパス・プッシュ転送、CDN）
 Relayed live streamingとは、低遅延のマイク接続ルームにおけるマルチチャンネルのプッシュ画面をコピーして、クラウド内で画面を混合して一つのチャネルにし、ミクスストリーミング後の画面をライブCDNにプッシュして配信、再生する技術のことです。 


[](id:que18)
### TRTCは、通話時間と使用量をどのように確認すればいいですか。  
TRTCコンソールの【[使用量の統計](https://console.cloud.tencent.com/trtc/statistics)】ページで確認することができます。



[](id:que19)
### TRTCにラグが発生した場合はどのように調査すればいいですか。
通話品質は、対応するRoomIDとUserIDを用いて、TRTCコンソールの【[監視ダッシュボード](https://console.cloud.tencent.com/trtc/monitor)】ページで確認することができます。
- 受信端末の視点から送信端末と受信端末ユーザーの状況を確認します。
- 送信端末と受信端末のパケット損失率が高いかどうか確認します。パケット損失率が通常より高い場合、ネットワーク状態が不安定なためにラグが発生しています。
- フレームレートとCPU使用率を確認します。フレームレートが低くCPU使用率が高いと、ラグが発生します。


[](id:que20)
### TRTCに画質の不良、ぼやけ、モザイクなどが発生する場合はどのように調査すればいいですか。
- 解像度は主にビットレートに関係しています。SDKのビットレートが低く設定されているか確認してください。解像度が高く、ビットレートが低いとモザイク現象が起こりやすくなります。
- TRTCは、クラウドQOSトラフィックコントロールポリシーを通じて、ネットワークの状態に応じ、ビットレートと解像度を動的に調整します。ネットワークが貧弱な場合、ビットレートが下がりやすくなり、解像度が低下します。
- 入室時にVideoCallモードとLiveモードのどちらを使用しているかチェックします。通話シーン向けのVideoCallモードは低遅延とスムーズさの維持に重点を置いています。したがって脆弱なネットワークの場合、スムーズさを確保するために画質が犠牲になりやすくなります。画質の方が大事なシーンには、Liveモードの使用をお勧めします。

[](id:que21)
### SDKの最新のバージョン番号はどのように確認しますか。
- 自動ロードを使用する場合は、`latest.release`により最新バージョンとマッチングされて自動ロードが実行されるため、バージョン番号を変更する必要はありません。具体的な統合方法については[SDKクイックインテグレーション](https://intl.cloud.tencent.com/document/product/647/35092)をご参照ください。
- 現在のSDKの最新バージョン番号はリリースノートから確認することができます。以下をご参照ください。
  - iOS & Androidでは、[リリースノート（App）](https://intl.cloud.tencent.com/document/product/647/39426)をご参照ください。
  - デスクトップブラウザでは、[リリースノート（Web）](https://intl.cloud.tencent.com/document/product/647/39779)をご参照ください。
  - Electronでは、[リリースノート（Electron）](https://intl.cloud.tencent.com/document/product/647/38702)をご参照ください。




