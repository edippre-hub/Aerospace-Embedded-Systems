# System Requirements (demonstration baseline)

|   ID    |                 Requirement                         | Verification |
|---------|-----------------------------------------------------|--------------|
| SYS-001 | Evaluate temperature and vibration samples          | Unit tests |
| SYS-002 | Identify warning and critical thresholds            | Boundary tests |
| SYS-003 | Detect unavailable or invalid sensor data           | Fault-injection tests |
| SYS-004 | Preserve sample sequence in health report           | Unit test |
| SYS-005 | Support Linux host build                            | CMake build |
| SYS-006 | Provide periodic RTOS acquisition task              | FreeRTOS target review/build |
| SYS-007 | Transfer samples between RTOS tasks through a queue | RTOS integration test on target |

Thresholds are illustrative values for this portfolio simulation, not certified aircraft limits.

