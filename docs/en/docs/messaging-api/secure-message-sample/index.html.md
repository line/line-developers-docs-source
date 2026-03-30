# Sample code and data for generating secure messages

Refer to the sample data and code provided here, when you develop a function to embed in beacon devices to generate secure messages. For the algorithm information on secure message generation, see [Generate a secure message](https://developers.line.biz/en/docs/messaging-api/beacon-device-spec/#generating-secure-message).

## Sample data 

The series of tables show sample data required to generate secure messages and the resulting values when you compute the data correctly. Compare with the data provided here to see if your function for secure message generation behaves properly.

Here are the parameters we'll use to compute secure messages:

| Field         | Value            |
| ------------- | ---------------- |
| HWID          | 01deadbeef       |
| Vendor key    | 5cf2a423         |
| Lot key       | 8c194fe41d7fe34f |
| Battery level | 0x01             |

Convert the value of each HWID, vendor key, and lot key to a byte array before calculation.

### Timestamp is zero 

The timestamp value `0` means that the device is powered on for the first time.

| | |
| --- | --- |
| Input value | 000000000000000001deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | 72de7eafe33a44f0094283e03c28ff8bf85230825616fa49b73edaa6be88a0a8 |
| Message authentication code | 037cf6f1 |
| Secure message | 037cf6f1000001 |

### Timestamp is one 

The timestamp value `1` means that 15 seconds have passed since the initial power-on.

| | |
| --- | --- |
| Input value | 000000000000000101deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | eba4633c394cf7d913a863f25e930e7b8d9227bd109c2019d9dfbb411366cc4f |
| Message authentication code | c86489c6 |
| Secure message | c86489c6000101 |

### Timestamp is 65535 

If the timestamp value is incremented from `65535` to `65536`, the masked timestamp in the secure message is reset to `0000`. See also the [Timestamp is 65536](https://developers.line.biz/en/docs/messaging-api/secure-message-sample/#timestamp-is-65536) section and check that the masked timestamp changes from `ffff` to `0000`.

| | |
| --- | --- |
| Input value | 000000000000ffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | f435f408d2978130607a8af69da2e6f65b66c260796f03ce2a7daf9b468ae0b5 |
| Message authentication code | 958497b8 |
| Secure message | 958497b8ffff01 |

### Timestamp is 65536 

When the timestamp value is incremented to `65536`, the masked timestamp in the secure message is reset to `0000`. See also the [Timestamp is 65535](https://developers.line.biz/en/docs/messaging-api/secure-message-sample/#timestamp-is-65535) section and check that the masked timestamp changes from `ffff` to `0000`.

| | |
| --- | --- |
| Input value | 000000000001000001deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | 70b58ab690b63d519caf37359ce3d910e8e1d79a90f095462ee2d56ae0f035e4 |
| Message authentication code | 564cfb90 |
| Secure message | 564cfb90000001 |

### Timestamp is 9223372036854775807 

The value `9223372036854775807` is the maximum value of a signed 64-bit integer.

| | |
| --- | --- |
| Input value | 7fffffffffffffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | c626232a199b163c53ba70f4d493c8b34891532d9e8fbf2b788e7e1cf3d13dec |
| Message authentication code | 05d522a7 |
| Secure message | 05d522a7ffff01 |

### Timestamp is 18446744073709551615 

The value `18446744073709551615` is the maximum value of an unsigned 64-bit integer.

| | |
| --- | --- |
| Input value | ffffffffffffffff01deadbeef5cf2a4238c194fe41d7fe34f01 |
| SHA-256 hash value | 53ab6c6874fc333398ae2186eb45ce5d5a77d10cd2d3fe3d933a12b33cb13090 |
| Message authentication code | 7393bd92 |
| Secure message | 7393bd92ffff01 |

## Sample code 

This sample Java code generates a secure message.

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

This sample code tests the code above, that generates a secure message, with the data from the [sample data](https://developers.line.biz/en/docs/messaging-api/secure-message-sample/#sample-data) section.

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
