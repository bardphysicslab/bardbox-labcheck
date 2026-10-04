# LabCheck Architecture

## Status (2026-10-03)

No test-suite implementation is committed. A local prototype (runner, fake
instruments, written specification, schemas, Analog Discovery driver and
station UI) was explored outside version control and discarded on 2026-10-03
at the maintainer's direction. It is not in this repository; do not assume
any of its files exist. No suite specification has been approved, and nothing
here establishes verified hardware safety.

## Intended design (not implemented)

The boundaries below come from that prototype and remain the intended
design for `psu_basic_v1`. They describe planned components, not delivered
code.

- **Runner:** `run_psu_basic_v1` owns test sequencing, per-case verdicts,
  cleanup and result assembly. Instruments are passed in, not constructed.
  Cleanup attempts to switch the load and DUT off in a `finally` block; that
  attempt alone does not establish a successful shutdown, which must be
  verified.
- **Fake instruments:** deterministic fake DUT, load and reference
  instruments with named failure scenarios, used to exercise sequencing,
  verdicts and failure handling before any hardware step.
- **Specification and schemas:** a written procedure, verdict rules, safety
  limits and a machine-readable result format, reviewed before instrument
  control is automated (see AGENTS.md, "Current implementation boundary").
- **Analog Discovery driver:** read-only measurement. Only a small backend
  module touches the vendor library, and that backend is injectable for
  tests.
- **Station UI:** runs scenarios, saves result JSON and shows instrument
  status. Sequencing and verdicts stay in the runner.

When real instruments are added, safe-state handling stays in the runner, not
the UI (BardBox architecture principle 6).
