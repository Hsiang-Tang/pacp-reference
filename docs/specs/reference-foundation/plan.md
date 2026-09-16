# Reference foundation plan

## Baseline and selection

The source already contains working control-plane validation, machine pointer
registration, a version 2 workspace manifest doctor, privacy rules, and tests.
This implementation exports only that coherent slice. It narrows vocabulary,
removes private product integrations, replaces all examples with synthetic
data, and retains standard-library execution.

## Risk and authority

- Risk: privacy-sensitive public repository delivery.
- Authorized: maintain the allowlisted reference slice, validate it, and push
  to the verified owner remote.
- Accepted publication decision: public visibility with the MIT License.
- Human gate: any broader disclosure, release, package, Pages activation, or
  license change.
- Failure posture: exclude uncertain content from public history.

## Design

- `control-plane.toml` owns the closed file and startup contract.
- `pacp.toml` owns machine-verifiable state and disclosure defaults.
- `register_machine.py` owns two namespaced path pointers.
- `workspace_doctor.py` owns read-only manifest and observed-state comparison.
- `audit_publication.py` owns deterministic publication-hazard patterns plus
  caller-supplied deny terms.
- The checked-in example is self-contained and non-Git; tests create temporary
  Git owners for boundary behavior.

## Verification strategy

Use known-good and known-bad unit fixtures, run all repository validators, scan
the candidate and staged/tracked file set, then clone the pushed commit into a
disposable directory and repeat the main gate. Confirm public visibility and
the intended hosted-surface settings after push.

## Rollback

After ordinary delivery, revert a faulty change with a new commit. If sensitive
material ever enters public history, remove it through an explicitly reviewed
incident procedure and rotate any affected credential. A history rewrite is
not a substitute for treating exposed data as compromised.
