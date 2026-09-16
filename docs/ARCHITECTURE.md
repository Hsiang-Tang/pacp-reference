# Architecture

## Topology

```text
                         repository policy
              AGENTS.md + control-plane.toml + rules
                                  |
                     deterministic validation
                                  |
                machine-local manifest pointer
                                  |
                      read-only workspace doctor
                                  |
          +-----------------------+-----------------------+
          |                       |                       |
   project repository      local sensitive store    external owner
   owns its own truth      owns its own records      owns dependencies
```

PACP is a routing and governance layer. It does not become the data owner for
every project it can locate.

## Components

### Control-plane contract

`control-plane.toml` defines the product identity, startup read order,
registration pointer names, and required-file allowlist. The validator rejects
missing, duplicated, escaping, or symlinked required paths and verifies the
privacy defaults in `pacp.toml`.

### Machine registration

`tools/register_machine.py` resolves an environment override before a
namespaced global Git configuration key. `--apply` records only the reference
checkout and an optional existing manifest pointer. `--remove` deletes only
those pointers and preserves files. The design makes the execution machine
replaceable without committing its absolute paths.

### Workspace manifest

The version 2 manifest is machine-local and declares:

- route and lifecycle;
- ownership class and sensitivity;
- canonical source of truth;
- backup expectation;
- Git requirement and expected local identity;
- remote policy, allowed hosts, and allowed URL prefixes;
- bounded exclusions for dependency trees with nested Git metadata.

The repository tracks only a synthetic manifest. A real inventory must never be
copied into this project.

### Workspace doctor

`tools/workspace_doctor.py` is read-only. It validates manifest structure,
workspace topology, Git discovery, linked-worktree ownership, repository-local
identity, fetch and push remotes, instruction bridging, pending-path volume,
and stale file intake. It reports findings but performs no repair.

### Publication audit

`tools/audit_publication.py` scans candidate tracked and untracked files that
are not ignored. It rejects common key/token shapes, credential-bearing URLs,
machine-user paths, non-placeholder email addresses, and artifact types that
should not enter source history. Additional source-specific terms can be passed
with repeated `--deny` options without storing those terms in the repository.

### Local validation pipeline

`tools/validate.py` composes the deterministic validators, publication scan,
tests, Python compilation, and staged/unstaged diff checks. Hosted CI is not a
runtime dependency; the exact delivery commit is validated again from a clean
local checkout.

## Trust boundaries

1. Repository policy is portable and reviewable.
2. Machine inventory and paths remain local.
3. Project truth remains with the project owner.
4. A route supplies location and governance metadata, never copy authority.
5. Automated scans reduce obvious risk but do not decide ownership or
   publication rights.
6. Unknown state is an error or warning, never inferred success.

## Data flow

```text
resolve reference root
  -> load the declared read order
  -> resolve a manifest pointer
  -> parse and validate the manifest
  -> discover actual Git roots
  -> compare declared and observed state
  -> emit bounded findings
  -> let a human or project-owned workflow decide remediation
```

No step uploads workspace contents, opens project files for aggregation, or
changes repository state.

## Recovery model

The canonical repository restores portable policy and tools. A machine is
reconstructed by cloning an authorized revision, registering the two
namespaced pointers, restoring any separately governed local data from its own
backup, and rerunning the validators. The reference project does not claim to
back up real machine data.

## Limits

This slice is not an orchestration engine, scheduler, status dashboard, secret
manager, backup product, or cross-project search system. It demonstrates the
smallest coherent governance, registration, validation, and privacy boundary
from the source architecture.
