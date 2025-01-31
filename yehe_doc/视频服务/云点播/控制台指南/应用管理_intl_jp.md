## 操作シナリオ
ユーザーはアプリケーション管理を通じて、アプリケーション内のリソースの非アクティブ化や削除ができるので、アプリケーションをよりフレキシブルに管理できます。VODアプリケーションには、通常・非アクティブ化・削除という3つのステータスがあります。アプリケーションのライフサイクルと関連ステータスの意味を次の図に示します。
![](https://qcloudimg.tencent-cloud.cn/raw/5d453fecd052b987f8219a2fe4e331a2.png)



| ステータスコード | 意味 |
|---------|---------|
| 通常 | このステータスでは、アプリケーションが標準的に使用されている状態にあり、ユーザーは設定の変更、関連のMPS、メディア資産管理などの操作を実行することができます。 |
|非アクティブ化済み|このステータスでは、ユーザーのアプリケーションは非アクティブ化され、このアプリケーションのリソースと設定ファイルが保存されます。対応するリソースが対応する課金項目に従って課金されますが、このステータスではアプリケーションの設定を変更したり、パブリックネットワークからアクセスしたりすることはできません。|
|削除済み|このステータスでは、アプリケーション内リソースは完全に削除され、すべてのリソースと設定ファイルがクリアされ、リソースと設定が元に戻らなくなります。シャットダウンシナリオに適しています。|

>!
>- 削除されたアプリケーションに対して、再アクティブ化をサポートしています。アクティブ化されたアプリケーションのID（appid/subappid）は変更しません。
>- 統計データにある程度の遅延があるため、アプリケーションが削除された後のデータ統計にはある程度の遅延が生じます。これは正常な現象であり、ユーザーの料金決済には影響しません。
>- アプリケーションのステータスを変更するには5～10分かかるため、ユーザーは頻繁に変更操作をしないでください。

アプリケーションにはVODユーザーのリソース管理権限が含まれるため、アプリケーションの非アクティブ化と削除操作は強制的かつセンシティブ権限に該当します。そのため、ユーザーの身元確認が必要で、確認後に操作が許可されます。身元確認にパスしてから30分間は、再度の確認は不要です。
アプリケーション管理機能の操作画面は、ユーザーがサブアプリケーションを開くかどうかに応じて変更されます。これら2つのシナリオ向けのコンソールガイドラインは、次のとおりです。

## アカウントにサブアプリケーションがない場合
アカウントにサブアプリケーションがない場合、アプリケーション管理は【共通ツール】によって行い、ユーザーはサブアプリケーションをアカウントに直接追加して、詳細を表示することができます。![](https://qcloudimg.tencent-cloud.cn/raw/6f80829605ee04ce07b6414f2fc2c405.png)
この時点で、ユーザーはすぐにサブアプリケーションを作成して詳細を表示することができます。

## アカウントに複数のサブアプリケーションがある場合
アカウントに複数のサブアプリケーションがある場合、アプリケーション管理は、管理者 >【アプリケーション管理】で行い、ユーザーはアプリケーション全体のステータスを変更することができます。ユーザーは、サブアプリケーションステータスで現在のアプリケーションステータスを確認できます。
![](https://qcloudimg.tencent-cloud.cn/raw/279d7be223412490b95bb0d73e2ed55d.png)
ユーザーは、切り替えスイッチを使用して、サブアプリケーションスを有効または無効にすることができます。

## 特記事項：
1. ユーザーにサブアプリケーションがない場合
	- メインアプリケーションを削除すると、VODアカウントのリソースと設定がクリアされます。
	- メインアプリケーションを削除した後に再アクティブ化すると、VODアカウントも再アクティブ化されます。ユーザーがアカウントの料金を滞納している場合、残高が0になるようにしてください。そうしないと使用できなくなります。

2. ユーザーにサブアプリケーションがある場合
	- ユーザーがメインアプリケーションを削除したい場合、必ずすべてのメイン/サブアプリケーションをあらかじめ非アクティブ化する必要があります。そうしないと、操作を実行できなくなります。
	- ユーザーがメインアプリケーションの削除後にサブアプリケーションを再アクティブ化する場合は、他のサブアプリケーションを再アクティブ化する前に、まずメインアプリケーションを再アクティブ化する必要があります。そうしないと、操作を実行できなくなります。

