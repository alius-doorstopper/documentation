# Structures

## Version

- major: u8,
- minor: u8,
- patch: u8,
- kind: [VersionKind](enumerations.md#versionkind)
- affix: u8

## LoRaPacket

- recipient: [Address](alias.md#address), address of the target,
- sender: [Address](alias.md#address), address of the sender,
- payload: [Array(u8)](alias.md#array-x), content of the message. might be empty.

## DiscoveredDevice

- name: [String](alias.md#string),
- address: [Address](alias.md#address), Unique address of the device,
- can: bool, tell if it was possible to reach the device through can medium
- lora: bool, tell if it was possible to reach the device through lora medium
- rssi: u8, if medium include lora
- lastSeen: [Time](alias.md#time), when the device was last seen

## AcquisitionModuleState

- name: [String](alias.md#string),
- address: u32, Unique address of the device,
- can: bool, tell if the device is reachable through can medium,
- lora: bool, tell if the device is reachable through lora medium,
- lastRssi: u8, rssi of the last lora message,
- acquisition_state: [AcquisitionMode](enumerations.md#acquisitionmode),

## AcquisitionModuleStatus

- error: u8,
- battery: u8,
-

## MeasureSchedule

- time: [Time](alias.md#time), when the measure must start,
- duration: [Duration](alias.md#duration), duration of the measure.

## Orientation

- yaw: u32,
- pitch: u32,
- roll: u32.

## AcquisitionMeasureSample

- tick: [Time](alias.md#time), time when the sample was stored,
- gauges: [Array(u32, 4)](alias.md#array-x-y), voltage measured by the gauges in volt,
- orientation: [Orientation](#orientation),
- temperature: u32, voltage measured by the temperature sensor.

## InterfaceMeasureSample

- tick: [Time](alias.md#time), time when the sample was stored,
- drill: u32, voltage measured.

## MediumConfiguration

- medium: [CommunicationMedium](enumerations.md#communicationmedium),
- address: [Address](alias.md#address), recipient address if medium is LoRa.

## AcquisitionPost

- passed: bool,
- battery: Error,
- power: Error,
- lora: Error,
- can: Error.