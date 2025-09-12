# Microcontroller_Sim

## Overview
Simulates communication between a host computer (Raspberry Pi 5 or NVIDIA Jetson) and multiple microcontrollers. Useful for prototyping distributed embedded systems, validating protocols, and measuring reliability/performance without needing all target hardware online.

## Features
- Multiple virtual microcontrollers with pluggable behavior
- Host-side I/O abstraction for Pi 5/Jetson (serial, SPI, I2C, TCP)
- Protocol layers: framing, CRC, ack/retry, heartbeat, time sync
- Fault injection (packet loss, delay, jitter, bit flips, resets)
- Deterministic and real-time simulation modes
- Logging and metrics export (CSV)
- Cross-platform C++17 build with CMake

## Architecture
- Core: event loop, scheduler, bus simulator
- Devices: microcontroller models (state machines) and drivers
- Buses: UART, SPI, I2C, and network transport adapters
- Protocols: lightweight message framing with reliability extensions
- Tools: CLI harness for runs, log parser, metrics calculator

## Components
- src/core: simulation kernel and timing
- src/devices: MCU models and behaviors
- src/bus: UART/SPI/I2C/TCP adapters
- src/proto: framing, CRC, reliability
- apps/host: host controller app (Pi/Jetson)
- apps/sim: simulator CLI to run scenarios
- tests: unit and integration tests



## License
MIT

## Acknowledgments
Inspired by real-world Pi/Jetson + MCU deployments in robotics and IoT.
