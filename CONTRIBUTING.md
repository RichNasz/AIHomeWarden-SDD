<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Contributing to AIHomeWarden-SDD

Thank you for your interest in contributing. This project follows Spec-Driven Development (SDD):
all changes originate in `specs/`, and generated files (firmware, docs) are never edited by hand.

---

## SDD onboarding

The single most important rule:

> **Every change starts with a spec edit, never with generated code.**

1. Identify which spec file drives the behavior you want to change.
   - Behavior and requirements live in `WHAT-*.md` files.
   - Implementation constraints and mechanisms live in `HOW-*.md` files.
2. Edit or create the appropriate spec file in `specs/<subfolder>/`.
3. Run the relevant skill or generation command to regenerate the affected output files.
4. Open a PR with both the spec change and the regenerated output.

If no spec exists for what you want to change, create one — do not patch generated code directly.
If you are unsure which spec to edit, open an issue with the `spec-improvement` template.

---

## Branch naming

| Prefix | Use for |
| --- | --- |
| `feat/<slug>` | New feature or component |
| `fix/<slug>` | Bug fix in generated output (via spec correction) |
| `spec/<slug>` | Spec-only change (no generated output yet) |
| `docs/<slug>` | Documentation-only change |

Example: `feat/eol-supervisor`, `spec/add-matter-bridge-what`

---

## PR checklist

Before requesting review, confirm:

- [ ] The relevant `WHAT-*.md` or `HOW-*.md` spec is updated or created
- [ ] All generated files affected by the spec change have been regenerated
- [ ] Every generated file has the standard agent-generated header citing the spec path
- [ ] No generated file was edited by hand (grep for the header if unsure)
- [ ] `board-specs/seeed/xiao-esp32c6.md` (or C5) was consulted for any GPIO or power facts
- [ ] `shared-specs/AIGenLessonsLearned.md` was read before any firmware generation or fix
- [ ] Traceability comment is present in every generated source file

---

## Running locally

### Prerequisites

- ESP-IDF v5.x installed; `$IDF_PATH` set in your shell
- Python 3.8+ (bundled with ESP-IDF installer)
- USB-C cable to Seeed XIAO ESP32-C6 (primary) or XIAO ESP32-C5 (fallback)

### Build and test

```bash
idf.py set-target esp32c6
idf.py build
idf.py flash monitor
```

For the ESP32-C5 fallback:

```bash
idf.py set-target esp32c5
idf.py build
idf.py flash monitor
```

---

## Code of conduct

This project follows the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md).
By participating, you agree to uphold these standards.
