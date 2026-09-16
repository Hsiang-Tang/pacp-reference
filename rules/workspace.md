# Workspace invariants

- Every registered project has one relative path and one stable synthetic-safe
  identifier in the local manifest.
- The manifest separates ownership class, sensitivity, canonical source,
  lifecycle, remote policy, and backup expectation.
- The manifest itself is machine-local. Only the synthetic example is tracked.
- Unknown Git repositories inside the workspace are errors unless they are
  declared dependency trees or linked worktrees governed by a registered Git
  owner.
- Required remotes must exist. Forbidden remotes must not exist. Every fetch
  and push URL must remain inside the declared host and URL-prefix allowlists.
- A repository-local identity must match the manifest when an expected email is
  declared.
- A thousand or more pending paths is an invariant error because it usually
  signals an uncontained generated-output tree.
- The doctor reports drift and never repairs, moves, deletes, commits, or
  pushes files.
