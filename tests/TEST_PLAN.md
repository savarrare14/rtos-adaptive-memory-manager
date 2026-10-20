# Memory Manager Test Plan

Use this checklist to record the behavior of the actual firmware. Mark a test as PASS only after running it and keeping an associated log or observation.

| Test | Expected behavior | Status | Evidence |
|---|---|---|---|
| Read/write | Valid allocated block can be written and read correctly | Not recorded here | Add log |
| Missing block | Request for a missing block is rejected safely | Not recorded here | Add log |
| Duplicate allocation | Duplicate allocation follows the documented policy | Not recorded here | Add log |
| Full memory | Allocation when all blocks are occupied is handled safely | Not recorded here | Add log |
| Free and reuse | Freed block can be reused according to policy | Not recorded here | Add log |
| Read free block | Reads from a free block are rejected | Not recorded here | Add log |
| Invalid block ID | Out-of-range or invalid IDs are rejected | Not recorded here | Add log |
| Boundary validation | Oversized or out-of-range access is rejected without corruption | Not recorded here | Add log |
| SPI frame | Start marker, version, command, length, and payload are parsed correctly | Not recorded here | Add logic-analyzer/serial evidence |
| Signal samples | Sampling rate and signal frequencies match intended configuration | Not recorded here | Add measured result |

## Reproducibility details

For every run, record:

- Firmware commit or version
- Board models and wiring
- Arduino IDE/core version and libraries
- Test procedure and expected output
- Actual serial output or measurement
- Any known limitation

Replace the status field with PASS, FAIL, or NOT RUN only after testing.
