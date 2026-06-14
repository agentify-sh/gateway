# Agentify Gateway Docs

Agentify Gateway uses [Mintlify](https://mintlify.com) for its documentation.
Some generated documentation paths and examples still use upstream TensorZero names for compatibility.

## Setup

Install dependencies from the `docs/` directory:

```bash
cd docs
pnpm install
```

## Local Development

Launch a local preview:

```bash
pnpm exec mint dev
```

## Check for Broken Links

```bash
pnpm exec mint broken-links --check-anchors
```
