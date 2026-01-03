# IoTLynx

A maker-friendly ESP32-C6 development board designed for accessibility and ease of use.

![IoTLynx Board](https://github.com/halherta/IoTLynx/blob/main/images/IoTLynx_photo.jpg)

## Overview

IoTLynx is a microcontroller development board based on Espressif's ESP32-C6 microcontroller (ESP32-C6-MINI-1 module). Designed with accessibility in mind, the IoTLynx platform caters to makers, hobbyists, and newcomers to programming and electronics. Though the board supports C programming, it was specifically designed to run MicroPython—a choice that aligns with its philosophy of ease of use. With the MicroPython REPL pre-loaded and ready to run, users can start coding immediately without the hassle of configuring development environments or installing IDEs.

## Features

### Hardware Specifications

**ESP32-C6 (ESP32-C6-MINI-1) Module:**
- **Processor:** RISC-V 32-bit single-core, up to 160 MHz
- **Memory:** 512 KB SRAM, 320 KB ROM, 4 MB embedded flash
- **Wireless:** Wi-Fi 6 (802.11 b/g/n, 2.4 GHz), Bluetooth 5.3 LE
- **GPIO:** 19 programmable GPIOs available on headers
- **Interfaces:** 2× SPI, 2× UART, 1× I2C, 1× I2S
- **Analog:** 7-channel 12-bit SAR ADC
- **PWM:** 6 LED PWM channels
- **USB:** USB 2.0 full-speed (OTG)
- **Other:** Built-in temperature sensor, 7-channel capacitive touch, hardware encryption

**Board Features:**
- **Dimensions:** 58mm × 38mm with rounded edges
- **Power Options:** USB-C or +5V via pin (can use both simultaneously)
- **Voltage Regulator:** Onboard +3.3V regulator
- **Headers:** 2× 14-pin female headers for GPIO access
- **Buttons:** RESET and BOOT pushbuttons
- **LED:** Power-on indicator
- **PCB:** 2-layer design with ground fills for noise immunity
- **Mounting:** M3 mounting holes on all four corners

### Power Consumption
- **Active mode (Wi-Fi):** ~95 mA
- **Modem-sleep:** ~15 mA
- **Light-sleep:** ~3 mA
- **Deep-sleep:** ~7-10 µA

## Pinout

![IoTLynx Pinout](https://github.com/halherta/IoTLynx/blob/main/images/IoTLynx_pinout.png)

Power can be applied via:
- **USB-C connector** for programming and power
- **+5Vin pin** (5V only) - can be used simultaneously with USB-C
- **+3V3 output** available for powering external components

## Schematic & PCB

The board features a straightforward design with all ESP32-C6-MINI-1 GPIOs (except USB pins) brought out to the headers. View the [full schematic PDF](https://github.com/halherta/IoTLynx/blob/main/IoTLynx.pdf) for complete details.

![IoTLynx Schematic](https://github.com/halherta/IoTLynx/blob/main/images/IoTLynx_schematic.png)
![IoTLynx PCB Layout](https://github.com/halherta/IoTLynx/blob/main/images/IoTLynx_pcb_layout.png)
![IoTLynx 3D Render](https://github.com/halherta/IoTLynx/blob/main/images/IoTLynx_3d_layout.png)

## Expansion Boards

The IoTLynx is designed to support "Top" boards—add-on boards that attach via the two female header connectors, similar to Arduino shields or Raspberry Pi hats. A KiCad template for creating Top boards is available in the [parts library](https://github.com/halherta/mykicadlibrary).


## Getting Started

### Prerequisites

- [Thonny IDE](https://thonny.org/) (MicroPython IDE)
- [esptool](https://github.com/espressif/esptool) (Espressif's flashing tool)
- [MicroPython firmware for ESP32-C6](https://micropython.org/download/ESP32_GENERIC_C6/)

### Installation

**1. Install Thonny and esptool:**

Via pip (in a Python virtual environment):
```bash
pip install thonny esptool
```

Or via apt (Debian/Ubuntu):
```bash
sudo apt install thonny esptool
```

**2. Find your serial port:**

Linux/Mac:
```bash
ls /dev/tty*
```

Windows (PowerShell):
```powershell
[System.IO.Ports.SerialPort]::getportnames()
```

Look for something like `/dev/ttyUSB0`, `/dev/ttyACM0` (Linux/Mac) or `COM3`, `COM4` (Windows).

**3. Erase the flash:**
```bash
esptool --chip esp32c6 --port /dev/ttyUSB0 erase_flash
```
*Replace `/dev/ttyUSB0` with your actual serial port.*

**4. Flash MicroPython firmware:**
```bash
esptool --chip esp32c6 --port /dev/ttyUSB0 write_flash -z 0x0 ESP32_GENERIC_C6-XXXXXXXX.bin
```
*Replace `ESP32_GENERIC_C6-XXXXXXXX.bin` with your downloaded firmware filename.*

**5. Configure Thonny:**
- Open Thonny
- Go to **Run → Configure Interpreter**
- Select **MicroPython (ESP32)** from the first dropdown
- Select your board's serial port from the second dropdown
- Click **OK**

You should see the MicroPython REPL prompt in the shell window:
```python
MicroPython v1.xx.x on 20xx-xx-xx; ESP32C6 module with ESP32C6
Type "help()" for more information.
>>>
```

Congratulations! You're ready to program your IoTLynx board!

## Repository Contents

- **IoTLynx.kicad_\*** - KiCad project files (schematic, PCB, settings)
- **IoTLynx.pdf** - Schematic in PDF format
- **IoTLynx.svg** - Board illustration
- **production/** - Manufacturing files (gerbers, BOM, etc.)
- **images/** - Documentation images
- **\*-backups/** - KiCad backup files

## Resources

- **Blog Post:** [Detailed IoTLynx writeup](https://hussamtalkstech.com/iotlynx/)
- **Parts Library:** [KiCad parts and Top board template](https://github.com/halherta/mykicadlibrary)
- **ESP32-C6 Datasheet:** [ESP32-C6-MINI-1 documentation](https://documentation.espressif.com/esp32-c6-mini-1_mini-1u_datasheet_en.html)
- **MicroPython Documentation:** [MicroPython for ESP32](https://docs.micropython.org/en/latest/esp32/quickref.html)

## License

This hardware project is open source. Please check the repository for specific license information.

## Contributing

Contributions, issues, and feature requests are welcome! Feel free to check the issues page or submit a pull request.

## Support

For questions, issues, or discussions about the IoTLynx board:
- Open an issue on this repository
- Visit the [blog post](https://hussamtalkstech.com/iotlynx/) for additional details

## Author

Created by [halherta](https://github.com/halherta)

---

**Note:** While the ESP32-C6 supports Zigbee, Thread, 6LoWPAN, and Matter protocols, these features are not currently available through MicroPython.
