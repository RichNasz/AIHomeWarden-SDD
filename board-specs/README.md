<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Board Specs

Board specs are agent-generated reference documents derived from official vendor documentation.
They are the single source of truth for GPIO assignments, power budgets, strapping pin warnings,
ADC channel mappings, and peripheral facts used in code generation. Never hand-edit a board spec —
regenerate it from the vendor source using the `aihomewarden-board-spec-generator` skill.

## Board index

| Board | Role | Chip | Spec file | Source |
| --- | --- | --- | --- | --- |
| Seeed XIAO ESP32-C6 | Primary target | ESP32-C6 | [`seeed/xiao-esp32c6.md`](seeed/xiao-esp32c6.md) | Seeed Wiki |
| Seeed XIAO ESP32-C5 | Fallback target | ESP32-C5 | [`seeed/xiao-esp32c5.md`](seeed/xiao-esp32c5.md) | Seeed Wiki |

## Usage

Always read the relevant board spec before generating any component that references:

- GPIO numbers or alternate functions
- ADC channels (note: ESP32-C6 has ADC1 only — no ADC2)
- Power budget figures (active mA, deep sleep µA)
- Strapping pins (the #1 cause of boot failures — always check before assigning GPIOs)
- Onboard peripherals (LED polarity, button GPIO, antenna switch pins)

## Regeneration

Board specs are regenerated from vendor documentation via the `aihomewarden-board-spec-generator`
skill. Provide the authoritative vendor URL and pre-verified key facts (LED GPIO + polarity,
strapping pins, PSRAM size, deep sleep current) before invoking the skill. Never generate a
board spec from memory alone — treat any output without a source URL as unverified.
