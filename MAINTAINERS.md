# Maintainers

This repository is the Agentify-maintained community fork of TensorZero.
The upstream `tensorzero/tensorzero` repository was archived on June 12, 2026 and is now read-only.

## Current maintainers

- Agentify maintainers, reachable at team@agentify.sh

## Maintenance policy

The initial maintenance scope is intentionally conservative:

- keep the gateway, UI, clients, docs, and examples buildable
- fix security issues and dependency vulnerabilities
- keep provider integrations compatible with current provider APIs
- review community bug fixes and small compatibility improvements
- preserve Apache-2.0 licensing, source history, and upstream attribution

Large feature work, package renames, release namespace changes, and compatibility-breaking API changes should start with a GitHub issue before implementation.

## Review expectations

- Security-sensitive changes require maintainer review.
- Release, CI, auth, database migration, and provider integration changes require extra scrutiny.
- Compatibility changes should include tests or a clear explanation when tests are not practical.
