# AIHomeWarden-SDD – CLAUDE INSTRUCTIONS (DO NOT EDIT MANUALLY)

Project rules:
- Target: ESP32-C6 (primary) with ESP32-C5 fallback
- Stack: ESP-IDF v5.x + esp-matter SDK + MQTT for robots
- All code and docs MUST be generated from specs/
- Add traceability comment in every generated file: "Generated from specs/XXX.md on [date]"
- Always scope work to ONE component or task at a time
- Prefer local-only operation (no cloud)
- Future vision: predictive/generative AI on sensor data
