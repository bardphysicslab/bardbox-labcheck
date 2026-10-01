# LabCheck Architecture

## Local prototype snapshot (2026-10-01)

The components below were inspected in the local development working tree and
are not yet committed with this document. A clean clone may not contain these
paths. This records the prototype's boundaries, not a delivered implementation
or verified hardware safety. Recheck the code and update this status when it is
committed. The suite specification's approval status remains unrecorded.

## Prototype structure
- `software/testsuites/psu_basic_v1/runner.py`: `run_psu_basic_v1` owns test
  sequencing, per-case verdicts, attempted cleanup (load and DUT off calls in a
  `finally` block; successful shutdown is not established by that alone) and result assembly. Instruments are passed in, not
  constructed.
- `fakes.py`: deterministic fake DUT, load and reference instruments with named
  failure scenarios.
- `SPEC.md` and `schema/*.json`: written procedure, verdict rules, safety limits
  and result format (approval status not recorded).
- `software/drivers/ads_driver.py` + `dwf_backend.py`: read-only Analog
  Discovery measurement; only `dwf_backend.py` touches the vendor library, and
  the backend is injectable.
- `software/station/app.py`: web UI that runs fake scenarios, saves result
  JSON and shows Analog Discovery status through `ADSDriver`; sequencing and
  verdicts stay in the runner.

## Intended
When real instruments are added, safe-state handling stays in the runner, not
the UI (BardBox architecture principle 6).
