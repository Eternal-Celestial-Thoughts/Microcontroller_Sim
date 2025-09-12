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

## Supported Hardware
- Raspberry Pi 5 (Debian-based)
- NVIDIA Jetson (JetPack/Ubuntu)
- Any Linux PC for simulation

## Protocols
- Message framing with length, type, and CRC-16
- Optional ack/seq-based reliability with retry/backoff
- Heartbeat and time sync messages

## Project Structure
```text
Microcontroller_Sim/
  CMakeLists.txt
  README.md
  apps/
    host/
    sim/
  src/
    core/
    devices/
    bus/
    proto/
  tests/
```

## Getting Started
### Prerequisites
- CMake >= 3.20, a C++17 compiler (gcc/clang), and Git
- On Pi/Jetson: enable and configure serial/I2C/SPI as needed

### Build
```bash
git clone <this-repo-url>
cd Microcontroller_Sim
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
```

### Run
```bash
# Run simulator with sample scenario
./build/apps/sim/sim --scenario examples/basic.yaml

# Run host app pointing at a serial device
./build/apps/host/host --port /dev/ttyACM0 --baud 115200
```

## Configuration
YAML-based scenarios define number of devices, bus types, latencies, drop rates, and protocol options.

## Examples
- examples/basic.yaml: 2 devices on a UART bus
- examples/spi_three_mcus.yaml: 3 devices on SPI with time sync

## Testing
```bash
ctest --test-dir build
```

## Performance Measurement
Export metrics (latency, throughput, loss, retries) to CSV. A Python notebook can parse CSV for plots.

## Roadmap
- CAN bus adapter
- ROS 2 bridge for Jetson
- Hardware-in-the-loop (HIL) mode

## Contributing
PRs welcome! Please run tests and clang-format before submitting.

## License
MIT

## Acknowledgments
Inspired by real-world Pi/Jetson + MCU deployments in robotics and IoT.
