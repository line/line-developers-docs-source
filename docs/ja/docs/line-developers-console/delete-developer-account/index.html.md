# 開発者アカウントを削除する

LINE Developersコンソールを利用する必要がなくなった場合は、[開発者アカウント](https://developers.line.biz/ja/docs/line-developers-console/login-account/#register-as-developer)を削除できます。開発者アカウントを削除すると、その開発者アカウントではLINE Developersコンソールにログインできなくなります。

<!-- warning start -->

**削除した開発者アカウントは元に戻せません**

一度削除した開発者アカウントは元に戻せません。そのため、削除した開発者アカウントが権限を持っていたプロバイダーやチャネルに他の開発者アカウントがアクセスできない場合、プロバイダーやチャネルの情報確認や設定変更ができなくなります。

開発者アカウントを削除する前に、運用中のサービスに影響が出ないよう、必要な権限を他の開発者アカウントに付与してください。

<!-- warning end -->

## 開発者アカウントを削除する 

開発者アカウントを削除するには、以下の手順に従ってください。

1. [LINE Developersコンソール](https://developers.line.biz/console/)にログインする。
1. 画面右上のプロフィールアイコンをクリックする。
1. アカウント情報をクリックし、[プロフィール画面](https://developers.line.biz/console/profile)を開く。
1. 「開発者アカウントの削除」セクションで、［**削除**］をクリックする。
1. 確認画面の内容を確認し、画面に表示されているDeveloper IDを入力後、［**上記に同意し、この開発者アカウントの永久削除を希望します。**］チェックボックスを選択し、［**削除**］をクリックする。

   ![](https://developers.line.biz/media/line-developers-console/delete-developer-account-confirmation-ja.png)

開発者アカウントの削除が完了すると、LINE Developersサイトのトップページへリダイレクトされます。また、登録していたメールアドレス宛てに、アカウント削除の完了を知らせるメールが送信されます。

### ［削除］ボタンが無効になっている場合 

以下の両方に当てはまるプロバイダーやチャネルがある場合、開発者アカウントを削除できません。

- 削除する開発者アカウントの以外にも、権限を持つ開発者アカウントが存在する。
- 削除する開発者アカウントだけがAdmin権限を持っている。

この場合、［**削除**］ボタンが無効になり、削除できない理由と対処方法を示すメッセージが表示されます。

![](https://developers.line.biz/media/line-developers-console/delete-developer-account-disabled-ja.webp)

該当するプロバイダーやチャネルで、他の開発者アカウントにAdmin権限を付与してから、アカウントを削除してください。権限を管理する方法について詳しくは、「[権限を管理する](https://developers.line.biz/ja/docs/line-developers-console/managing-roles/)」を参照してください。

なお、削除する開発者アカウントの他に、プロバイダーやチャネルの権限を持つ開発者アカウントが存在しない場合は、開発者アカウントを削除できます。

<!-- note start -->

**プロバイダーやチャネルを削除する場合**

［**削除**］ボタンをクリックできない場合は、他の開発者アカウントにAdmin権限を付与する代わりに、該当するプロバイダーやチャネルを削除する方法もあります。ただし、プロバイダーやチャネルを削除すると、稼働中のサービスが利用できなくなる可能性があります。プロバイダーやチャネルを削除する前に、サービスへの影響がないことを確認してください。

また、ブロックチェーンサービスおよびLINEミニアプリのチャネルは、LINE Developersコンソールから削除できません。これらのチャネルでは、他の開発者アカウントにAdmin権限を付与してください。

プロバイダーやチャネルを管理する際の考え方について詳しくは、「[プロバイダーとチャネル管理のベストプラクティス](https://developers.line.biz/ja/docs/line-developers-console/best-practices-for-provider-and-channel-management/)」を参照してください。

<!-- note end -->

## 開発者アカウントを削除した後の状態 

開発者アカウントを削除すると、以下の状態になります。

- 削除した開発者アカウントでは、LINE Developersコンソールにログインできなくなります。
- 削除した開発者アカウントからは、これまで権限を持っていたプロバイダーやチャネルにアクセスできなくなります。

なお、開発者アカウントを削除しても、開発者アカウントに紐づく[ビジネスID](https://help2.line.me/business_id/web/?lang=ja&contentId=20011264)やLINEアカウントは削除されません。

### LINE Developersコンソールの利用を再開する 

同じビジネスIDでLINE Developersコンソールを再度利用するには、[初回ログイン時](https://developers.line.biz/ja/docs/line-developers-console/login-account/#register-as-developer)と同じように新しい開発者アカウントを作成します。この場合、削除前とは別の開発者アカウントとして作成されるため、削除前の開発者アカウントが持っていたプロバイダーやチャネルの権限は引き継がれません。開発者アカウントの作成について詳しくは、「[開発者アカウントを作成する（初回ログイン時のみ）](https://developers.line.biz/ja/docs/line-developers-console/login-account/#register-as-developer)」を参照してください。
