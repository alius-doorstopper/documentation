# Enumerations

> For each enumeration, the value 0 is always used as an unknown/invalid value

## DeviceKind

Used by the [GUI](gui.md) to know to what device it is communicating with as they do not share the sames commands

1. Laboratory,
2. Interface,
3. Acquisition.

## ProbeConnectionState

Report the probe connection state of an [acquisition module](acquisition-module.md)

1. Disconnected,
2. Connected,
3. Error.

## AcquisitionMode

Tell the mode of the [acquisition module](acquisition-module.md)

1. Init,
2. LowPower,
3. Idle,
4. Measure,
5. Error.

## MeasureState

1. Running,
2. Complete.

## CommunicationMedium

Tell what medium is used or was used for a command.  
Used by the GUI to tell the interface module what medium to use.  
Used by the Acquisition module to known on what medium to answer.

1. LoRa,
2. CAN.

## BridgeSendResult

1. Success,
2. Failure.

## VersionKind

1. alpha,
2. beta,
3. release-candidate,
4. release.

## Error

Special kind of enumeration, items are not in sequential order to separate them into groups.

First byte is for the group, second byte is for the description.

`0000` and `FFFF` are special values that do not belong to a group.

| hex  | group         | description        |
|------|---------------|--------------------|
| 0000 | ALL           | Unknown            |
| 0001 | NONE          | Undocumented       |
| 0002 | NONE          | Unimplemented      |
| 0101 | HAL           | Error              | 
| 0102 | HAL           | Busy               | 
| 0103 | HAL           | Timeout            | 
| 0201 | LORA          | Invalid Version    |
| 0301 | COMMAND       | Ill Sized Data     |
| 0302 | COMMAND       | Invalid Command Id |
| 0303 | COMMAND       | Parsing Failed     |
| 0401 | CONFIGURATION | Invalid Section    |
| 0402 | CONFIGURATION | Invalid Field      |
| 0403 | CONFIGURATION | Invalid Value      |
| FFFF | ALL           | None               |