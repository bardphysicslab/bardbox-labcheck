# BardBox LabCheck

**BardBox LabCheck is an open-source automated electronics laboratory test, verification, and instrumentation platform built on BardBox.**

The project automates repeatable verification and characterization of laboratory bench instruments while preserving raw measurements, test metadata, reference-instrument information, and machine-readable results for long-term equipment history.

## Initial scope

The first test suite is `psu_basic_v1`, aimed at routine bench power-supply verification.

Initial reference hardware:

- ET5406A programmable electronic load for controlled DC loading
- Analog Discovery Studio for ripple, startup, and transient measurements
- a higher-accuracy DMM later for absolute DC voltage reference measurements

The initial PSU workflow will exercise the DUT at a small set of controlled load points and transient steps, retain raw data, and derive metrics such as nominal output voltage, load regulation, ripple, transient droop, and recovery behavior.

LabCheck is initially a **verification and characterization** system, not a formal calibration service. Calibration terminology should only be used where the procedure, uncertainty analysis, and reference chain justify it.

## BardBox relationship

This repository is a BardBox project and consumes the standards defined in `bardphysicslab/bardbox`.

The project manifest is `bardbox.toml`. Shared BardBox tooling, protocol logic, drivers, and generic maintenance utilities should live in shared BardBox packages rather than being copied into LabCheck.

LabCheck-specific software belongs here: test-suite definitions, sequencing, result models, instrument adapters, local station behavior, and the LabCheck UI/API.

## Planned structure

```text
bardbox-labcheck/
├── AGENTS.md
├── bardbox.toml
├── README.md
├── software/
│   ├── station/
│   ├── testsuites/
│   │   └── psu_basic_v1/
│   └── drivers/
├── data/
├── docs/
├── hardware/
└── tests/
```

The repository was created from `bardbox-project-template`; template files will be adapted or removed deliberately as LabCheck requirements become concrete rather than rewritten wholesale at the start.

## Current implementation boundary

Before adding instrument-control code, define and review `psu_basic_v1` as a deterministic test specification: measurement sequence, load points, raw outputs, derived metrics, safety limits, error handling, and pass/fail policy.

Once the project is cloned locally, the first BardBox platform checks are:

```bash
bardbox doctor
bardbox audit
```

These checks are intended to make LabCheck the first new BardBox project developed against the shared manifest/audit model from the beginning.
