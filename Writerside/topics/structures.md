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

Each axis is given in degrees.

- x: i16 ([-179, 179]),
- y: i16 ([-89, 89]),
- z: i16 ([-179, 179]).

## AcquisitionMeasureSample

- itTick: [Time](alias.md#time), time when the sample was stored,
- adcTick: [Time](alias.md#time), time when ADC produced sample,
- gauges: [Array(float, 4)](alias.md#array-x-y), voltage measured by the gauges in volt,
- orientation: [Orientation](#orientation),
- temperature: float, voltage measured by the temperature sensor.

## InterfaceMeasureSample

- itTick: [Time](alias.md#time), time when the sample was stored,
- adcTick: [Time](alias.md#time), time when ADC produced sample,
- drill: float, voltage measured.

## MediumConfiguration

- medium: [CommunicationMedium](enumerations.md#communicationmedium),
- address: [Address](alias.md#address), recipient address if medium is LoRa.

## GaugeCalibration

- balanced: u32,
- unbalanced: u32.

## AcquisitionCalibration

- time: [Time](alias.md#time), time of the calibration,
- gauge: Array([GaugeCalibration](#gaugecalibration), 4), gauge calibrations.

## AcquisitionPost

- passed: bool,
- battery: Error,
- power: Error,
- lora: Error,
- can: Error.
