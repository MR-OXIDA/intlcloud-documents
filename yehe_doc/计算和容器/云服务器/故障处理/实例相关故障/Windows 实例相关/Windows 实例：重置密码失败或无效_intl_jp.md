このドキュメントでは、Windows Server 2012のOSを例として、Windows CVMインスタンスのパスワードリセットが失敗または有効にならなかった場合のトラブルシューティング方法および対処方法を説明します。

## 現象の説明

- CVMのパスワードをリセットした後、「システムがビジー状態のため、インスタンスはインスタンスパスワードのリセットに失敗しました(7617d94c)」と表示されます。
- CVMのパスワードをリセットした後、新しいパスワードは有効にならず、ログインパスワードは古いパスワードのままです。


## 考えられる原因
CVMパスワードリセットが失敗または有効にならなかったことについて考えられる理由は次のとおりです。
- CVMの`cloudbase-init`コンポーネントが破損している、変更されている、禁止されている、または起動していないことによります。
- CVMに360 Safeguardまたは火絨などのサードパーティ製セキュリティソフトウェアをインストールしており、サードパーティ製セキュリティソフトウェアがパスワードリセットコンポーネント`cloudbase-init`をブロックしたことにより、インスタンスのパスワードリセットが無効になった可能性があります。


## 障害の特定および処理

パスワードリセットの失敗の考えられる原因に従って、次の2つの確認方法が提供されています。

### cloudbase-initサービスの確認

1. [VNCを使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)を参照し、目的のWindowsインスタンスにログインします。
2. OS画面で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>を右クリックして【実行】を選択し、【実行】画面で**services.msc**と入力し、**Enter**を押して「サービス」ウィンドウを開きます。
3. `cloudbase-init`サービスが存在するかどうかを確認します。次の図に示します。
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、`cloudbase-init`サービスを再インストールしてください。具体的な操作については[Windows OSのCloudbase-Initインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
4. ダブルクリックして`cloudbase-init`のプロパティを開きます。次の図に示します。
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. 【通常】タブで、`cloudbase-init`の起動タイプが【自動】に設定されているかどうかを確認します。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、`cloudbase-init`の起動タイプを【自動】に設定してください。
6. 【ログイン】タブに切り替え、`cloudbase-init`のログインIDで【ローカルシステムアカウント】が選択されているかどうかを確認します。
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、`cloudbase-init`のログインIDを【ローカルシステムアカウント】に設定してください。
7. 【通常】タブに切り替え、サービスステータスの【起動】をクリックし、`cloudbase-init`を手動で起動し、エラーが表示されるかどうかを観察します。
 - 「はい」の場合は、[CVMにインストールされているセキュリティソフトウェアを確認する](#CheckSecuritySoftware)を行ってください。
 - 「いいえ」の場合は、次の手順に進んでください。
8. OS画面で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>を右クリックして【実行】を選択し、【実行】画面で**regedit**と入力し、**Enter**を押して「レジストリエディタ」ウィンドウを開きます。
9. 左側のレジストリナビゲーションに、順に【HKEY_LOCAL_MACHINE】>【SOFTWARE】>【Cloudbase Solutions】>【Cloudbase-Init】ディレクトリが表示されます。
10. 【ins-xxx】下のすべての「LocalScriptsPlugin」レジストリを探し、LocalScriptsPluginの数値データが2かどうかを確認します。
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - 「はい」の場合は、次の手順に進んでください。
 - 「いいえ」の場合は、LocalScriptsPluginの数値データを2に設定してください。
11. OS画面で、<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: -3px 0px;"></img>をクリックし、【このコンピュータ】を選択し、デバイスとドライバーの中にCD-ドライバーがロードされているかどうかを確認します。次の図に示します。
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - そうである場合、[CVMにインストールされているセキュリティソフトウェアを確認する](#CheckSecuritySoftware)。
 - そうでない場合、デバイスマネージャでCD-ROMドライブを起動します。

<span id="CheckSecuritySoftware"></span>
### CVMにインストールされているセキュリティソフトウェアを確認する

インストールされているセキュリティソフトウェアでフルスキャンを選択し、CVMに脆弱性がないか、および`cloudbase-init`のコアコンポーネントがブロックされていないかを確認します。
- CVMの脆弱性が検出された場合は、修復してください。
- コアコンポーネントのブロックが検出された場合は、ブロックを取り消してください。

`cloudbase-init`コンポーネントの確認および設定の手順は次のとおりです。
1. [VNCを使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)を参照し、目的のWindowsインスタンスにログインします。
2. 実際にインストールされているサードパーティ製セキュリティソフトウェアに応じて、`cloudbase-init`コンポーネントをリカバリし、設定します。

<dx-tabs>
::: 360 Safeguard
360 Safeguardはインストール完了後、システムを定期的にスキャンします。`cloudbase-init`コンポーネントをスキャンすると、ハイリスクと認識して隔離する場合があります。次の手順を参照してコンポーネントをリカバリするとともに、信頼できるファイルとして設定してください。

1. 360 Safeguardを開き、【トロイの木馬の検出と駆除】>【リカバリエリア】を選択します。次の図に示します。
![](https://main.qcloudimg.com/raw/cfc16c35c1eafbf4938f5ef4711cf0ee.png)
2. ポップアップした「セキュリティ操作センター」ウィンドウで、ファイルにチェックを入れ、【選択したものをリカバリ】をクリックします。
3. ポップアップした確認ウィンドウで、 「リカバリ後はこのファイルを信頼し、検出・駆除を行いません」にチェックを入れ、【リカバリ】をクリックすれば完了です。次の図に示します。
![](https://main.qcloudimg.com/raw/4e7dee481a05243cec89ba5c6b1a5eb0.png)
:::
::: 火絨セキュリティソフトウェア
火絨セキュリティソフトウェアはインストール完了後、`cloudbase-init`コンポーネントを自動的に隔離することはありませんが、`cloudbase-init`のパスワード変更行為をブロックすることがあります。次の手順を参照し、コンポーネントを信頼できるファイルとして設定してください。
1. 火絨セキュリティソフトウェアを開き、右上隅の<img src="https://main.qcloudimg.com/raw/66dcf0fca93bab386180ab4337ebda92.png" style="margin:-3px 0px">を選択し、ポップアップメニューの中から【信頼エリア】をクリックします。次の図に示します。
![](https://main.qcloudimg.com/raw/93e25735ff17294bb36d224b074ec67a.png)
2. ポップアップした「信頼エリア」ウィンドウで、下記のファイルおよびフォルダを順に追加すれば完了です。次の図に示します。
![](https://main.qcloudimg.com/raw/a8b0bd702407e5100238237fb6a5821a.png)
ファイルおよびフォルダパスは次のとおりです。
 - `C:\Program Files\Cloudbase Solutions`
 - `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts`
 - `C:\Program Files\QCloud`
 - `C:\Windows\System32\cmd.exe`
 - `C:\Windows\System32\WindowsPowerShell`
 - `C:\Windows\SysWOW64\cmd.exe`
:::
</dx-tabs>


