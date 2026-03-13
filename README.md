# AIHomeWarden-SDD

AI-spec-driven ESP32-C6/C5 security panel replacement.

- Reuses legacy wired zones with EOL supervision
- Matter-over-Thread bridge (fallback Wi-Fi) for SmartThings V2 and Apple Home
- Local robot presence announcement (MQTT/BLE) to suppress false alarms
- Future-ready for predictive/generative AI on sensor data

All code and docs are generated from `specs/` following Spec-Driven Development (SDD).
See `CLAUDE.md` for project rules.

---

## Quick Start

### Prerequisites

- [ESP-IDF v5.x](https://docs.espressif.com/projects/esp-idf/en/stable/esp32c6/get-started/)
  installed and `$IDF_PATH` set in your shell.

### Build & Flash (ESP32-C6)

```bash
# 1. Set target
idf.py set-target esp32c6

# 2. (Optional) Review / adjust config
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

---

## Repository Layout

```
specs/          Spec-Driven Development source files (all code generated from here)
main/           ESP-IDF app_main entry point
components/     Custom IDF components (one per spec module)
board-specs/    Hardware pin maps and schematic references
docs/           Architecture, how-to guides, and reference material
tools/          Host-side scripts and utilities
third_party/    Vendored dependencies (esp-matter, etc.)
examples/       Standalone example projects
```
