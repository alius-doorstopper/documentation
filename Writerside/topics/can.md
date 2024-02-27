<show-structure for="chapter" depth="2"/>

# CAN

A CAN BUS is used to communicate between the interface and acquisition modules.

## Multi-Packet protocol

Due to the can bus being able to send only 8 bytes of data per frame, we designed a custom protocol allowing to send
longer packet. It allows to automatically deconstruct a packet into chunk of up to 8 bytes, then reconstruct it to its
initial size and order.

The protocol allows payloads of up to 8KB and 16 concurrent packets.

The source code can be found on
this [gitlab repository](https://gitlab.com/conception-electronique-prive/doorstopper/modules/services/can)


### Header
We put the header inside the ID of the can frame. Currently, we only use Extended ID.

Bytes 0 to 3 are used to discriminate the kind of the frame. There is currently only one kind of frame, which is a
chunk-carrier whose value is 4.

Bytes 4 to 7 are for the message nonce. This allows to handle the reception of multiple packet at the same time.

Byte 8 is a nonce-discriminator. It is expected to alternate its value between each message of the same nonce. This
allows the recipient of a message to know if its current nonce message is outdated and incomplete.

Bytes 9 to 18 tells the number of chunk the packet have.

Bytes 19 to 28 tells the index of the current chunk in the packet.

> length and index are little-endian
> {style="note"}

![chunk-carrier packet header](can_header.drawio.png)




