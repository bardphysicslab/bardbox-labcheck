# AGENTS.md

This repository is a BardBox project. AI agents and automated engineering tools should follow the canonical BardBox standards and governance in `bardphysicslab/bardbox`.

## Project role

BardBox LabCheck is an open-source automated electronics laboratory test, verification, and instrumentation platform built on BardBox.

Initial scope is automated verification of bench power supplies, beginning with the `psu_basic_v1` test suite. The first reference instruments are an ET5406A programmable electronic load and an Analog Discovery Studio, with a higher-accuracy DMM added later for absolute DC reference measurements.

## Working rules

- Read the project `README.md` and `bardbox.toml` before making changes.
- Follow canonical BardBox protocol, naming, manifest, audit, and contributor rules rather than inventing project-specific alternatives.
- Keep reusable BardBox drivers, protocol logic, config machinery, and tooling in shared BardBox libraries/tools rather than copying them into this repository.
- Keep LabCheck-specific test definitions, sequencing, result models, instrument adapters, and UI behavior in this repository unless they become broadly reusable.
- Preserve raw measurements and machine-readable evidence before generating summaries or pass/fail conclusions.
- Do not describe LabCheck as a calibration system unless a procedure and reference chain actually support that claim; use verification/characterization terminology by default.
- No arbitrary destructive instrument control, deployment, Git history rewriting, or production changes without explicit human authorization.
- Before consequential changes, run applicable tests and `bardbox doctor` / `bardbox audit` when available.

## Current implementation boundary

Do not add production instrument-control code until the first test-suite specification is written and reviewed. The immediate implementation target is `psu_basic_v1`: define what is measured, the sequence, raw outputs, derived metrics, safety limits, and pass/fail policy before automating the ET5406A or Analog Discovery Studio.
