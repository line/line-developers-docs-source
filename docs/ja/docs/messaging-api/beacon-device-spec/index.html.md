# LINE Beacon端末の仕様

このLINE Beaconの仕様は、LINE Beaconを利用するためにビーコン端末を導入したい法人ユーザー向けの仕様です。ビーコン端末は本仕様に準拠する必要があります。

[LINE Simple Beacon](https://github.com/line/line-simple-beacon)と異なり、LINE Beaconのパケットには、セキュリティを保護する仕組みとして[Secure message](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#generating-secure-message)が含まれます。

## LINE Beacon対応端末の要件 

LINE Beaconに対応するビーコン端末とは、Bluetooth® Low Energy Version 4.0とAppleの[iBeacon](https://developer.apple.com/ibeacon/)に対応し、LINE Beaconパケットをアドバタイズできるビーコン端末です。具体的には、以下の条件を満たす必要があります。

- [LINE Beaconパケット](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#line-beacon-packet)をアドバタイズする。
- SHA-256とXOR（排他的論理和）の演算でハッシュ化したデータから[Secure message](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#generating-secure-message)を生成する。
- Secure messageを15秒間隔で更新する。
- 端末固有の[HWID](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#hwid)が割り当てられ、端末本体にHWIDが表示されている。

## LINE Beaconパケット 

LINEがビーコン端末を迅速に発見できるよう、Generic access profileで規定されるBroadcaster role（BLUETOOTH SPECIFICATION Version 4.0 [Vol 3], Part C Section 2.2.2.1）に従って、ビーコン端末を制御する必要があります。

### パケットの送信間隔 

LINE Beaconパケットは、152.5ミリ秒間隔で送信することを強く推奨します。

### アドバタイジングパケットの仕様 

アドバタイジングパケットは、以下の図のように、3つのAD structureから構成してください。

![LINE Beaconパケット](https://developers.line.biz/media/messaging-api/beacon-device-spec/advDataFormat.png)

アドバタイジングパケットの仕様は以下のとおりです。値カラムの16進数の値は、説明カラムの括弧書きの値と同等です。

| オクテット | フィールド | 値 | 説明 |
| --- | --- | --- | --- |
| 00 | Length | 0x02 | 第1のAD structureのデータ長（2バイト） |
| 01 | AD type | 0x01 | 第1のAD structureのAD type（Flags） |
| 02 | AD data | 0x06 | Flags（LE General Discoverable Mode、BR/EDR Not Supported） |
| 03 | Length | 0x03 | 第2のAD structureのデータ長（3バイト） |
| 04 | AD type | 0x03 | 第2のAD structureのAD type（Complete list of 16-bit UUIDs available） |
| 05 | 16-bit UUID | 0x6F | 次のバイトと合わせてLINEの16ビットUUID（0xFE6F）を示します。 |
| 06 | 16-bit UUID | 0xFE | 前のバイトと合わせてLINEの16ビットUUID（0xFE6F）を示します。 |
| 07 | Length | 0x11 | 第3のAD structureのデータ長（17バイト） |
| 08 | AD type | 0x16 | 第3のAD structureのAD type（Service Data - 16-bit UUID） |
| 09 | 16-bit UUID | 0x6F | 次のバイトと合わせてLINEの16ビットUUID（0xFE6F）を示します。 |
| 10 | 16-bit UUID | 0xFE | 前のバイトと合わせてLINEの16ビットUUID（0xFE6F）を示します。 |
| 11 | Frame type | 0x02 | フレームタイプ（LINE Beacon） |
| 12-16 | HWID | 端末固有の値 | ビーコン端末の5バイトの固有ID。詳しくは、「[HWID](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#hwid)」を参照してください。 |
| 17 | Measured TxPower | 端末固有の値 | LINEがインストールされているデバイスとビーコン端末の距離が1メートルの場合のRSSI（受信信号強度インジケータ）。iBeaconパケットと同様の値を設定します。詳しくは、iBeaconのドキュメントを参照してください。<br />RSSIのデータを利用しない場合は、0x7Fを指定します。 |
| 18-21 | Message authentication code | 変動値 | [メッセージ認証](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#step-one-generate-message-auth-code)のための4バイトコード |
| 22-23 | Masked timestamp | 変動値 | 2バイトの[マスクしたタイムスタンプ](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#step-two-generate-masked-timestamp) |
| 24 | Battery level | 変動値 | [バッテリー残量](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#battery-level) |
| 25-30 | Non-significant part | 0x00 | 未使用部。すべて0x00を指定します。 |

## Secure messageを生成する 

Secure messageは、LINE Beaconパケットの改ざんやリプレイ攻撃を防ぐために使用します。Secure messageは、Message authentication code、Masked timestamp、およびBattery levelを連結した7バイトのデータです。ビーコン端末から発信されたSecure messageは、LINE経由でLINEプラットフォームに送信され、検証されます。

Secure messageを生成するには、SHA-256で生成したハッシュ値に対してXOR（排他的論理和）演算を3回実行します。以下の図は、Secure messageの生成の流れを示します。生成に必要なパラメータについては、「[Secure messageに必要なパラメータ](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#parameters)」を参照してください。

![Secure messageの生成アルゴリズム](https://developers.line.biz/media/messaging-api/beacon-device-spec/secureMessageAlgorithm.png)

Secure messageは、以下の手順に従って生成します。

### 1. Message authentication codeを生成する 

1. 以下の項目を順に連結し、SHA-256を使って32バイトのハッシュ値を生成します。

   - [Timestamp](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#timestamp)
   - [HWID](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#hwid)
   - [Vendor key](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#vendor-key)
   - [Lot key](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#lot-key)
   - [Battery level](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#battery-level)

1. ハッシュ値の前半の16バイトと後半の16バイトの排他的論理和を求めます。
1. 前のステップで得た値の前半の8バイトと後半の8バイトの排他的論理和を求めます。
1. 前のステップで得た値の前半の4バイトと後半の4バイトの排他的論理和を求めます。

これで、Message authentication codeが完成します。

### 2. Masked timestampを生成する 

タイムスタンプの冒頭から6バイトをマスクして、末尾の2バイトを残します。これがMasked timestampです。

### 3. 項目を連結する 

Secure messageを生成するには、以下の項目を順に連結します。

- [ステップ1](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#step-one-generate-message-auth-code)で生成したMessage authentication code
- [ステップ2](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#step-two-generate-masked-timestamp)で生成したMasked timestamp
- [Battery level](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#battery-level)

これで、Secure messageが完成します。Secure messageを生成するためのビーコン端末の開発とテストについては、「[Secure message生成のサンプルデータとコード](https://developers.line.biz/ja/docs/messaging-api/secure-message-sample/)」を参照してください。

### Secure messageに必要なパラメータ 

Secure messageを生成するには、以下のパラメータが必要です。

- [Battery level](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#battery-level)
- [HWID](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#hwid)
- [Lot key](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#lot-key)
- [Timestamp](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#timestamp)
- [Vendor key](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#vendor-key)

HWID、Lot key、およびVendor keyは、LINEヤフー株式会社が生成し管理するデータです。これらのパラメータを取得するには、LINEヤフー株式会社の貴社担当者までお問い合わせください。申請フォームを提出し、承認されると、パラメータが発行されます。

#### Battery level 

Battery levelとは、バッテリー残量のことです。以下の表に従って、残量を指定してください。

| 10進数値 | 16進数値 | 説明 |
| --- | --- | --- |
| 0 | 0x00 | 不明、または外部電源に接続されています。 |
| 1 | 0x01 | 残量0%。完全放電の状態です。 |
| 2 | 0x02 | 残量10% |
| … | … | … |
| 10 | 0x0A | 残量90% |
| 11 | 0x0B | 残量100%。完全充電の状態です。 |
| (12-255) | 0x0C-0xFF | 将来の利用のため予約されています。使用しないでください。 |

#### HWID 

HWIDはLINEヤフー株式会社によって発行される、ビーコン端末のハードウェアIDです。HWIDは16進数表記の10文字の文字列です。これをバイト配列に変換し、5バイトのバイナリデータとしてビーコン端末に書き込みます。また、HWIDはビーコン端末本体に表示してください。

#### Lot key 

Lot keyはLINEヤフー株式会社によって発行される、ロットごとに割り当てるキーです。Lot keyは16文字の文字列です。HWIDの場合と同様にバイト配列に変換し、8バイトのバイナリデータとしてビーコン端末に書き込みます。

#### Timestamp 

符号なし64ビット整数型のタイムスタンプです。

- ビーコン端末の電源を初めて投入した時点からインクリメントを開始します。
- 0から開始し、15秒ごとにインクリメントします。たとえば、ビーコン端末の電源を投入してから1分後のタイムスタンプは4になります。
- ビーコン端末の電源を再投入するときにタイムスタンプを0にリセットせず、電源が切れる前の時点のタイムスタンプを引き続きインクリメントしてください。
- 端末のHWIDを新たに発行されたHWIDに書き換える場合、タイムスタンプは再び0から開始するようにリセットしてください。

#### Vendor key 

Vendor keyはLINEヤフー株式会社によって発行される、製造者ごとに割り当てるキーです。Vendor keyは16進数表記の8文字の文字列です。HWIDの場合と同様にバイト配列に変換し、4バイトのバイナリデータとしてビーコン端末に書き込みます。

## iBeaconパケット 

LINE Beaconデバイスが付近にあることをiOSデバイスに通知するため、iBeaconパケットを必ず送信してください。以下のLINE Beacon特有のパラメータをiBeaconパケットに含めてください。

| パラメータ | 値                                   |
| ---------- | ------------------------------------ |
| UUID       | D0D2CE24-9EFC-11E5-82C4-1C6A7A17EF38 |
| Major      | 0x4C49                               |
| Minor      | 0x4E45                               |

iBeaconパケットのAD structureと送信間隔については、『Proximity Beacon Specification』を参照してください。このドキュメントは、[Apple DeveloperサイトのiBeaconのセクション](https://developer.apple.com/ibeacon/)からダウンロードできます。
