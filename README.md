<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# AIHomeWarden-SDD

*AI-spec-driven ESP32-C6/C5 security panel replacement*

AIHomeWarden-SDD is an open-source, spec-driven firmware project that replaces legacy wired
security panels with an ESP32-C6 (primary) or ESP32-C5 (fallback) controller. All firmware and
documentation are generated from `specs/` using Spec-Driven Development (SDD), ensuring every
change is traceable to a written requirement. The system operates fully locally — no cloud
dependency — and is designed for predictive and generative AI extension on live sensor data.

![ESP-IDF](https://img.shields.io/badge/ESP--IDF-v5.x-blue)
![ESP32-C6](https://img.shields.io/badge/target-ESP32--C6-green)
![Matter](https://img.shields.io/badge/protocol-Matter%20over%20Thread-purple)
![Built with Claude Code](https://img.shields.io/badge/built%20with-Claude%20Code-orange)

---

## Table of Contents

- [Features](#features)
- [Quick Start](#quick-start)
- [Prerequisites](#prerequisites)
- [Component Table](#component-table)
- [Spec Index](#spec-index)
- [Skills](#skills)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **EOL Zone Supervision**: Reuses existing wired zones with End-of-Line resistor supervision
  (open / closed / tamper / short detection), preserving legacy sensor investments
- **Matter-over-Thread Bridge**: Native Thread radio on ESP32-C6 enables Matter device
  commissioning into SmartThings V2 and Apple Home, with Wi-Fi fallback
- **MQTT + BLE Robot Integration**: Receives robot presence announcements over MQTT and BLE
  to suppress false motion alarms when known robots are operating
- **Local-Only Operation**: No cloud API calls at runtime; all logic executes on-device
- **Predictive / Generative AI Vision**: Architecture is AI-extension-ready for on-device
  anomaly detection and generative alert summarization on sensor data streams
- **Spec-Driven Development**: Every generated file is traceable to a `specs/` file —
  no hand-edited firmware or documentation

---

## Quick Start

### Prerequisites

- [ESP-IDF v5.x](https://docs.espressif.com/projects/esp-idf/en/stable/esp32c6/get-started/)
  installed and `$IDF_PATH` set in your shell
- Python 3.8+ (bundled with ESP-IDF installer)
- USB-C cable connected to the XIAO ESP32-C6

### Build and flash (ESP32-C6)

```bash
# 1. Set target
idf.py set-target esp32c6

# 2. (Optional) Review or adjust config
idf.py menuconfig

# 3. Build
idf.py build

# 4. Flash and open serial monitor
idf.py flash monitor
```

Expected monitor output:

```
I (xxx) AIHomeWarden: AIHomeWarden starting
```

### Switching to ESP32-C5 (fallback)

Replace `esp32c6` with `esp32c5` in the `idf.py set-target` command above and rebuild.

> **Note**: Ensure `CONFIG_ESP_CONSOLE_USB_SERIAL_JTAG=y` is set in `sdkconfig.defaults`
> for serial output over USB-C. Without this, `idf.py monitor` produces no output.

---

## Component Table

| Component | Purpose |
| --- | --- |
| `eol_supervisor` | EOL resistor zone state machine (open/closed/tamper/short) |
| `matter_bridge` | Matter-over-Thread device bridge with Wi-Fi fallback |
| `mqtt_robot_presence` | MQTT subscriber for robot presence suppression |
| `ble_robot_presence` | BLE scanner for robot presence suppression |
| `alarm_logic` | Central alarm state machine (armed/disarmed/triggered/suppressed) |
| `ai_sensor_pipeline` | Sensor data pipeline for future predictive AI inference |

---

## Spec Index

All code and documentation are generated from `specs/`. Humans only ever edit files in
`specs/` and `shared-specs/` — never in generated output.

| Subfolder | Contents |
| --- | --- |
| `specs/core/` | Core system specs (documentation, architecture, alarm logic) |
| `specs/hardware/` | Hardware-related specs (GPIO assignments, EOL circuit, power) |
| `specs/security/` | Security specs (EOL supervision, tamper detection, zone hardening) |
| `specs/integration/` | Integration specs (Matter, MQTT, BLE, SmartThings, Apple Home) |
| `specs/robotics/` | Robotics specs (robot presence protocols, suppression logic) |
| `specs/skills/` | Skills specs (skill definitions and workflow descriptions) |

---

## Skills

Agent-invocable skills drive repeatable generation tasks. See [`skills/README.md`](skills/README.md)
for full details.

| Skill | Purpose |
| --- | --- |
| `aihomewarden-documentation-generator` | Generates README.md, CONTRIBUTING.md, community files, and all docs/ READMEs from WHAT-/HOW- specs |

---

## Documentation

Extended documentation lives in [`docs/`](docs/README.md):

| Section | Contents |
| --- | --- |
| `docs/guides/` | Goal-oriented guides combining multiple how-tos |
| `docs/reference/` | API, component interface, and configuration reference |
| `docs/tutorials/` | Learning-oriented step-by-step walkthroughs |
| `docs/how-to/` | Problem-oriented recipes (e.g., "How to add a new zone") |
| `docs/explanation/` | Background concepts (EOL theory, Matter pairing, etc.) |

Board hardware facts are in [`board-specs/`](board-specs/README.md). Project-wide generation
rules and institutional memory are in [`shared-specs/`](shared-specs/README.md).

---

## Contributing

Contributions are welcome. Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) before opening a
pull request — all changes start with a spec edit, never with generated code.

---

## License

Apache 2.0 — see `LICENSE` (TBD: license file to be added).

---

*All code and docs are generated from `specs/` following Spec-Driven Development (SDD).*
