# Maintenance Transition

This repository is the Agentify-maintained community fork of TensorZero.
The upstream `tensorzero/tensorzero` repository was archived on June 12, 2026 and is now read-only.

## Immediate priorities

- [x] Preserve source history and Apache-2.0 attribution.
- [x] Mark this repository as the maintained community fork.
- [x] Replace upstream-only security and support contacts.
- [ ] Enable GitHub private vulnerability reporting.
- [ ] Configure branch protection for `main`.
- [ ] Decide whether GitHub Discussions should be enabled.
- [ ] Replace upstream CODEOWNERS with Agentify-owned teams or maintainers.
- [ ] Audit GitHub Actions that are gated to `tensorzero/tensorzero`.
- [ ] Decide package and container publishing namespaces.
- [ ] Run a full baseline build and test pass.
- [ ] Publish a no-feature custody release from `agentify-sh/gateway`.

## Suggested pinned issue body

Title: `TensorZero maintenance transition`

Body:

```markdown
This repository is the Agentify-maintained community fork of TensorZero.
The upstream `tensorzero/tensorzero` repository was archived on June 12, 2026 and is now read-only.

Initial maintenance scope:

- security fixes
- provider compatibility fixes
- build and CI continuity
- documentation and example repairs
- conservative bug fixes

Open transition work:

- enable private vulnerability reporting
- configure branch protection for `main`
- replace upstream CODEOWNERS entries with Agentify owners
- audit GitHub Actions gated to `tensorzero/tensorzero`
- decide package, Docker, Helm, and docs publishing namespaces
- cut the first no-feature custody release

Security reports should follow `SECURITY.md`.
```
