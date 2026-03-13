<!-- ================================================
     HUMAN-WRITTEN — GOLD STANDARD INSTITUTIONAL MEMORY
     ================================================ -->

# AIGenLessonsLearned.md — Gold Standard Lessons Learned

**MANDATORY FIRST STEP**: Every time you generate, regenerate, fix, or debug ANY code in this
repository, read this file first.

## Core Rules (Never Violate)

- Humans only ever edit files inside `specs/` and `shared-specs/`.
- Never edit generated files (`.c`, `.h`, `CMakeLists.txt`, `sdkconfig.defaults`, `README.md`, etc.) by hand.
- If something is wrong, improve the spec — never patch the generated code.
- Always reference `board-specs/` files instead of hard-coding GPIO numbers or power figures.
- `specs/` is READ-ONLY to agents — never create, edit, or generate files inside it.
- If a required spec is missing, stop and ask the user — never invent content.
- Every generated file must begin with the standard agent-generated header citing the full spec path.

## Key Lessons Learned (ESP32-C6 / ESP32-C5 Specific)

- **RTC GPIO ranges differ per ESP32 family — validate before assigning wakeup GPIOs.**
  `ext1` deep-sleep wakeup requires RTC-capable GPIOs. Valid ranges:
  - **ESP32-C6: GPIO 0–7 only** — boot button GPIO 9 is NOT an RTC GPIO
  - **ESP32-C5: GPIO 0–6 only** — boot button GPIO 9 is NOT an RTC GPIO
  When the only physical button is not RTC-capable, use timer-only wakeup or an external
  RTC-capable GPIO. Document the limitation clearly — no external hardware workarounds.
  Symptoms: `esp_sleep_enable_ext1_wakeup()` returns `ESP_ERR_INVALID_ARG` at runtime,
  or device never wakes from deep sleep on button press. (Sourced from esp32-sdd-showcase, Mar 2026)

- **ESP32-S3 / C3 / C6 / H2 do NOT support `esp_sleep_enable_ext0_wakeup()`.**
  `ext0` is ESP32-original-only. On all other families use:
  `esp_sleep_enable_ext1_wakeup(1ULL << gpio_num, ESP_EXT1_WAKEUP_ANY_LOW)`.
  Wakeup cause is `ESP_SLEEP_WAKEUP_EXT1`, not `ESP_SLEEP_WAKEUP_EXT0`.
  Compiler error: `implicit declaration of function 'esp_sleep_enable_ext0_wakeup'`.
  (Sourced from esp32-sdd-showcase, Mar 2026)

- **`nvs_flash_init()` is required before any BLE or Wi-Fi API call.**
  The BLE controller stores PHY calibration data in NVS. Without it, `esp_bt_controller_init()`
  fails with `BLE_INIT: controller init failed`. On USB CDC boards the crash loop is invisible
  (device resets too fast to enumerate). Always include the erase-on-corruption pattern and add
  `nvs_flash` to `REQUIRES` in `main/CMakeLists.txt`.
  (Sourced from esp32-sdd-showcase, Mar 2026)

- **`nimble_port_init()` handles BLE controller init — do NOT call `esp_bt_controller_init/enable` explicitly.**
  In ESP-IDF 5.x, `nimble_port_init()` internally calls init and enable. Calling them first
  causes a double-init crash. Similarly `nimble_port_deinit()` handles disable and deinit.
  Correct lifecycle: `nimble_port_init()` → use stack → `nimble_port_stop()` → `nimble_port_deinit()`.
  No `#include "esp_bt.h"` needed. (Sourced from esp32-sdd-showcase, Mar 2026)

- **NimBLE broadcaster-only builds require `CONFIG_BT_NIMBLE_SECURITY_ENABLE=n`** on ESP-IDF 5.5.x.
  Guard mismatch in `ble_hs.c` causes `undefined reference to 'ble_sm_deinit'` at link time.
  Fix: `CONFIG_BT_NIMBLE_SECURITY_ENABLE=n` in `sdkconfig.defaults`. A non-connectable broadcaster
  has zero use for the security manager. (Sourced from esp32-sdd-showcase, Mar 2026)

- **`sdkconfig.defaults` is only applied when no `sdkconfig` file exists at the project root.**
  After any `idf.py menuconfig` session, delete `sdkconfig` before a clean build to ensure
  `sdkconfig.defaults` takes effect. (Sourced from esp32-sdd-showcase, Mar 2026)

## Key Lessons Learned (ESP-IDF Build System)

- **CMakeLists.txt ordering: `include(project.cmake)` BEFORE `project()`.**
  ESP-IDF injects the cross-compiler toolchain via `project.cmake`, which must load before
  CMake's `project()` call. Reversing the order causes CMake to detect the host compiler
  (Apple Clang on macOS) instead of the RISC-V cross-compiler, silently breaking the build.
  Always: `include($ENV{IDF_PATH}/tools/cmake/project.cmake)` then `project(name)`.
  (Sourced from esp32-sdd-showcase, Mar 2026)

- **`Kconfig.projbuild` must live in a component directory (e.g. `main/`), not the project root.**
  ESP-IDF only auto-discovers `Kconfig.projbuild` inside component dirs. Placing it at the root
  silently drops all symbols, causing `#error` guards and undeclared-identifier cascades.
  (Sourced from esp32-sdd-showcase, Feb 2026)

- **Stack overflow Kconfig symbol is `FREERTOS_CHECK_STACKOVERFLOW_CANARY`**, not
  `ESP_SYSTEM_CHECK_STACKOVERFLOW_CANARY`. The latter does not exist in ESP-IDF 5.x.
  Use `CONFIG_FREERTOS_CHECK_STACKOVERFLOW_CANARY=y` in `sdkconfig.defaults`.
  (Sourced from esp32-sdd-showcase, Mar 2026)

- **ESP-IDF 5.5.x component name corrections for `main/CMakeLists.txt` REQUIRES:**
  - OTA operations → component is **`app_update`**, NOT `esp_ota_ops`
  - Task watchdog (`esp_task_wdt.h`) → header lives in **`esp_system`** component
  Using wrong names causes cmake to fail with "component could not be found".
  (Sourced from esp32-sdd-showcase, Mar 2026)

## Required Workflow When Something Goes Wrong

1. Read this file.
2. Check `board-specs/<vendor>/<board>.md` and the relevant `specs/` files.
3. Improve the appropriate `specs/` WHAT- or HOW- file.
4. Regenerate from the corrected spec.
5. Never manually edit generated code.

## Template for Adding New Lessons

When you discover something important:

- Add it under the appropriate section above
- Date it and note the symptom, root cause, and fix
- Make it actionable for future AI agents reading this file

This file is the living quality guardrail and institutional memory of the AIHomeWarden-SDD project.
