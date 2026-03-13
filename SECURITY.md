<!-- ================================================
     AGENT-GENERATED — DO NOT EDIT BY HAND
     Generated from specs/core/WHAT-Documentation.md
                  + specs/core/HOW-DocumentationGeneration.md
     Date: 2026-03-13 | Agent: Claude Code
     ================================================ -->

# Security Policy

## Scope

AIHomeWarden-SDD is a local-only firmware project. The device has no cloud attack surface at
runtime — all alarm logic, zone supervision, and robot presence suppression run on-device.
The threat surface is limited to the local network (MQTT, BLE, Thread/Matter) and physical
access to the hardware.

This policy covers firmware vulnerabilities, protocol implementation flaws, and hardware design
issues that could compromise the security or safety of a deployed alarm system.

## Supported versions

Only the current `main` branch is actively maintained. Older commits do not receive security patches.

## Reporting a vulnerability

**Do not post vulnerability details in a public GitHub issue.**

Report privately using GitHub's built-in Security Advisories:

1. Go to the repository's **Security** tab.
2. Select **Report a vulnerability**.
3. Describe the issue, affected component, and reproduction steps.

We will acknowledge receipt within 5 business days and aim to release a patch within 30 days
for critical issues. We will credit reporters in release notes unless anonymity is requested.

## Notes for researchers

- Threat modeling should consider local network access, MQTT broker configuration,
  BLE sniffing, and physical tamper scenarios.
- GPIO assignments and power behavior are documented in `board-specs/` — consult these
  before testing hardware-level attack vectors.
- The EOL resistor supervision circuit is a physical safety mechanism; any vulnerability
  that defeats tamper detection is considered critical.
