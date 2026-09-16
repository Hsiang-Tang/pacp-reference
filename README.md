# PACP Reference Implementation

**In plain terms:** this is a small toolkit that keeps AI coding agents (such
as Claude Code and Codex) working from the same shared rules across several
machines and projects, without ever storing real project data, file paths, or
credentials in Git. It answers a concrete problem: when more than one AI agent
edits your code on more than one machine, how do you make sure they all read
the same policy, stay inside the right project boundary, and never leak
machine-specific or private details into a repository you might publish. The
sections below describe the underlying design in more general terms.

For example, on a machine that runs both Claude Code and Codex against
several personal projects, this toolkit is what confirms, before either agent
makes a change, that the local checkout matches the approved rules, that the
project the agent is about to touch is the one it thinks it is, and that
nothing sensitive (paths, secrets, personal data) is about to be committed.
That check runs locally and produces no output beyond a pass/fail result and a
list of any violations.

PACP Reference Implementation is a sanitized, minimal slice of the
**Personal Agent Control Plane (PACP)**. It demonstrates how durable agent
rules, machine-local workspace registration, repository validation, and
privacy-aware delivery can work together without centralizing project data.

This repository is a private public-display candidate. It is not yet approved
for public visibility, has no open-source license, and must remain private until
the human review in [`docs/PUBLICATION-CHECKLIST.md`](docs/PUBLICATION-CHECKLIST.md)
is complete.

## What this reference includes

- a closed control-plane configuration and deterministic validator;
- environment-first, Git-config-second machine pointer registration;
- a read-only versioned workspace manifest doctor;
- remote host and URL-scope checks;
- ownership, sensitivity, source-of-truth, lifecycle, and backup metadata;
- generated-output and unknown-repository detection;
- synthetic fixtures and positive, negative, boundary, and recovery tests;
- a publication audit for common secrets, personal paths, email addresses, and
  generated artifacts;
- explicit security, privacy, architecture, verification, and publication
  boundaries.

It intentionally excludes the full private product, real workspace inventory,
runtime evidence stores, automations, mobile clients, private status, project
names, machine settings, and historical records.

## Core concept

PACP is a map and control surface, not a warehouse:

```text
intent -> load durable rules -> resolve machine-local route
       -> enter the project-owned boundary -> verify -> record evidence there
```

The checked-in policy is portable. Exact machine paths and project inventory
stay in an untracked machine-local manifest. Each project keeps its own source,
requirements, decisions, status, and detailed evidence.

## Requirements

- Python 3.11 or newer
- Git
- no third-party Python packages

## Quick start

Clone the repository, then run the complete local checks:

```sh
python3 tools/validate.py
```

The local pipeline runs the control-plane validator, synthetic workspace
doctor, publication audit, unit tests, Python compilation, and staged/unstaged
diff checks. Add private review terms without storing them in Git:

```sh
python3 tools/validate.py --deny internal-codename
```

Inspect the current reference pointers without changing machine state:

```sh
python3 tools/register_machine.py
```

To exercise registration safely, use a disposable global Git configuration:

```sh
temporary_config="$(mktemp)"
GIT_CONFIG_GLOBAL="$temporary_config" \
  python3 tools/register_machine.py --apply \
  --workspace-manifest examples/workspace.toml
GIT_CONFIG_GLOBAL="$temporary_config" python3 tools/register_machine.py
```

The production-style `--apply` command writes only the namespaced
`pacp.referenceRoot` and `pacp.referenceWorkspaceManifest` pointers. It never
copies manifest contents into this repository.

## Synthetic example

[`examples/workspace.toml`](examples/workspace.toml) registers one fictional,
non-Git notes project under a self-contained synthetic workspace. It contains
no real names, paths, remotes, accounts, or records.

```sh
python3 tools/workspace_doctor.py --manifest examples/workspace.toml --json
```

An empty JSON array means the synthetic workspace satisfies the manifest
contract. The tests create temporary Git repositories to prove unregistered
repository, identity, remote-scope, and large-worktree failure behavior.

## Architecture and safety

- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) describes components, trust
  boundaries, and the validation flow.
- [`rules/security.md`](rules/security.md) defines the disclosure boundary.
- [`rules/workspace.md`](rules/workspace.md) defines the manifest and repository
  invariants.
- [`docs/DIFFERENCES.md`](docs/DIFFERENCES.md) explains what was adapted and
  what was deliberately omitted from the source project.
- [`docs/VERIFICATION.md`](docs/VERIFICATION.md) owns executable acceptance.

Private hosting is not a substitute for sanitization. Unknown material is
excluded, automated scans are defense in depth, and a human must still confirm
ownership and disclosure rights before publication.

## Testing

The test suite uses `unittest` and the Python standard library. Tests cover the
real checked-in configuration, malformed and missing configuration, pointer
precedence and removal, synthetic workspace success, unregistered Git roots,
remote allowlists, sensitive-looking text, and forbidden artifact names.

Hosted CI is intentionally absent because validation runs locally. A delivery
candidate must pass the local pipeline again from a clean checkout of its exact
commit. Passing validation does not authorize publication.

## Publication status

Current status is tracked in [`docs/STATUS.md`](docs/STATUS.md). Before any
visibility change, release, package, or Pages configuration, complete
[`docs/PUBLICATION-CHECKLIST.md`](docs/PUBLICATION-CHECKLIST.md) and obtain an
explicit human decision. Until then, this repository stays Private.
