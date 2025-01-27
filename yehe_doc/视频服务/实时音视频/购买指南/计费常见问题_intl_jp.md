[](id:que0)

### サービス使用量が大量なのですが、割引は受けられますか。

- 通常割引：パッケージの仕様が大きくなるほど割引率が高くなります。例えば、300万分以上の仕様のパッケージを購入した場合、20%の割引が適用されます。
- 長期割引：お客様のTRTCの月間消費額が3000米ドルを超える場合は、[お問い合わせ](https://intl.cloud.tencent.com/contact-us)にお問い合わせいただき、契約を締結することで長期割引が適用されます。

### TRTCはどのように課金されますか。

TRTCの課金項目はサービスのタイプによって基本サービスと付加価値サービスの2つに分かれます。詳細な課金説明については[課金概要](https://intl.cloud.tencent.com/document/product/647/34610)をご参照ください。新規ユーザーには10000分間の[無料時間](https://intl.cloud.tencent.com/document/product/647/42735)を提供しています。

[](id:que1)

### どのように請求書と控除明細を確認できますか。
[料金センター > 請求書詳細](https://console.cloud.tencent.com/expense/bill/summary)で請求書と控除明細の詳細を確認することができます。

[](id:que3)
### どのように従量課金明細を確認/取得できますか。
- リアルタイム使用量：TRTCコンソール - [使用量の統計](https://console.cloud.tencent.com/trtc/statistics)画面で、使用状況のグラフや詳細なフローデータを直接確認することができます。単日では5分ごとの明細を、複数日では1日ごとに集計した明細を表示します。分単位でカウントされます。
- 請求書使用量：Tencent Cloud料金センターで、出力した請求書に対応する使用量の明細を[ダウンロード](https://console.cloud.tencent.com/expense/bill/dosageDownload)できます。ダウンロードの結果は、5分ごとの明細と日ごとの明細を含むExcelファイルです。秒単位でカウントされます。
- サーバーAPI：より高度なニーズがある場合は、[サーバーAPI](https://intl.cloud.tencent.com/document/product/647/42971)を通じて詳細な従量課金データを取得することもできます。問い合わせる時間が1日以下の場合は、5分単位のデータを返します。問い合わせ時間が1日より大きい場合は、1日ごとに集計したデータを返します。秒単位でカウントされます。

>!リアルタイム使用量データはリアルタイムに変化するため、最終的な決済使用量とは若干異なる場合があります。**請求書使用量を基準としてください**。

[](id:que4)
### どのようにパッケージの残りの分数を確認できますか。
パッケージはリアルタイム控除方式を採用し、5分ごとに一度、残りの分数を更新します。[パッケージ管理](https://console.cloud.tencent.com/trtc/package)画面でパッケージの残りの分数を確認できます。

[](id:que5)
### 秒単位で課金され、1分未満の残高は1分としてカウントすると、パッケージを使用した時に分数を多く差し引くことになりませんか。
いいえ。パッケージから差し引かれる分数は、当日の累積時間に応じて計算され、二重に差し引かれることはありません。
パッケージから分数を差し引く操作例は下表のとおりです。

|統計区間|区間サービス使用量|累計サービス使用量|累計課金時間|区間控除時間|累計控除時間|
|---|---|---|---|---|---|
|00:00:00 - 00:04:59|30秒|30秒|1分|1分控除|1分控除|
|00:05:00 - 00:09:59|20秒|50秒|1分|0分控除|1分控除|
|00:10:00 - 00:14:59|40秒|90秒|2分|1分控除|2分控除|


[](id:que6)
### 新しく購入したパッケージから差し引かれる分数が、パッケージ購入後の使用量より多いのはなぜですか。

新しく購入したパッケージが有効になると、新しいパッケージ購入当日の0時を起点として発生した、その他のパッケージから差し引かれていない使用量が、すぐに差し引かれます。TRTCコンソールの[使用量の統計](https://console.cloud.tencent.com/trtc/statistics)画面で、パッケージ購入当日の使用量を確認できます。

[](id:que15)
### 購入した音声/SD/HDパッケージは一般パッケージに切り替えられますか。
できます。具体的なルールは以下のとおりです。
- **音声パッケージ**1分 = 一般パッケージ1分。
- **SDパッケージ**1分 = 一般パッケージ2分。
- **HDパッケージ**1分 = 一般パッケージ4分。

自動切り替えは現在行っていません。必要があれば、[チケットを提出](https://console.cloud.tencent.com/workorder/category)でサポートを受けることができます。 

[](id:que7)
### 一般パッケージを購入できないと表示されるのはなぜですか。
グローバルサイトは現在、ホワイトリストの審査を受けなければ関連サービスの利用ができないという状態です。[チケットを提出](https://console.cloud.tencent.com/workorder/category) してサポートを受けることができます。

[](id:que16)
### 自分の業務の基本サービス使用量と料金の見積もりはどのように行えますか。
ご自身の業務で発生する使用量と料金の見積もり方法がわからない場合は、[TRTC価格計算機](https://buy.cloud.tencent.com/price/trtc/calculator)による計算補助を利用することができます。

[](id:que8)
### ビデオ通話やビデオ・インタラクティブストリーミングで、どうして音声時間が発生するのですか。
通常の状況で、ユーザーが1つのオーディオ・ビデオストリーミングを購読する際は、オーディオデータとビデオデータの両方が含まれます。送信者がカメラをオフ、受信者がビデオ画面をオフ、受信者のネットワーク異常、部屋に1人しかいない等の状況がある場合、ユーザーが実際にはビデオ画面を受信していないことになります。料金を節約するため、ユーザーがビデオ画面を受信しない時は、TRTCは音声時間によって使用量をカウントします。

[](id:que9)
### 画面共有はどのように課金されますか。
画面共有は、画面シェアとも呼ばれますが、単独のビデオストリームです。ユーザーが画面共有でビデオストリームを購読し、ビデオ画面を受信すると、ビデオ時間に応じて課金されます。

[](id:que10)

### CDNライブストリーミングの視聴はどのように課金されますか。
TRTCはRelayed Pushにより[CSS](https://intl.cloud.tencent.com/document/product/267)の能力を使用し、CDN relayed live streamingの機能をご提供しています。**CSS**は実際のご利用状況に応じて[CDN relayed live streaming≻関連費用](https://intl.cloud.tencent.com/document/product/647/35242)を請求します。

[](id:que12)

### 1人しかルームにいない場合も課金されますか。
1人しかルームにいない場合、ストリームをプッシュしなくても（アップストリームデータが生成されなくても）、TRTCのクラウドサービスリソースを消費します。ルームに1人の場合は、他の人のオーディオ・ビデオストリーミングを購読できず、ビデオ画面を受信することはないため、**音声時間**によってサービス使用量をカウントします。

[](id:que13)
### サービスのステータスが「サービス停止」と表示されるのはなぜですか。
- Tencent Cloudアカウントに支払い遅延があるためサービス停止に至った場合：[支払い遅延の解消](https://console.cloud.tencent.com/expense/overview)の後、サービスは自動的に復旧します。
- 手動操作でアプリケーションを無効化したため、サービスが停止状態となっている場合：【アプリケーションの有効化】をクリックするとサービスを再開できます。

