<show-structure for="chapter" depth="2"/>

# Interface

The interface module serves as the interface between the [Acquisition](acquisition-module.md) module and the GUI

## Configuration

The device configuration is stored inside the `config.ini` file.

If the file is missing, a default one is created with the following content

```Ini
[Application]
logLevel        = error       # Set maximum log level: none, error, warning, info, debug, all
restartPeriod   = 1000        # Time between send trials in ms

[Measure]
meanWidth       = 1           # number of sample to use for the moving average

[LoRa]
address         = 00000000    # 8-digit hex number representing the LoRa address of the device. Must be unique.
bandwith        = 9           # 0: 7.8KHz, 1: 10.4KHz, 2: 15.6KHz, 3: 20.8KHz, 4: 31.2kHz, 5: 41.7KHz, 6: 62.5KHz, 7: 125KHz, 8: 250KHz, 9: 500KHz 
codingRate      = 1           # 1: 4/5, 2: 4/6, 3: 4/7, 4: 4/8
spreadingFactor = 7           # 6 to 12, the lower the faster, the higher the further 
hopPeriod       = 32          # number of symbols between each Frequency Hop, 0 disable it, [0 - 255]
```

> The address field allows the interface to differentiate devices over LoRa.
> The default value will be generated based on the MCU unique address but there is no
> guarantee that the result will be unique.
> Make sure that each of your acquisition module have a different address
> {style="warning"}

## Commands

| Name                     | Connection | Description                                       | 
|--------------------------|------------|---------------------------------------------------|
| Get Version              | false      | Get bridge current version                        |
| Get Kind                 | false      | Get device kind                                   | 
| Get Medium Configuration | false      | Return the currently selected medium              |
| Set Medium Configuration | false      | Set what medium to use                            |
| Get Configuration Field  | false      | Get a configuration field                         |
| Set Configuration Field  | false      | Set a configuration field                         | 
| Reload Configuration     | false      | Reload device configuration                       | 
| Get Time                 | false      | Return the interface module current time          |
| Sync device              | true       | Synchronize Interface and Acquisition modules     |
| Get Measure Schedule     | true       | Get current measure schedule                      |
| Set Measure Schedule     | true       | Set current measure schedule                      |
| Get Measure Progress     | true       | Fetch current progress of the measurement         |
| Get Measure Results      | true       | Fetch interface measure results                   |
| Send Command             | true       | Send directly a command to the acquisition module |
| Error                    | false      | Returned when command failed                      |

> Like other enumerations, Command ID start at 1.
> 0 is reserved as unknown

--- 

### Get version

Return the firmware version of the module.

#### Parameters {id="get-version-parameters"}

None

#### Returns {id="get-version-returns"}

- version: [Version](structures.md#version)

---

### Get Kind

#### Parameters {id="get-kind-parameters"}

None

#### Returns {id="get-kind-returns"}

- kind: [DeviceKind](enumerations.md#devicekind), always Interface.

---

### Get Medium Configuration

Fetch the current medium configuration of the module.
If not connected, the medium field in configuration will have the Unknown value (0).

#### Parameters {id="get-medium-configuration-parameters"}

None

#### Returns {id="get-medium-configuration-returns"}

- configuration: [MediumConfiguration](structures.md#mediumconfiguration).

---

### Set Medium Configuration

Change module medium configuration.

#### Parameters {id="set-medium-configuration-parameters"}

- configuration: [MediumConfiguration](structures.md#mediumconfiguration).

#### Returns {id="set-medium-configuration-returns"}

- configuration: [MediumConfiguration](structures.md#mediumconfiguration).

---

### Get Configuration Field {id="get-configuration-field"}

Fetch a field from the configuration.

#### Parameters {id="get-configuration-field-parameters"}

- section: String,
- name: String.

#### Returns {id="get-configuration-field-returns"}

- section: String,
- name: String,
- value: String, empty if non-existent.

---

### Set Configuration Field {id="set-configuration-field"}

Set a field to the configuration.

If the value is empty, the field will be removed from the configuration.

If there is no field inside a section, it will be removed from the configuration.

#### Parameters {id="set-configuration-field-parameters"}

- section : String,
- name: String,
- value: String.

#### Returns {id="set-configuration-field-returns"}

- section: String,
- name: String,
- value: String.

---

### Get Time

Fetch interface time

#### Parameters {id="get-time-parameters"}

None

#### Returns {id="get-time-returns"}

- time : [Time](alias.md#time)

---

### Sync Device

Request a synchronisation between interface and acquisition module

#### Parameters {id="sync-device-parameters"}

None

#### Returns {id="sync-device-returns"}

- interfaceTick : [Time](alias.md#time),
- acquisitionTick : [Time](alias.md#time).

---

### Get Measure Schedule

Get current measure schedule

#### Parameters {id="get-measure-schedule-parameters"}

None

#### Returns {id="get-measure-schedule-returns"}

- schedule: [MeasureSchedule](structures.md#measureschedule), the schedule of the measure.

---

### Set Measure Schedule

Update measure schedule

#### Parameters {id="set-measure-schedule-parameters"}

- schedule: [MeasureSchedule](structures.md#measureschedule).

#### Returns {id="set-measure-schedule-returns"}

- schedule: [MeasureSchedule](structures.md#measureschedule).

---

### Get Measure Progress

Request a progression report from the interface.

#### Parameters {id="get-measure-progress-parameters"}

None

#### Returns {id="get-measure-progress-returns"}

- schedule: [MeasureSchedule](structures.md#measureschedule),
- sample: [InterfaceSamples](structures.md#interfacemeasuresample), last sample from interface,
- time: [Time](alias.md#time), current time for the interface.

---

### Get Measure Results

Fetch results samples from interface module.

#### Parameters {id="get-interface-measure-result-parameters"}

- start: u32, start index for this chunk,
- length: u32, max number of sample to returns in this message.

#### Returns {id="get-interface-measure-result-returns"}

- start: u32, start index for the chunk,
- length: u32, number of samples returned in this message,
- total: u32, number of samples recorded in last acquisition,
- samples: [Interface samples](structures.md#interfacemeasuresample).

---

### Send Command

Allows to directly send any commands to the acquisition module.

#### Parameters {id="send-command-parameters"}

- id: u8, command ID,
- payload: String, representation of an Array(u8) using HEX STRING.

#### Returns {id="send-command-returns"}

- id: u8, command ID,
- payload: String, representation of an Array(u8) using HEX STRING.

---

### Restart

Request the device to restart.

Restart is not immediate, allowing the device to reply.

#### Parameters {id="restart-parameters"}

None

#### Returns {id="restart-returns"}

None

---

### Error {id="error-command"}

Returned from acquisition module when a command has failed.

#### Parameters {id="error-command-parameters"}

None

#### Returns {id="error-command-returns"}

- id: u8, the ID of the command that failed
- code: [Error](enumerations.md#error).