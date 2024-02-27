<show-structure for="chapter" depth="2"/>

# LoRa

LoRa is a communication medium used for communication between the Bridge and the Acquisition modules.

Due to LoRa being a connection-less medium, we append a header to our packets in order to know the sender and receiver.
The full packet structure is describe by the [LoRaPacket](structures.md#lorapacket) structure
