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
- [x] Audit GitHub Actions that are gated to `tensorzero/tensorzero`.
- [ ] Configure Agentify container publishing for CI images.
- [ ] Set `ENABLE_DOCKER_CI=true` after Agentify container publishing is configured.
- [ ] Set `ENABLE_LIVE_PROVIDER_CRONS=true` after live-provider secrets are configured.
- [ ] Configure Agentify release publishing for Docker, PyPI, and Helm artifacts.
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
- configure Agentify container publishing for CI images
- set `ENABLE_DOCKER_CI=true` after Agentify container publishing is configured
- configure live-provider cron secrets before setting `ENABLE_LIVE_PROVIDER_CRONS=true`
- configure Agentify release publishing for Docker, PyPI, and Helm artifacts
- decide package, Docker, Helm, and docs publishing namespaces
- cut the first no-feature custody release

Security reports should follow `SECURITY.md`.
```
