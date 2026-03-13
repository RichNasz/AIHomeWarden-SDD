<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Skill: aihomewarden-documentation-generator

**Version**: 1.0.0
**Type**: Documentation generation
**Invocation**: Say "run the aihomewarden-documentation-generator skill" or invoke by name

## Description

Generates all project documentation from the WHAT-/HOW- spec pair in `specs/core/`. Produces
`README.md`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, `.github/` templates,
`docs/` section READMEs, `board-specs/README.md`, `shared-specs/README.md`, and `skills/README.md`.

Every output file carries the standard agent-generated header and is fully overwritten on each run.

## Inputs

| Input | Source | Required |
| --- | --- | --- |
| `WHAT-Documentation.md` | `specs/core/WHAT-Documentation.md` | Yes |
| `HOW-DocumentationGeneration.md` | `specs/core/HOW-DocumentationGeneration.md` | Yes |
| `AIGenLessonsLearned.md` | `shared-specs/AIGenLessonsLearned.md` | Yes (read first) |

## Workflow

### Step 1 — Read institutional memory (MANDATORY)

Read `shared-specs/AIGenLessonsLearned.md` in full before doing anything else.
This file contains project-wide rules that override any default behavior.

### Step 2 — Read the spec pair

Read both spec files completely:

1. `specs/core/WHAT-Documentation.md` — project identity, features, component catalog,
   spec subfolder index, board targets, skills catalog
2. `specs/core/HOW-DocumentationGeneration.md` — generation rules, required sections per file,
   badge format, tone, table style, never-generate list

### Step 3 — Generate all files

Generate every file listed in `HOW-DocumentationGeneration.md` under "Files to Generate".
For each file:

- Write the agent-generated header comment block first (exact format from HOW spec)
- Follow the "Required Sections" for that file type
- Use spaced table separators `| --- | --- |` throughout
- Use language tags on all fenced code blocks
- Do NOT add emoji unless the spec explicitly calls for them
- Do NOT generate anything inside `specs/`, `shared-specs/`, or `.github/workflows/`

### Step 4 — Verify

After all files are written, confirm:

- [ ] Every generated file has the agent-generated header
- [ ] `README.md` has all 16 required sections
- [ ] Badge row uses static Shields.io URLs (no CI badge)
- [ ] `CONTRIBUTING.md` has the SDD onboarding section
- [ ] `SECURITY.md` references GitHub Security Advisories
- [ ] All `docs/<section>/README.md` files exist and link back to `docs/README.md`
- [ ] `board-specs/README.md` table lists both primary and fallback boards
- [ ] `shared-specs/README.md` references `AIGenLessonsLearned.md`
- [ ] `skills/README.md` lists `aihomewarden-documentation-generator`
- [ ] No file was created inside `specs/`, `shared-specs/`, or `.github/workflows/`

### Step 5 — Completion message

Output exactly:

> All documentation is now in sync.

## Output Files

```
README.md
CONTRIBUTING.md
CODE_OF_CONDUCT.md
SECURITY.md
.github/ISSUE_TEMPLATE/spec-improvement.md
.github/ISSUE_TEMPLATE/bug-report.md
.github/PULL_REQUEST_TEMPLATE.md
docs/README.md
docs/guides/README.md
docs/reference/README.md
docs/tutorials/README.md
docs/how-to/README.md
docs/explanation/README.md
board-specs/README.md
shared-specs/README.md
skills/README.md
```
