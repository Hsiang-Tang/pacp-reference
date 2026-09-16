# Source and reference differences

This repository was produced through an allowlist selective export into a new
Git history. It is not a fork and contains no source `.git` directory, commits,
branches, tags, or remotes.

## Adapted capabilities

- The TOML read helper preserves the source's standard-library parsing model.
- Machine registration preserves environment-first and Git-config-second
  pointer resolution, scoped apply/remove behavior, and non-copying manifest
  registration. Product-specific bootstrap installation and runtime-state
  pointers are omitted.
- Workspace validation preserves the versioned manifest, governance fields,
  Git discovery, linked-worktree ownership, identity, remote allowlists,
  worktree-volume boundary, stale-inbox check, and read-only behavior. The
  public vocabulary is narrower and generic.
- The control-plane validator preserves a declared required-file contract and
  fail-closed policy invariants, reduced to this repository's minimal surface.
- Tests preserve the source's temporary-directory and known-bad-fixture style,
  with entirely synthetic identities and repositories.

## Deliberately excluded

- real workspace inventory, absolute paths, machine roles, device state, and
  private remote URLs;
- personal project status, history, notes, evidence, metrics, and logs;
- employer, customer, and organization-specific material;
- runtime databases, automation schedules, engine evaluation records, model
  routing, orchestration, mobile clients, dashboards, and product-family data;
- credentials, authentication details, `.env` files, caches, build artifacts,
  and generated outputs;
- private operating rules that could not be safely generalized;
- source repository history and compatibility aliases that are unnecessary for
  a standalone reference implementation.

## Behavioral limits

The reference doctor reports state but does not repair it. Registration writes
only two namespaced pointers. Publication scanning catches common patterns but
cannot establish copyright, ownership, or disclosure permission. Those limits
are intentional and must not be represented as missing production features.
