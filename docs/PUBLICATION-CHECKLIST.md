# Public publication checklist

This checklist is a human gate. Automated checks cannot approve publication.

- [ ] Confirm every tracked file is owned by the repository owner or is
  otherwise licensed for publication.
- [ ] Review the complete diff and every Git object, not only the working tree.
- [ ] Confirm no secrets, credentials, cookies, keys, `.env` data, or auth
  metadata are present.
- [ ] Confirm no real workspace inventory, machine path, user account, email,
  private remote, project codename, organization name, customer data, or
  personal record is present.
- [ ] Confirm all examples, paths, identities, URLs, and datasets are synthetic.
- [ ] Confirm excluded source capabilities are not implied or claimed.
- [ ] Run every command in `docs/VERIFICATION.md` from a clean checkout of the
  exact candidate commit.
- [ ] Run an independent secret scanner and review all results.
- [ ] Select and review an open-source license; no license is granted today.
- [ ] Review repository description, topics, issue templates, Actions,
  collaborators, branch controls, and security settings.
- [ ] Decide whether Issues and Actions should remain enabled for a public repo.
- [ ] Confirm GitHub Pages remains disabled.
- [ ] Confirm there are no releases, packages, deployments, or public forks.
- [ ] Obtain explicit human approval for the exact commit SHA before changing
  visibility.
- [ ] After any approved visibility change, recheck rendered files, repository
  metadata, Pages, releases, packages, collaborators, and the default branch.

Until every applicable item is complete and the owner explicitly approves the
exact candidate, the repository must remain Private.
