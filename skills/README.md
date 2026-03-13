<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Skills

Skills are agent-invocable workflows defined in `SKILL.md` files. Each skill encodes a
repeatable generation task — reading the relevant specs, applying the generation rules, and
producing a consistent set of output files. Skills are invoked by name in Claude Code and
are never hand-executed step-by-step.

## Skills index

| Skill | Location | Purpose | Invocation |
| --- | --- | --- | --- |
| `aihomewarden-documentation-generator` | [`aihomewarden-documentation-generator/SKILL.md`](aihomewarden-documentation-generator/SKILL.md) | Generates README.md, CONTRIBUTING.md, community files, and all docs/ READMEs from WHAT-/HOW- specs | "Run the aihomewarden-documentation-generator skill" |

## Adding a new skill

1. Create `skills/<skill-name>/SKILL.md` following the pattern in an existing skill.
2. Add the corresponding spec definition to `specs/skills/<SKILL-NAME>.md`.
3. Mirror the skill file to `.claude/skills/<skill-name>/SKILL.md` so Claude Code can discover it.
4. Add a row to the skills index table above (regenerate this file via the documentation skill).

Skill names use lowercase-kebab convention (e.g., `aihomewarden-board-spec-generator`).
