# Security and privacy boundary

- Keep secrets in an approved secret manager or local environment, never Git.
- Keep machine inventories, exact local paths, logs, databases, credentials,
  and private project records outside this repository.
- A manifest records routing metadata; it does not authorize copying project
  contents across ownership boundaries.
- Public examples and tests use synthetic identifiers and reserved example
  domains only.
- Private repository visibility is access control, not permission to publish or
  proof that content is sanitized.
- When disclosure safety is uncertain, leave the material with its source owner
  and require human review.

Before delivery, run `tools/audit_publication.py`, inspect all tracked files,
and review the staged diff. A clean automated result never replaces ownership
and disclosure review.
