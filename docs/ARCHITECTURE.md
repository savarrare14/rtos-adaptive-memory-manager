# Architecture Notes

## Intended high-level data path

```text
MPU6050 / test-signal source
          |
          v
Arduino Uno
  - data acquisition / sample generation
  - fixed-size block manager
  - block validation tests
          |
          | SPI (protocol configuration in source)
          v
ESP32
  - receive / further processing (confirm against implementation)
```

This is a high-level project summary. Confirm the final division of responsibilities, signal path, and implemented ESP32 features against the source code before treating this as an as-built diagram.

## Recorded configuration

- Memory blocks: 4
- Block size: 128 bytes
- Sample size: 2 bytes
- Samples per block: 64
- Nominal signal sample rate: 100 Hz
- Test frequencies: 5 Hz and 15 Hz
- SPI start-of-frame marker: 0xAA
- Protocol version: 0x01
- Ping command: 0x01
- Read-block command: 0x02

## Hardware documentation to add

- Board model and revision for each microcontroller
- Exact SPI pin mapping for both boards
- Common ground and logic-level compatibility
- Sensor wiring and power requirements
- OLED pin mapping, if used
- Packet/frame diagram including lengths, IDs, byte order, and error responses

Do not infer electrical connections from the conceptual diagram. Record and verify the actual wiring.
