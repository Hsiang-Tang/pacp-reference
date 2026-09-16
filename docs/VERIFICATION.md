# Verification contract

## Required commands

Run from the repository root:

```sh
python3 tools/validate.py
```

Before public delivery, also run the audit with a local, untracked denylist
translated into repeated `--deny` arguments and use an independently installed
secret scanner when available:

```sh
python3 tools/validate.py --deny internal-codename
```

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
- Public visibility, license, disabled Pages, releases, deployments,
  collaborators, and repository security settings must be checked after
  delivery.

## Evidence invalidation

Any source, rule, schema, manifest, workflow, test-selection, remote, or
visibility change invalidates the corresponding evidence. Documentation-only
changes still require the validator, publication audit, tests, and diff check
because documentation is part of the disclosure surface.

## Initial private-candidate evidence

On 2026-09-16, the initial private candidate passed the complete command set,
18 unit tests, the built-in publication audit, an additional local deny-term
scan, and a 31-file tracked-object audit. The pushed commit was cloned into a
new temporary directory and passed the same validator, synthetic workspace,
publication, test, compilation, diff, clean-worktree, and artifact-name gates.
The host reported Private visibility and no enabled Pages endpoint. This is
delivery evidence only; it does not approve public disclosure.

An early hosted-workflow attempt was stopped by GitHub before any step because
of an account quota/billing gate; it reported no code or test failure. Hosted
CI was then removed by owner direction. `tools/validate.py` and a clean local
checkout now own the complete validation contract.

## Public release evidence

On 2026-09-16, the owner selected the MIT License and authorized public
visibility. The public repository was re-audited after that transition: the
local validation pipeline passed 19 tests, the publication audit passed, Pages
was disabled, and there were no releases, deployments, forks, additional
collaborators, pending invitations, or Actions workflows. The commit history
uses only the owner's GitHub identity. Future changes invalidate the relevant
evidence and must repeat this contract.
