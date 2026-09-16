# Verification contract

## Required commands

Run from the repository root:

```sh
python3 tools/check_control_plane.py
python3 tools/workspace_doctor.py --manifest examples/workspace.toml
python3 tools/audit_publication.py
python3 -m unittest discover -s tests -v
python3 -m compileall -q tools tests
git diff --check
```

Before publication review, also run the audit with a local, untracked denylist
translated into repeated `--deny` arguments and use an independently installed
secret scanner when available.

## Requirement traceability

| Requirement | Implementation | Evidence |
| --- | --- | --- |
| REF-001 closed configuration | `control-plane.toml`, `pacp.toml`, `tools/check_control_plane.py` | positive and known-bad validator tests |
| REF-002 scoped registration | `tools/register_machine.py` | environment precedence, apply, remove, preservation tests |
| REF-003 manifest governance | `tools/workspace_doctor.py` | synthetic success and invalid-governance tests |
| REF-004 Git and remote safety | `tools/workspace_doctor.py` | unknown-repository, identity, fetch/push scope tests |
| REF-005 privacy boundary | `rules/security.md`, `tools/audit_publication.py` | token, path, email, and artifact negative fixtures |
| REF-006 synthetic-only example | `examples/` | doctor returns zero findings |
| REF-007 clean delivery | Git audit and clean-checkout run | tracked-files review and fresh-clone evidence at delivery |

## Acceptance interpretation

- Validator and test failures block delivery.
- Workspace warnings must be explained and resolved when they concern this
  repository.
- A clean publication audit is defense in depth, not a publication decision.
- The fresh-checkout run must use the exact pushed commit.
- Private visibility and disabled Pages must be checked both before first push
  and after delivery.

## Evidence invalidation

Any source, rule, schema, manifest, workflow, test-selection, remote, or
visibility change invalidates the corresponding evidence. Documentation-only
changes still require the validator, publication audit, tests, and diff check
because documentation is part of the disclosure surface.
