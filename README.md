# Smart Solar Battery Charger
Portable solar battery charger that works with Home Assistant

<img alt="Smart Solar Battery Charger Video Thumbnail" src="Solar%20Battery%20Charger%20Thumbnail.png">

## Sketch
<img alt="Rough Sketch" src="Solar%20Charger%20Sketch.png">

*the pinnacle of my artistic ability*

## Schematic
[<img alt="Schematic Diagram" src="schematic.png">](Schematic_Solar-Charger-(STD)_2025-09-20.pdf)

## Renogy Wanderer Interface
RS-232 Pinout
| Pin | Color  | Description   | CAT5 Color  |
|-----|--------| --------------|-------------|
|  1  | Blue   | Transmit      | Brown       |
|  2  | Green  | Receive       | Blue        |
|  3  | Grey   | Ground        | Brown/White |
|  4  | White  | Not Connected |             |
|  5  | Orange | +12 Volts     |             |
|  6  | Brown  | Not Connected |             |

Modbus Registers
| Address | Units       | Description              |
|---------|-------------|--------------------------|
| 0x100   | Percent     | Battery State of Charge  |
| 0x101   | Volts       | Battery Voltage          |
| 0x102   | Amps        | Battery Charging Amps    |
| 0x103   | Degrees (C) | Controller Temp          |
| 0x104   | Volts       | Load Voltage             |
| 0x105   | Amps        | Load Amps                |
| 0x106   | Watts       | Load Power               |
| 0x107   | Volts       | Solar Voltage            |
| 0x108   | Amps        | Solar Amps               |
| 0x109   | Watts       | Solar Power              |
| 0x120   | Integer     | Charging State           |
| 0x121   | Integer     | Error State              |
* All volts are expressed as tenths of a volt (multiply result by 0.1 to get volts)
* All amps are expressed as hundredths of an amp (multiply result by 0.01 to get amps)
* Controller Temp register (0x103) requires a bitmask of 0xFF00
* Charging State register (0x120) requires a bitmask of 0x00FF

Charging States
| Register Value | State          |
|----------------|----------------|
| 0       | Not Charging          |
| 1       | Charging              |
| 2       | Power Point Tracking  |
| 3       | Equalizing            |
| 4       | Boosting              |
| 5       | Floating              |
| 6       | Overpower             |

Error States
| Register Value | State                            |
|----------------|----------------------------------|
| 0              | Normal                           |
| 1              | Battery Over-Discharge           |
| 2              | Battery Over-Voltage             |
| 4              | Battery Under-Voltage            |
| 8              | Load Short Circuit               |
| 16             | Load Over-Power/Over-Current     |
| 32             | Controller Over-Temperature      |
| 64             | Ambient Over-Temperature         |
| 128            | Solar Over-Power                 |
| 256            | Solar Short Circuit              |
| 512            | Solar Over-Voltage               |
| 1024           | Solar Counter Current            |
| 2048           | Solar Working Point Over-Voltage |
| 4096           | Solar Reverse Connection         |
| 8192           | Anti-Reverse MOS Short Circuit   |
| 16384          | Charge MOS Short Circuit         |


[Full Renogy Modbus Protocol Document](ROVER_MODBUS.pdf)


## ESP32 Hardware and Software Configuration

Pin Usage
| Pin | Description               |  
|-----|---------------------------|
| 4   | DHT Data                  |
| 13  | Red (Charging) LED        |
| 16  | UART Receive              |
| 17  | UART Transmit             |
| 18  | Green (Charged) LED       |
| 19  | Blue (Wifi Connected) LED |
| 23  | Yellow (Error) LED)       |


[ESPHome Configuration](solar-charge-controller.yaml)

