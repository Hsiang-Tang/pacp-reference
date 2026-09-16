# Public maintenance checklist

The initial publication gate was completed by the owner on 2026-09-16. Keep
this checklist as a repeatable gate for material changes; automated checks
cannot approve ownership or disclosure.

- [x] Confirm every tracked file is owned by the repository owner or is
  otherwise licensed for publication.
- [x] Review the complete diff and every Git object, not only the working tree.
- [x] Confirm no secrets, credentials, cookies, keys, `.env` data, or auth
  metadata are present.
- [x] Confirm no real workspace inventory, machine path, user account, email,
  private remote, project codename, organization name, customer data, or
  personal record is present.
- [x] Confirm all examples, paths, identities, URLs, and datasets are synthetic.
- [x] Confirm excluded source capabilities are not implied or claimed.
- [x] Run every command in `docs/VERIFICATION.md` from a clean checkout of the
  exact candidate commit.
- [x] Run an independent hosted secret scan and review all results.
- [x] Select and review the MIT open-source license.
- [x] Review repository description, topics, issue templates, Actions,
  collaborators, branch controls, and security settings.
- [x] Confirm hosted Actions workflows remain absent unless a separately
  reviewed publication plan deliberately adds them.
- [x] Confirm GitHub Pages remains disabled.
- [x] Confirm there are no releases, packages, deployments, or public forks.
- [x] Obtain explicit owner approval for public visibility.
- [x] After the visibility change, recheck rendered files, repository
  metadata, Pages, releases, packages, collaborators, and the default branch.

For future material changes, repeat every applicable check before push and
again against the exact public commit.
