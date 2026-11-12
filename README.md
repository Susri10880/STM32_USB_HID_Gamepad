# STM32 USB HID Gamepad Controller

A custom USB HID gamepad built using the **STM32F407VG Discovery Board** and STM32 HAL. The controller reads two physical analog joysticks and two push buttons, then sends their inputs to a PC over USB.

The controller has been successfully tested on Windows and works with the **FreeRider drone simulator**.

## Features

- Four analog joystick axes.
- Two physical push buttons.
- USB HID Gamepad implementation.
- 12-bit ADC readings (0–4095).
- Custom HID report descriptor.
- 9-byte USB input report.
- STM32 HAL-based firmware.

## Hardware

| Component | Description |
|---|---|
| Microcontroller | STM32F407VG |
| Development board | STM32F4 Discovery |
| Joysticks | 2 × Analog joysticks |
| Push buttons | 2 × Physical switches |
| USB interface | USB OTG FS |

## Pin Configuration

| Function | STM32 Pin | ADC Channel |
|---|---|---|
| Joystick 1 X | PA1 | ADC1 Channel 1 |
| Joystick 1 Y | PA2 | ADC1 Channel 2 |
| Joystick 2 X | PB0 | ADC1 Channel 8 |
| Joystick 2 Y | PB1 | ADC1 Channel 9 |
| Switch 1 | PE6 | GPIO Input |
| Switch 2 | PC5 | GPIO Input |

## How It Works

1. ADC1 reads the four analog joystick axes.
2. GPIO reads the two physical switches.
3. The firmware packs the readings into a 9-byte HID input report.
4. The STM32 sends the report to the PC through USB.
5. Windows recognises the STM32 as a game controller.

## HID Report Format

| Byte(s) | Data |
|---|---|
| 0–1 | Joystick 1 X |
| 2–3 | Joystick 1 Y |
| 4–5 | Joystick 2 X |
| 6–7 | Joystick 2 Y |
| 8 | Two buttons and six padding bits |

Each analog axis is represented using a 16-bit field. The ADC readings are 12-bit values, ranging from 0 to 4095.

## USB Connection

- **CN1:** ST-LINK connection for programming and debugging.
- **CN5:** USB OTG FS connection for gamepad communication with the PC.

## Software and Tools

- STM32CubeIDE
- STM32CubeMX (integrated)
- STM32 HAL
- USB Device Middleware
- Git and GitHub
- Windows Game Controllers (`joy.cpl`)
- FreeRider Drone Simulator

## Testing

The controller has been tested using:

- Windows Game Controllers control panel (`joy.cpl`).
- FreeRider drone simulator.

## Future Improvements

- USB HID keyboard interface for keyboard shortcuts.
- Configurable joystick deadzone and calibration.
- Button debouncing.
- Improved USB transmission and ADC error handling.
- PC-side application launching support.

## Project Status

**Version 1.0 – USB HID Gamepad**

Core joystick and button functionality implemented and tested successfully.

---

Built as an embedded systems learning project using STM32 HAL.