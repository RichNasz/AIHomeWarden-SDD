# WHAT-Documentation.md — Project Catalog and Documentation Content

## Project Identity

- **Name**: AIHomeWarden-SDD
- **Tagline**: AI-spec-driven ESP32-C6/C5 security panel replacement
- **Description**: AIHomeWarden-SDD is an open-source, spec-driven firmware project that replaces
  legacy wired security panels with an ESP32-C6 (primary) or ESP32-C5 (fallback) controller.
  All firmware and documentation are generated from `specs/` using Spec-Driven Development (SDD),
  ensuring every change is traceable to a written requirement. The system operates fully locally —
  no cloud dependency — and is designed for predictive and generative AI extension on live sensor
  data.

## Feature Bullets

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

## Component Catalog

Planned components under `components/` (one component per spec):

| Component | Purpose |
| --- | --- |
| `eol_supervisor` | EOL resistor zone state machine (open/closed/tamper/short) |
| `matter_bridge` | Matter-over-Thread device bridge with Wi-Fi fallback |
| `mqtt_robot_presence` | MQTT subscriber for robot presence suppression |
| `ble_robot_presence` | BLE scanner for robot presence suppression |
| `alarm_logic` | Central alarm state machine (armed/disarmed/triggered/suppressed) |
| `ai_sensor_pipeline` | Sensor data pipeline for future predictive AI inference |

## Spec Subfolder Index

| Subfolder | Contents |
| --- | --- |
| `specs/core/` | Core system specs (documentation, architecture, alarm logic) |
| `specs/hardware/` | Hardware-related specs (GPIO assignments, EOL circuit, power) |
| `specs/security/` | Security specs (EOL supervision, tamper detection, zone hardening) |
| `specs/integration/` | Integration specs (Matter, MQTT, BLE, SmartThings, Apple Home) |
| `specs/robotics/` | Robotics specs (robot presence protocols, suppression logic) |
| `specs/skills/` | Skills specs (skill definitions and workflow descriptions) |

## Board Targets

| Role | Board | Chip | Board Spec |
| --- | --- | --- | --- |
| Primary | Seeed XIAO ESP32-C6 | ESP32-C6 | `board-specs/seeed/xiao-esp32c6.md` |
| Fallback | Seeed XIAO ESP32-C5 | ESP32-C5 | `board-specs/seeed/xiao-esp32c5.md` |

Key hardware facts for documentation:
- ESP32-C6: ADC1-only (no ADC2 conflict with Wi-Fi), Thread/Zigbee (802.15.4), Wi-Fi 6
- Both boards: 4 MB flash, no PSRAM, XIAO form factor (21 × 17.8 mm)
- Deep sleep: ~15 µA (C6), suitable for battery-backed alarm controller

## Skills Catalog

| Skill name | Purpose |
| --- | --- |
| `aihomewarden-documentation-generator` | Generates README.md, CONTRIBUTING.md, community files, and all docs/ READMEs from WHAT-/HOW- specs |

Future skills (to be defined in `specs/skills/`):
- `aihomewarden-component-generator` — Generates a new ESP-IDF component scaffold from a spec pair
- `aihomewarden-board-spec-generator` — Generates board-specs/ entries from vendor documentation
