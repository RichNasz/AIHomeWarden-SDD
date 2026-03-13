# HOW-DocumentationGeneration.md — Documentation Generation Rules

## Agent-Generated File Header

Every file produced by the documentation generator MUST begin with this comment block.
Adapt the spec citation to list both WHAT- and HOW- files that drove the content:

```
<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: YYYY-MM-DD | Agent: Claude Code
     ================================================ -->
```

For `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, `SECURITY.md`, and `.github/` templates, use an
HTML comment at the top of the file as above. For files where HTML comments are not appropriate
(none expected in this set), adapt accordingly.

## Files to Generate

The skill MUST generate all of the following. Existing files are overwritten in full.

| File | Description |
| --- | --- |
| `README.md` | Root project readme — primary entry point for all contributors |
| `CONTRIBUTING.md` | Contribution guide (SDD rules, branch naming, PR checklist) |
| `CODE_OF_CONDUCT.md` | Contributor Covenant v2.1 |
| `SECURITY.md` | Security disclosure policy (local-only device, responsible disclosure) |
| `.github/ISSUE_TEMPLATE/spec-improvement.md` | Issue template for spec improvements |
| `.github/ISSUE_TEMPLATE/bug-report.md` | Issue template for firmware bug reports |
| `.github/PULL_REQUEST_TEMPLATE.md` | PR template with SDD checklist |
| `docs/README.md` | Docs root index — links to all sub-sections |
| `docs/guides/README.md` | Placeholder: guides index |
| `docs/reference/README.md` | Placeholder: reference index |
| `docs/tutorials/README.md` | Placeholder: tutorials index |
| `docs/how-to/README.md` | Placeholder: how-to index |
| `docs/explanation/README.md` | Placeholder: explanation index |
| `board-specs/README.md` | Board specs index — lists all boards with primary/fallback role |
| `shared-specs/README.md` | Shared-specs index — describes AIGenLessonsLearned.md and usage |
| `skills/README.md` | Skills index — lists all skills with name, purpose, invocation |

### Files NEVER to generate

- Anything inside `.github/workflows/` — CI/CD pipelines are human-authored
- Anything inside `specs/` or `shared-specs/` — those are human-authored
- Binary assets or images

## README.md Required Sections (in order)

1. **Agent-generated header** (HTML comment block as above)
2. **Badge row**: ESP-IDF v5.x | ESP32-C6 | Matter | Built with Claude Code
   — no CI/CD badge (no workflows exist yet)
3. **Title**: `# AIHomeWarden-SDD`
4. **Tagline**: one-line italic description under the title
5. **Description**: 2–3 sentence paragraph expanding on the tagline
6. **Features**: bulleted list from `WHAT-Documentation.md` feature bullets
7. **Table of Contents**: anchor links to all major sections
8. **Quick Start**: prerequisites + build/flash commands for ESP32-C6 + note on C5 fallback
9. **Prerequisites**: ESP-IDF v5.x, `$IDF_PATH`, idf.py set-target, optional esp-matter SDK
10. **Component Table**: columns: Component | Purpose — from `WHAT-Documentation.md` component catalog
11. **Spec Index**: table of spec subfolders from `WHAT-Documentation.md`
12. **Skills Table**: columns: Skill | Purpose — from `WHAT-Documentation.md` skills catalog
13. **Documentation**: link to `docs/README.md` with a one-line description
14. **Contributing**: one sentence + link to `CONTRIBUTING.md`
15. **License**: MIT statement + link to [`LICENSE.TXT`](LICENSE.TXT)
16. **Footer**: "All code and docs are generated from specs/ following Spec-Driven Development (SDD)."

## Badge Row Spec

Use static Shields.io badges (no CI dependency). Format:

```markdown
![ESP-IDF](https://img.shields.io/badge/ESP--IDF-v5.x-blue)
![ESP32-C6](https://img.shields.io/badge/target-ESP32--C6-green)
![Matter](https://img.shields.io/badge/protocol-Matter%20over%20Thread-purple)
![Built with Claude Code](https://img.shields.io/badge/built%20with-Claude%20Code-orange)
```

## Tone and Style

- **Professional and precise**: use exact technical terms (EOL supervision, not "sensor monitoring")
- **Security-focused**: acknowledge that this is a physical security system;
  phrase features in terms of reliability and tamper resistance
- **Community-friendly**: welcoming to contributors; clear SDD onboarding path
- **No marketing fluff**: avoid superlatives; let the feature list speak
- **Tense**: present tense for current capabilities, future tense for roadmap items
- **Headings**: title case for H1/H2; sentence case for H3 and below
- **Tables**: always use spaced separator style `| --- | --- |` (markdownlint compliant)
- **Code blocks**: always specify a language tag (` ```bash `, ` ```ini `, ` ```c `)

## CONTRIBUTING.md Required Sections

1. Agent-generated header
2. **SDD Onboarding** — explain that all changes start with a spec edit, never with code
3. **Branch Naming** — `feat/<slug>`, `fix/<slug>`, `spec/<slug>`, `docs/<slug>`
4. **PR Checklist** — spec updated, generated files regenerated, traceability header present,
   no hand-edited generated files, board-specs/ consulted for GPIO/power facts
5. **Running Locally** — prerequisite list and `idf.py build` commands
6. **Code of Conduct** — one-line reference to `CODE_OF_CONDUCT.md`

## SECURITY.md Required Sections

1. Agent-generated header
2. **Scope** — firmware-only, local network; note that the device has no cloud attack surface
3. **Supported Versions** — current `main` branch only
4. **Reporting a Vulnerability** — instruct reporters to open a GitHub Security Advisory
   (private); do NOT post vulnerabilities in public Issues
5. **Response SLA** — acknowledge within 5 business days; patch within 30 days for critical

## docs/ Sub-README Sections

Each `docs/<section>/README.md` is a placeholder that:
- States what kind of content will live in that section (Diátaxis model):
  - `guides/` — goal-oriented guides combining multiple how-tos
  - `reference/` — API, component interface, and configuration reference
  - `tutorials/` — learning-oriented step-by-step walkthroughs
  - `how-to/` — problem-oriented recipes (e.g., "How to add a new zone")
  - `explanation/` — background concepts (EOL theory, Matter pairing, etc.)
- Links back to `docs/README.md`
- Contains a "Content coming soon" note

## board-specs/README.md Required Sections

1. Agent-generated header
2. **Purpose** — one paragraph: board specs are agent-generated from vendor documentation;
   they are the source of truth for GPIO, power, and peripheral facts used in code generation
3. **Board Index** — table: Board | Role | Chip | Spec File | Source URL
4. **Usage Note** — "Always read the relevant board spec before generating any component
   that references GPIO numbers, ADC channels, or power budgets."
5. **Regeneration** — brief note that board specs are regenerated from vendor docs via the
   `aihomewarden-board-spec-generator` skill; never hand-edit

## shared-specs/README.md Required Sections

1. Agent-generated header
2. **Purpose** — one paragraph: shared-specs/ contains human-authored institutional memory;
   it is NOT generated; it is the gold standard for agent behavior in this project
3. **File Index** — table: File | Purpose
   - `AIGenLessonsLearned.md` — mandatory first-read for every agent generation or fix session
4. **Reading Order** — "Read AIGenLessonsLearned.md BEFORE any generation, fix, or debug."

## skills/README.md Required Sections

1. Agent-generated header
2. **Purpose** — one paragraph: skills are agent-invocable workflows defined in SKILL.md files;
   each skill is invoked by name in Claude Code and drives a repeatable generation task
3. **Skills Index** — table: Skill | Location | Purpose | Invocation
4. **Adding a New Skill** — brief note: create `skills/<name>/SKILL.md`,
   add it to `specs/skills/`, mirror in `.claude/skills/`
