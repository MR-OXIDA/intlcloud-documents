ユーザーは以下の特徴に応じてイメージを選択することができます。
- 位置（[リージョンとアベイラビリティーゾーン](https://intl.cloud.tencent.com/document/product/213/6091)をご参照ください）
- オペレーティングシステムのタイプ
- アーキテクチャ（32ビットまたは64ビット）

異なるソースに応じて、Tencent Cloudは以下のイメージタイプを提供します。パブリックイメージ、カスタムイメージ、共有イメージ。

## パブリックイメージ
**パブリックイメージ**はTencent Cloudを介して公式に提供されるイメージです。これには基本的なオペレーティングシステムおよびTencent Cloudが提供する初期化コンポーネントが含まれ、すべてのユーザーが使用することができます。

パブリックイメージの特徴:
 - **オペレーティングシステムのタイプ：**自由選択（例：LinuxタイプのシステムまたはWindowsタイプのシステム）で、定期的に更新されます。
 - **ソフトウェアのサポート：**Tencent Cloudが提供するソフトウェアパッケージ（API等）を統合し、複数のバージョンのJava、MySQL、SQL Server、Python、Ruby、Tomcat等の一般的なソフトウェアおよびそれらの完全な権限をサポートしています。
 - **セキュリティ：**提供するオペレーティングシステムは完全に合法的なものであり、すべて公式の正規版OSを使用しています。Tencent Cloud内の専門的なセキュリティメンテナンスチームにより作成され、厳格なテストが実行されました。内蔵されているTencent Cloudセキュリティコンポーネントを選択することができます。
 - **制限：**現在は使用上の制限がありません。
 - **料金：**中国大陸地区以外の他のリージョンでは、Windowsタイプのイメージの場合、一定のLicense料金が発生します。それ以外はすべて無料です。
 - **テクニカルサポート：**
  - Tencent LinuxはTencent Cloudのサポートおよびメンテナンスを受けており、関係するテクニカルサポートが提供されます。
  - サードパーティイメージに関連する問題については、オープンソースコミュニティまたはOS開発企業にご連絡いただきテクニカルサポートを受けてください。Tencent Cloudは問題を調査するための技術的な協力を提供いたします。



## カスタムイメージ[](id:customOS)
**カスタムイメージ**はユーザーがイメージ作成機能を使用して作成、またはイメージインポート機能を使用してインポートするイメージです。作成者および共有者のみ使用することができます。

カスタムイメージの特徴：
 - **ユースケース：**デプロイ済みアプリケーションの1つのCVMインスタンスに対してイメージを作成し、同様の設定を含むさらに多くのインスタンスを素早く作成することができます。
 - **機能のサポート：**ユーザーによる自由な作成、コピー、共有および破棄をサポートしています。
 - **制限：**リージョン毎に最大10のカスタムイメージがサポートされます。
 - **料金：**作成すると料金が発生する場合がありますが、具体的な価格はインスタンス作成時に表示される料金に基づきます。地域間コピーされるカスタムイメージでは、今のところ料金は発生しません。

さらに多くの操作方法および制限については、[カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)、[カスタムイメージのコピー](https://intl.cloud.tencent.com/document/product/213/4943)、[カスタムイメージの共有](https://intl.cloud.tencent.com/document/product/213/4944)、[カスタムイメージの共有を取り消す](https://intl.cloud.tencent.com/document/product/213/7148)、[カスタムイメージのインポート](https://intl.cloud.tencent.com/document/product/213/4945)をご参照ください。

## 共有イメージ
**共有イメージ**は、Tencent Cloudの他のユーザーがイメージ共有機能を通じて自分のカスタムイメージを現在のユーザーに共有することです。
共有されたイメージは共有されるユーザーの元のイメージと同じリージョンで表示されます。

共有イメージの特徴
 - **ユースケース：**他のユーザーがCVMを素早く作成するために役立ちます。
 - **機能のサポート：**共有イメージはCVMの作成にのみ使用され、名前の変更、コピー、共有等の他の操作を実行することはできません。
 - **セキュリティ：**共有されたイメージはTencent Cloudの審査を受けないため、セキュリティリスクが存在する可能性があります。そのため、ソース元が不明なイメージを受け入れないように強くお勧めします。
 - **制限：**カスタムイメージ毎に最大50のTencent Cloudユーザーと共有することができます。イメージ共有はアカウントが同じリージョンの相手との共有のみをサポートしています。

詳細手順については、[カスタムイメージの共有](https://intl.cloud.tencent.com/document/product/213/4944)、[カスタムイメージの共有を取り消す](https://intl.cloud.tencent.com/document/product/213/7148)をご参照ください。


