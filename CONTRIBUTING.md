# Contributing to Agentify Gateway

Thank you for your interest in contributing to Agentify Gateway.

This repository is derived from the archived TensorZero project.
The upstream `tensorzero/tensorzero` repository was archived on June 12, 2026 and is now read-only.
Please target contributions at `agentify-sh/gateway` unless a maintainer says otherwise.

Agentify Gateway aims to provide a practical, open-source LLM gateway and LLMOps stack.
We'd love to collaborate with you to make this vision a reality.

## License

Agentify Gateway is licensed under the [Apache 2.0 license](LICENSE).
By contributing to this repository, you agree to license your contributions under the same license.

## Community & Support

### GitHub

We use GitHub Issues to track bugs and feature requests.
For general questions, technical support, and conversations not directly related to code, please open an issue and use the `question` label.

## Contributions

> [!TIP]
>
> See the [`good-first-issue`](https://github.com/agentify-sh/gateway/issues?q=is%3Aopen+is%3Aissue+label%3Agood-first-issue) label for simpler issues that might be a good starting point for new contributors.

### Code

For small changes (i.e. a few lines of code), feel free to open a PR directly.

For larger changes, please communicate with us first to avoid duplicate work or wasted effort.
Open an issue as a starting point.
The team will be happy to provide feedback and guidance.

At this time, we don't assign issues to new external contributors (in the past, most people we assigned issues to never submitted a PR).
Please submit a PR directly once you're ready to start working on an issue.

> [!TIP]
>
> See the "Technical Guide" section below for more details on building and testing Agentify Gateway.

### Documentation

The content for our documentation lives in the `docs/` directory.

For small changes (e.g. typos), feel free to open a PR directly.

For larger changes, please communicate with us first to avoid duplicate work or wasted effort.
Open an issue as a starting point.

### Content — Examples, Tutorials, etc.

We'd love to collaborate on examples, tutorials, and other content that showcases how to build AI applications with Agentify Gateway.

For content contributed directly to our repository, please follow the same process as code contributions.

For external content (e.g. blog posts, videos, social media content), we're excited to support and amplify your work.
Open an issue if you'd like technical review or feedback before publishing.

We're happy to provide guidance and support for both types of content to help you create high-quality resources for the Agentify Gateway community.

### Integrations

We're open to exploring integrations with other projects and tools (both open-source and commercial).
Reach out if you're interested in collaborating.

### Security

If you discover a security vulnerability, please follow [SECURITY.md](SECURITY.md).

### Other

Did you have something else in mind? Open an issue and let us know.

---

## Technical Guide

### Setup

- Install Rust (1.80+) [→](https://www.rust-lang.org/tools/install)
- Install `cargo-deny` [→](https://github.com/EmbarkStudios/cargo-deny)
- Install `cargo-nextest` [→](https://nexte.st/docs/installation/pre-built-binaries/)
- Install `pre-commit` [→](https://pre-commit.com/#install)
- Enable `pre-commit` in your repository: `pre-commit install`
- Install Docker [→](https://docs.docker.com/get-docker/)
- Install `uv` [→](https://docs.astral.sh/uv/)
- Install Python (3.10+) (e.g. `uv python install 3.10` + )
- Install Node.js (we use v24.13.0) and `npm` [→](https://nodejs.org/en)
- Install pnpm `npm install -g pnpm@10.15.0` [→](https://pnpm.io/installation)

**macOS users:** If you see Rust build errors about missing dynamic libraries for Python, set up a Python virtual environment at `tensorzero/.venv` (e.g. `uv venv` from the `tensorzero` directory)
This ensures the correct Python libraries are available for the build.

### Tests

#### Rust Unit Tests

```bash
cargo test-unit
```

#### Rust E2E Tests with ClickHouse

1. Launch the test containers

   ```bash
   docker compose -f crates/tensorzero-core/tests/e2e/docker-compose.yml up --wait
   ```

2. Set the relevant environment variables (`TENSORZERO_CLICKHOUSE_URL` and model provider API keys like `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, etc.). See the [credential docs](docs/deployment/tensorzero-gateway.mdx#set-up-model-provider-credentials) for the full list.

3. Launch the gateway in testing mode

   ```bash
   cargo run-e2e
   ```

4. Run the E2E tests
   ```bash
   cargo test-e2e
   ```

> [!TIP]
>
> The E2E tests involve every supported model provider, so you need every possible credential to run the entire test suite.
>
> If your changes don't affect every provider, you can run a subset of tests with `cargo test-e2e xyz`, which will only run tests with `xyz` in their name.

#### Rust E2E Tests with Postgres

1. Launch the test containers

   ```bash
   docker compose -f crates/tensorzero-core/tests/e2e/docker-compose.yml up --wait
   ```

2. Set the relevant environment variables (`TENSORZERO_CLICKHOUSE_URL` and model provider API keys like `OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, etc.). See the [credential docs](docs/deployment/tensorzero-gateway.mdx#set-up-model-provider-credentials) for the full list.

3. Launch the gateway in testing mode

   ```bash
   cargo run-e2e-postgres
   ```

4. Run the E2E tests
   ```bash
   TENSORZERO_INTERNAL_TEST_OBSERVABILITY_BACKEND=postgres cargo test-e2e
   ```

#### Python

1. Launch ClickHouse and the gateway in E2E testing mode (see above).

2. Go to the relevant directory (e.g. `cd clients/python`)

3. Install the Python dependencies. We recommend using [`uv`](https://github.com/astral-sh/uv).

   ```bash
   uv sync
   ```

4. Run the tests

   ```bash
   uv run pytest
   ```

5. Run the type checker

   ```bash
   uv pip install pyright
   uv run pyright
   ```

6. Run the formatter

   ```bash
   uv pip install ruff
   uv run ruff format --check .
   uv run ruff check --output-format=github --extend-select I .
   ```

#### Agentify Gateway UI

The UI depends on ClickHouse and other gateway components.
For development, we recommend running the gateway and ClickHouse as containers.
We also provide fixtures in `ui/fixtures/`.

To set it up, follow these steps from the repository's root directory:

1. Install dependencies: `pnpm install`
2. Build the internal N-API client using `pnpm -r build`. If you have changed your Rust code, you may also have to run `pnpm build-bindings`.
3. Create a `ui/fixtures/.env` following the `ui/fixtures/.env.example`.
4. Create a `ui/.env` following the `ui/.env.example`, or set the environment variables from that file in your shell before running the dev script.
5. Launch the dependencies:

   ```bash
   # For local development without R2 credentials (downloads via public HTTP):
   TENSORZERO_DOWNLOAD_FIXTURES_WITHOUT_CREDENTIALS=1 docker compose -f ui/fixtures/docker-compose.yml up --build --force-recreate

   # With R2 credentials (faster S3 sync, used in CI):
   docker compose -f ui/fixtures/docker-compose.yml up --build --force-recreate
   ```

   You can omit the `--build --force-recreate` flags to skip the build step, but they ensure you're using the latest gateway.

6. Launch the development server: `pnpm ui:dev`

Separately, you can run headless tests with `pnpm ui:test` and Playwright tests with `pnpm ui:test:e2e` (the latter will require a `pnpm exec playwright install`).

We also maintain a Docker Compose for e2e tests `ui/fixtures/docker-compose.e2e.yml` that is used in CI for the Playwright tests. This file uses a different configuration that mandates credentials for image fetching.

##### Autopilot Tests (Internal Only)

> [!NOTE]
>
> The Autopilot feature depends on a closed-source internal API. The tests in `ui/e2e_tests/autopilot/` require access to the private `autopilot` repository and cannot be run by external contributors. These tests are excluded by default and run in CI via repository dispatch from the autopilot repo.

For internal contributors with access to the autopilot repository, see `ui/AGENTS.md` for detailed instructions on running the autopilot development environment and tests.

### Advanced

- To test batch and optimization workflows without real provider APIs, spin up the `mock-provider-api` and set `TENSORZERO_INTERNAL_MOCK_PROVIDER_API=http://localhost:3030` when running the gateway.
- If your code affects the serialization of stored data, batch tests might fail because they'll rely on an older serialization of the request. In such cases, maintainers may need to refresh the shared test data before re-running the tests.

---

Thanks again for your interest in contributing to Agentify Gateway.
