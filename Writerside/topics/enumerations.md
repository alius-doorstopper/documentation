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

1. Idle,
2. LowPower,
3. Measure,
4. Error.

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
