# LINE公式アカウントの利用を停止する

<!-- tip start -->

**Messaging APIの利用を停止する**

Messaging APIチャネルに紐づいているLINE公式アカウントの利用は継続したいが、Messaging APIの利用は停止したい場合は、「[Messaging APIの利用を停止する](https://developers.line.biz/ja/docs/messaging-api/stop-using-messaging-api/)」を参照してください。

<!-- tip end -->

Messaging APIチャネルと紐づいているLINE公式アカウントの利用を停止するには、以下の手順に従って、LINE公式アカウントを削除してください。Messaging APIチャネルと紐づいているLINE公式アカウントを削除すると、Messaging APIチャネルも削除されます。

1. [LINE Developersコンソール](https://developers.line.biz/console/)で、削除するMessaging APIチャネルを選択します。
2. ［**チャネル基本設定**］タブが表示されます。「チャネルの削除」セクションにある［**削除**］をクリックします。

![](https://developers.line.biz/media/messaging-api/stop-using-line-official-account/delete-this-channel-ja.png)

3. 「このチャネルを削除しますか？」モーダルが表示されます。［**LINE Official Account Managerを表示**］をクリックします。

![](https://developers.line.biz/media/messaging-api/stop-using-line-official-account/display-line-official-account-manager-ja.png)

4. LINE Official Account Managerが別タブで開かれ、「LINE公式アカウントを削除」画面が表示されます。以降の手順は、LINE Official Account Manager上で操作します。［**上記の注意事項を理解して、このLINE公式アカウントの削除に同意します。**］にチェックし、［**アカウントを削除**］をクリックします。

![](https://developers.line.biz/media/messaging-api/stop-using-line-official-account/delete-account-ja.png)

<!-- note start -->

**「LINE公式アカウントを削除」画面ではなく「403 Forbidden」が表示される**

LINE公式アカウントを削除するには、LINE公式アカウントの管理者権限が必要です。LINE公式アカウントの権限は、[LINE Official Account Manager](https://manager.line.biz)で設定できます。詳しくは、『LINEヤフー for Business』の「[権限設定](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_permission/)」および「[【LINE公式アカウント】管理者の追加・変更](https://help.linebiz.com/lineadshelp/s/article/L000001104?language=ja)」を参照してください。

<!-- note end -->

5. 「LINE公式アカウントを削除」モーダルが表示されます。［**削除**］をクリックすると、LINE公式アカウントが削除され、LINE公式アカウントに紐づくMessaging APIチャネルも削除されます。

![](https://developers.line.biz/media/messaging-api/stop-using-line-official-account/delete-ja.png)
