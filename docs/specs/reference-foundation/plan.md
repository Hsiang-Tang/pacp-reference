# Reference foundation plan

## Baseline and selection

The source already contains working control-plane validation, machine pointer
registration, a version 2 workspace manifest doctor, privacy rules, and tests.
This implementation exports only that coherent slice. It narrows vocabulary,
removes private product integrations, replaces all examples with synthetic
data, and retains standard-library execution.

## Risk and authority

- Risk: privacy-sensitive private repository delivery.
- Authorized: create the new repository, adapt allowlisted files, validate,
  commit, and push to the verified private owner remote.
- Human gate: any public visibility, license choice, release, package, or Pages
  activation.
- Failure posture: exclude uncertain content and keep the repository Private.

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
disposable directory and repeat the main gate. Confirm hosted visibility and
Pages state before and after push.

## Rollback

Before first push, remove the unneeded empty remote only through an explicit
owner decision. After push, revert with a new commit or archive the still-private
repository. Never rewrite or publish unsafe history as a cleanup shortcut.
