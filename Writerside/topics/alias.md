# Alias

An alias is a renaming of an existing type so that it is easier to understand its purpose and ease its evolution in the
code and documentation if needed.

## String

A [text container](fundamental.md#containers) like std::string in c++.

## Array(X)

A variable length [container](fundamental.md#containers) for elements of type X.

## Array(X, Y)

A fixed length [container](fundamental.md#containers) of Y elements of type X.

## Time

u32, timestamp in ms.

## Duration

u32, duration in ms.

## Address

u32, used by LoRa to discriminate the sender/receiver.

### Special values

| value        | Name      | Definition                                                                                   | 
|--------------|-----------|----------------------------------------------------------------------------------------------| 
| `0x00000000` | Invalid   | Tell when an address has not been set or is invalid. Must not be used when sending a packet. | 
| `0xFFFFFFFF` | Broadcast | When set to recipient, any device receiving this message will consider it as meant for them. |

[//]: # (Should we allows broadcast as sender address?)

[//]: # (What would happen is that when a device receive from broadcast sender, they will reply to broadcast)

[//]: # (There might be a usage for that)

## ErrorCode

| code   | description   |
|--------|---------------| 
| 0x0001 | Not Connected |
| 0xFFFF | Generic       |