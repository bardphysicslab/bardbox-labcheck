# AGENTS.md

This repository is a BardBox project. AI agents and automated engineering tools should follow the canonical BardBox standards and governance in `bardphysicslab/bardbox`.

## Shared guidance

Before planning, proposing, reviewing, delegating or implementing changes,
read the shared engineering guidance in `bardphysicslab/bardbox`. Your tool
does not load it automatically.

1. Resolve `main` once per task.
   - With a local bardbox clone, usually `../bardbox` beside this repository:
     run `git -C ../bardbox fetch origin main`, then
     `git -C ../bardbox rev-parse origin/main`. If the fetch fails, use the
     existing `origin/main` and say it may be stale.
   - Without a clone, run
     `gh api repos/bardphysicslab/bardbox/commits/main --jq .sha`.
2. Read these files at that SHA:
   - `docs/engineering/README.md`
   - `docs/engineering/development-workflow.md`
   - `docs/engineering/agent-practice.md`
   - `docs/engineering/checkouts-and-worktrees.md`

   With the clone, use `git -C ../bardbox show <sha>:docs/engineering/<file>`.
   Without it, use
   `gh api "repos/bardphysicslab/bardbox/contents/docs/engineering/<file>?ref=<sha>" -H "Accept: application/vnd.github.raw"`.
3. Record `Shared guidance: bardphysicslab/bardbox@<sha>` once in the task's
   durable evidence. If a review or proposal produces no such artifact, state
   it once in your response.

Copies (desktop files, chat project sources, memory) do not substitute for
the resolved SHA. If a required file cannot be read at the resolved SHA, do
read-only investigation only, and report it. Do not implement, commit, push,
deploy or end checkouts unless the maintainer explicitly says to proceed
without it.

This is a BardBox project: also read bardbox's root `AGENTS.md` and
`ARCHITECTURE.md` at the same SHA, and the detailed standards relevant to the
task.

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
- Instruments are passed into `run_psu_basic_v1`; exercise sequencing, verdicts and failure handling with `fakes.py` scenarios before any hardware step.

## Current implementation boundary

Do not add production instrument-control code until the first test-suite specification is written and reviewed. The immediate implementation target is `psu_basic_v1`: define what is measured, the sequence, raw outputs, derived metrics, safety limits, and pass/fail policy before automating the ET5406A or Analog Discovery Studio.

See [ARCHITECTURE.md](ARCHITECTURE.md) for the dated local prototype snapshot,
its uncommitted status, and component boundaries. Verify that the referenced code
is present before relying on it. Where the runner and suite specification differ,
report the discrepancy rather than silently changing either to match the other;
specification approval is not recorded. Results produced with fakes are not
hardware evidence.
