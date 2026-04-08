# Messaging APIの料金

このページでは、Messaging APIを使ってメッセージを送る際に発生する料金について説明します。

<!-- table of contents -->

## 料金の仕組み 

LINE公式アカウントには、無料のプランと、月額固定費がかかるプランがあります。

いずれのプランも、毎月一定数のメッセージを無料で送信できます。送信できる無料メッセージ通数は、料金プランによって異なります。また、月の途中で上位の料金プランに変更すると、その月の無料メッセージ通数を増やすことができます。

無料メッセージ通数を超えて、追加メッセージを送信できるプランもあります。追加メッセージを送信すると、送信数に応じた料金がかかります。追加メッセージを送信するには、[LINE Official Account Manager](https://manager.line.biz/)で対象のLINE公式アカウントを選択して、追加メッセージが利用可能な料金プランに変更した上で、追加メッセージ数の上限目安を設定する必要があります。

### 国・地域ごとの料金プラン 

国・地域ごとの料金プランについては、下記を参照してください。

| 国・地域 | 料金情報 |
| --- | --- |
| 日本 | [LINE公式アカウント料金プラン](https://www.lycbiz.com/jp/service/line-official-account/plan/) <br> [利用と請求（プラン変更やお支払い関連の管理）](https://www.lycbiz.com/jp/manual/OfficialAccountManager/account-settings_plan/) |
| 台湾 | [LINE Official Account](https://tw.linebiz.com/service/account-solutions/line-official-account/) <br> [LINE Official Account - FAQ](https://tw.linebiz.com/faq/oa-price/) |
| タイ | [LINE Official Account](https://lineforbusiness.com/th/service/line-oa-features/broadcast-message) |
| その他の地域 | [LINE Official Account](https://www.lycbiz.jp/en/other/) |

### 料金プランの例 

次の表は、日本の料金プランの例です。

|  | コミュニケーションプラン | ライトプラン | スタンダードプラン |
| :-- | :-: | :-: | :-: |
| 月額固定費 [^1] | 0円 | 5,000円 | 15,000円 |
| 無料メッセージ通数 （月） | 200通 | 5,000通 | 30,000通 |
| 追加メッセージ料金 [^1] | 不可 | 不可 | ～3円/通 [^2] |

[^1]: 税別。

[^2]: 追加メッセージの単価は送信数によって異なります。

たとえば、月に1,000通のメッセージを送信したい場合は、無料メッセージ通数が5,000通のライトプランを選択します。

月に40,000通のメッセージを送信するには、無料メッセージ通数が30,000通のスタンダードプランを選択した上で、無料分を超過する10,000通分の追加メッセージ料金が必要になります。

料金プランは国または地域によって異なりますので、[該当する地域の料金プラン](https://developers.line.biz/ja/docs/messaging-api/pricing/#global-pricing)をご確認ください。

## 無料メッセージ通数を超過した場合 

当月に送信できるメッセージ通数の上限を超えてメッセージを送信しようとした場合、エラーレスポンスが返りメッセージは送信されません。詳しくは、『Messaging APIリファレンス』の「[ステータスコード](https://developers.line.biz/ja/reference/messaging-api/#status-codes)」および「[エラーレスポンス](https://developers.line.biz/ja/reference/messaging-api/#error-responses)」を参照してください。

当月の利用状況は、以下のエンドポイントで確認できます。

- [当月に送信できるメッセージ数の上限目安を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-quota)
- [当月のメッセージ利用状況を取得する](https://developers.line.biz/ja/reference/messaging-api/#get-consumption)

料金プランを変更して無料メッセージ通数を増やす、または追加メッセージを送信する方法については、「[料金の仕組み](https://developers.line.biz/ja/docs/messaging-api/pricing/#pricing-system)」を参照してください。

## メッセージ通数のカウント方法について 

メッセージ通数は、メッセージの送信対象となった人数でカウントされます。たとえばメッセージオブジェクトを4件指定したプッシュメッセージを、5人いるトークルームに対して1回送った場合、カウントされるメッセージ通数は5通です。1回のリクエストで指定した[メッセージオブジェクト](https://developers.line.biz/ja/reference/messaging-api/#message-objects)の件数は、メッセージ通数には影響しません。

またLINE公式アカウントをブロックしているユーザーIDや、存在していないユーザーIDなど、メッセージが実際には届かないユーザーを宛先に指定してメッセージを送信した場合は、メッセージ通数にはカウントされません。

## 料金プランのメッセージ通数としてカウントされる送信方法 

Messaging APIについて、すべてのメッセージ送信が料金プランのメッセージ通数としてカウントされるわけではありません。メッセージ通数としてカウントされる送信方法とされない方法を以下に示します。

- メッセージ通数としてカウントされる送信方法
  - [プッシュメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-push-message)
  - [マルチキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-multicast-message)
  - [ブロードキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-broadcast-message)
  - [ナローキャストメッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-narrowcast-message)
- メッセージ通数としてカウントされない送信方法
  - [応答メッセージ](https://developers.line.biz/ja/reference/messaging-api/#send-reply-message)

Messaging API以外のメッセージ機能の料金について詳しくは、『LINEヤフー for Business』の「[課金対象となるメッセージについて](https://www.lycbiz.com/jp/service/line-official-account/plan/)」を参照してください。
