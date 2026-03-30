# Secure message生成のサンプルデータとコード

このトピックでは、ビーコン端末に組み込むSecure message生成機能の開発中に利用できる、サンプルのデータとコードについて説明します。Secure message生成のアルゴリズムについては、「[Secure messageを生成する](https://developers.line.biz/ja/docs/messaging-api/beacon-device-spec/#generating-secure-message)」を参照してください。

## サンプルデータ 

一連の表は、Secure messageの生成に必要なデータのサンプルと、そのデータを正しく計算した結果の値を示しています。ここで提供されているデータと比較して、Secure message生成機能が正しく動作しているかどうかを確認してください。

以下は、Secure messageの計算に使用するパラメータです。

| フィールド    | 値               |
| ------------- | ---------------- |
| HWID          | 01deadbeef       |
| Vendor key    | 5cf2a423         |
| Lot key       | 8c194fe41d7fe34f |
| Battery level | 0x01             |

HWID、Vendor key、およびLot keyは、バイト配列に変換してから計算します。

### Timestampが0の場合 

Timestampの値が`0`とは、端末に初めて電源が入ったことを意味します。

| | |
| --- | --- |
| 入力値 | 000000000000000001deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | 72de7eafe33a44f0094283e03c28ff8bf85230825616fa49b73edaa6be88a0a8 |
| Message authentication code | 037cf6f1 |
| Secure message | 037cf6f1000001 |

### Timestampが1の場合 

Timestampの値が`1`とは、最初に電源を入れてから15秒経過したことを意味します。

| | |
| --- | --- |
| 入力値 | 000000000000000101deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | eba4633c394cf7d913a863f25e930e7b8d9227bd109c2019d9dfbb411366cc4f |
| Message authentication code | c86489c6 |
| Secure message | c86489c6000101 |

### Timestampが65535の場合 

Timestampの値が`65535`から`65536`にインクリメントされると、Secure messageのMasked timestampは`0000`にリセットされます。「[Timestampが65536の場合](https://developers.line.biz/ja/docs/messaging-api/secure-message-sample/#timestamp-is-65536)」セクションも合わせて参照し、Masked timestampが`ffff`から`0000`になることを確認してください。

| | |
| --- | --- |
| 入力値 | 000000000000ffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | f435f408d2978130607a8af69da2e6f65b66c260796f03ce2a7daf9b468ae0b5 |
| Message authentication code | 958497b8 |
| Secure message | 958497b8ffff01 |

### Timestampが65536の場合 

Timestampの値が`65536`にインクリメントされると、Secure messageのMasked timestampは`0000`にリセットされます。「[Timestampが65535の場合](https://developers.line.biz/ja/docs/messaging-api/secure-message-sample/#timestamp-is-65535)」セクションも合わせて参照し、Masked timestampが`ffff`から`0000`になることを確認してください。

| | |
| --- | --- |
| 入力値 | 000000000001000001deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | 70b58ab690b63d519caf37359ce3d910e8e1d79a90f095462ee2d56ae0f035e4 |
| Message authentication code | 564cfb90 |
| Secure message | 564cfb90000001 |

### Timestampが9223372036854775807の場合 

`9223372036854775807`は、符号付き64ビット整数型で格納できる最大値です。

| | |
| --- | --- |
| 入力値 | 7fffffffffffffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | c626232a199b163c53ba70f4d493c8b34891532d9e8fbf2b788e7e1cf3d13dec |
| Message authentication code | 05d522a7 |
| Secure message | 05d522a7ffff01 |

### Timestampが18446744073709551615の場合 

`18446744073709551615`は、符号なし64ビット整数型で格納できる最大値です。

| | |
| --- | --- |
| 入力値 | ffffffffffffffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256ハッシュ値 | 53ab6c6874fc333398ae2186eb45ce5d5a77d10cd2d3fe3d933a12b33cb13090 |
| Message authentication code | 7393bd92 |
| Secure message | 7393bd92ffff01 |

## サンプルコード 

以下は、Secure messageを生成するJavaのサンプルコードです。

```java
import java.nio.ByteBuffer;
import java.nio.ByteOrder;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
import java.util.Arrays;

import javax.xml.bind.DatatypeConverter;

public class LineBeacon {

    private static byte[] sha256(byte[] input) {
        try {
            return MessageDigest.getInstance("SHA-256").digest(input);
        } catch (NoSuchAlgorithmException e) {
            throw new IllegalStateException("SHA-256 is always supported in Java7+", e);
        }
    }

    private static byte[] xor(byte[] input, int xorCount) {
        if (xorCount == 0) {
            return input;
        }

        byte[] latterHalf = Arrays.copyOfRange(input, input.length / 2, input.length);
        for (int i = 0; i < latterHalf.length; i++) {
            latterHalf[i] ^= input[i];
        }
        return xor(latterHalf, xorCount - 1);
    }

    private static byte[] concat(byte[]...inputs) {
        int size = 0;
        for (byte[] in: inputs) {
            size += in .length;
        }
        ByteBuffer bb = ByteBuffer.allocate(size);
        for (byte[] in: inputs) {
            bb.put( in );
        }
        return bb.array();
    }

    public static byte[] createSecureMessage(long timestamp, byte[] hwid, byte[] vendorKey, byte[] lotKey, byte batteryLevel) {
        if (hwid.length != 5) {
            throw new IllegalArgumentException("HWID must be 5 bytes long. " + hwid.length);
        }
        if (vendorKey.length != 4) {
            throw new IllegalArgumentException("Vendor key must be 4 bytes long. " + vendorKey.length);
        }
        if (lotKey.length != 8) {
            throw new IllegalArgumentException("Lot key must be 8 bytes long. " + lotKey.length);
        }
        if (batteryLevel < 0x00 || 0x0b < batteryLevel) {
            throw new IllegalArgumentException("Battery Level must be between 0x00 and 0x0b: " + batteryLevel);
        }

        byte[] rawTimestamp = ByteBuffer
            .allocate(8) // Timestamp of LINE Beacon is always 8 bytes long.
            .order(ByteOrder.BIG_ENDIAN) // LINE Beacon always uses big-endian.
            .putLong(timestamp)
            .array();
        byte[] input = concat(rawTimestamp, hwid, vendorKey, lotKey, new byte[] {
            batteryLevel
        });
        byte[] digest = sha256(input);
        byte[] messageAuthenticationCode = xor(digest, 3);
        byte[] secureMessage = ByteBuffer
            .allocate(7) // Current secureMessage is always 7 bytes long.
            .put(messageAuthenticationCode)
            .put(rawTimestamp, 6, 2) // Mask the upper 6 bytes of the timestamp.
            .put(batteryLevel)
            .array();

        System.out.printf("%20s\t%s\t%s\t%s\t%s\n",
            Long.toUnsignedString(timestamp),
            DatatypeConverter.printHexBinary(secureMessage),
            DatatypeConverter.printHexBinary(input),
            DatatypeConverter.printHexBinary(digest),
            DatatypeConverter.printHexBinary(messageAuthenticationCode)
        );
        return secureMessage;
    }
}
```

以下は、「[サンプルデータ](https://developers.line.biz/ja/docs/messaging-api/secure-message-sample/#sample-data)」セクションのデータを使って、上記のSecure message生成コードをテストするサンプルコードです。

```java
import org.junit.Test;

import static org.junit.Assert.*;

import javax.xml.bind.DatatypeConverter;

public class LineBeaconTest {
    @Test
    public void testSecureMessage() {
        byte[] HWID_01deadbeef = DatatypeConverter.parseHexBinary("01deadbeef");
        byte[] VENDOR_KEY_5cf2a423 = DatatypeConverter.parseHexBinary("5cf2a423");
        byte[] LOTKEY_8c194fe41d7fe34f = DatatypeConverter.parseHexBinary("8c194fe41d7fe34f");
        byte BATTEY_LEVEL_0x01 = 0x01;

        assertArrayEquals(
            "initial timestamp",
            DatatypeConverter.parseHexBinary("037cf6f1000001"),
            LineBeacon.createSecureMessage(
                0,
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
        assertArrayEquals(
            "timestamp after 15 sec",
            DatatypeConverter.parseHexBinary("c86489c6000101"),
            LineBeacon.createSecureMessage(
                1,
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
        assertArrayEquals(
            "timestamp as UNSIGNED_SHORT_MAX_VALUE",
            DatatypeConverter.parseHexBinary("958497b8ffff01"),
            LineBeacon.createSecureMessage(
                0xffff,
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
        assertArrayEquals(
            "carry-over test",
            DatatypeConverter.parseHexBinary("564cfb90000001"),
            LineBeacon.createSecureMessage(
                0x0001 _0000,
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
        assertArrayEquals(
            "timestamp as SIGNED_LONG_MAX_VALUE",
            DatatypeConverter.parseHexBinary("05d522a7ffff01"),
            LineBeacon.createSecureMessage(
                9223372036854775807 L,
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
        assertArrayEquals(
            "timestamp as UNSIGNED_LONG_MAX_VALUE",
            DatatypeConverter.parseHexBinary("7393bd92ffff01"),
            LineBeacon.createSecureMessage(
                Long.parseUnsignedLong("ffffffffffffffff", 16),
                HWID_01deadbeef,
                VENDOR_KEY_5cf2a423,
                LOTKEY_8c194fe41d7fe34f,
                BATTEY_LEVEL_0x01

            )
        );
    }
}
```
