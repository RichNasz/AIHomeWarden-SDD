<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Shared Specs

`shared-specs/` contains human-authored institutional memory for this project. Unlike files in
`specs/`, which drive code and documentation generation, `shared-specs/` documents hard-won
lessons and cross-cutting rules that all agent generation sessions must follow. This directory
is never generated — it is written and maintained by humans.

## File index

| File | Purpose |
| --- | --- |
| [`AIGenLessonsLearned.md`](AIGenLessonsLearned.md) | Mandatory first-read for every agent generation, fix, or debug session. Contains ESP32-C6/C5 hardware pitfalls, ESP-IDF build system lessons, and the required workflow when something goes wrong. |

## Reading order

**Read `AIGenLessonsLearned.md` BEFORE any generation, fix, or debug session.**

This is not optional. The file contains rules that override default agent behavior, including:

- RTC GPIO ranges per chip family (wakeup GPIO assignments)
- NimBLE initialization lifecycle (double-init crash prevention)
- NVS flash init requirement before BLE/Wi-Fi
- CMakeLists.txt ordering rules
- Component name corrections for ESP-IDF 5.5.x

If you discover a new lesson during a generation or debug session, add it to
`AIGenLessonsLearned.md` following the template at the bottom of that file.
