# RTOS-Based Adaptive Heterogeneous Memory Management and Signal Processing

An embedded-systems project exploring fixed-size memory-block management, data acquisition, SPI communication, and signal processing using an Arduino Uno and ESP32.

> **Project status:** This repository is being organized for documentation and source-code upload. Update statements and checkboxes as the implementation and hardware validation evolve. Only claim features and results that are present in the code and have been tested.

## Overview

The project is designed around two microcontrollers:

- **Arduino Uno:** sensor/data acquisition, signal generation, and memory-block management.
- **ESP32:** intended peer for data exchange and further processing over SPI.

The system uses a fixed-size block abstraction to organize sample data and validate allocation, access, release, and boundary handling.

## Hardware

- Arduino Uno
- ESP32 development board
- MPU6050 inertial measurement sensor (where integrated)
- SPI wiring between the boards
- Optional 0.96-inch OLED display (if included in the current build)

Confirm the final bill of materials and wiring against the actual hardware before reproducing the project.

## Configuration

| Parameter | Value |
|---|---:|
| Number of memory blocks | 4 |
| Block size | 128 bytes |
| Sample size | 2 bytes |
| Samples per block | 64 |
| Nominal sample rate | 100 Hz |
| Test signal frequencies | 5 Hz and 15 Hz |

These are the documented configuration/test values. Verify them against the source configuration before changing the hardware setup.

## Memory-block manager

The memory manager uses a block descriptor containing metadata such as:

- Block ID
- Validity state
- Dirty state
- Access count
- Last-access information

The recorded test plan covers read/write operations, missing or invalid block rejection, duplicate allocation, full-memory handling, freeing and reusing blocks, reads from free blocks, and boundary validation. Save actual serial logs and test results under `results/` so the behavior can be independently reviewed.

## SPI protocol configuration

The project configuration notes specify:

| Field | Value |
|---|---|
| Start-of-frame marker | `0xAA` |
| Protocol version | `0x01` |
| Ping command | `0x01` |
| Read-block command | `0x02` |
| Maximum payload | `BLOCK_SIZE` (128 bytes) |

Refer to the firmware for the complete frame format, byte order, response codes, timing, and error handling. These constants alone do not define the entire protocol.

## Suggested repository layout

```text
rtos-adaptive-memory-manager/
├── README.md
├── .gitignore
├── src/
│   ├── arduino/
│   └── esp32/
├── tests/
├── docs/
└── results/
```

The documentation and test-plan files are included as scaffolding. Add source directories when the real board-specific firmware is uploaded; Git does not track empty folders.

## Build and run

1. Install the Arduino IDE.
2. Open the relevant sketch/source for each board.
3. Select the correct board and serial port.
4. Verify SPI pin assignments, common ground, voltage compatibility, and wiring for the actual boards.
5. Flash the appropriate firmware to each board.
6. Open Serial Monitor at the baud rate configured in the source and run the included tests.
7. Save representative, unedited test output in `results/`.

Board-specific setup, dependencies, pin assignments, and baud rate must be confirmed from the actual source files before reproducing the project.

## Validation checklist

- [ ] Read/write behavior
- [ ] Missing and invalid block IDs rejected
- [ ] Duplicate-allocation behavior
- [ ] Full-memory behavior
- [ ] Free and reuse behavior
- [ ] Reads from free blocks rejected
- [ ] Boundary conditions handled safely
- [ ] SPI framing and transfer behavior verified on hardware
- [ ] Signal samples and processing results documented

## Future improvements

- Document the complete SPI packet structure and response codes.
- Add circuit/wiring and architecture diagrams.
- Include reproducible tests and captured hardware test output.
- Measure transfer timing, memory usage, and signal-processing performance.
- Document task scheduling and RTOS behavior only if an RTOS scheduler/tasks are actually implemented in the code.

## Repository safety

Commit source code, diagrams, and results that you created and are permitted to share. Never commit credentials, private configuration, IDE caches, generated binaries, or confidential material.

## Author

Embedded-systems project focused on microcontrollers, memory management, communication protocols, and signal processing.
