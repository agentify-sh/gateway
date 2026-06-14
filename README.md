# Agentify Gateway

Agentify Gateway is a community-maintained project derived from the Apache-2.0 licensed TensorZero codebase.
It provides an open-source LLM gateway, observability layer, evaluation tooling, optimization workflows, and experimentation primitives for production LLM applications.

> [!IMPORTANT]
>
> This repository is maintained by Agentify at `agentify-sh/gateway`.
> It is derived from the upstream `tensorzero/tensorzero` repository, which was archived on June 12, 2026 and is now read-only.
> The TensorZero name, logo, and other marks belong to their respective owners; this fork uses the name only for attribution and compatibility context.

## What It Includes

- **Gateway:** access major LLM providers through one OpenAI-compatible API.
- **Observability:** store inferences and feedback in your own database.
- **Evaluation:** benchmark individual inferences or end-to-end workflows.
- **Optimization:** use production metrics and feedback to improve prompts, models, and inference strategies.
- **Experimentation:** ship routing, fallbacks, retries, and A/B tests with explicit configuration.

The codebase currently retains TensorZero protocol names, environment variables, package names, crate names, and model strings where changing them would be a breaking compatibility migration.
Those names should be treated as compatibility surfaces, not as current project branding.

## Links

- [Repository](https://github.com/agentify-sh/gateway)
- [Issues](https://github.com/agentify-sh/gateway/issues)
- [Security](SECURITY.md)
- [Contributing](CONTRIBUTING.md)
- [Maintainers](MAINTAINERS.md)
- [Maintenance transition](MAINTENANCE.md)
- [Quick Start](docs/quickstart.mdx)
- [Deployment Guide](docs/deployment/tensorzero-gateway.mdx)
- [Configuration Reference](docs/gateway/configuration-reference.mdx)

## Usage Example

You can use Agentify Gateway with OpenAI-compatible SDKs.
The compatibility model strings still use the existing `tensorzero::...` prefix.

```python
from openai import OpenAI

client = OpenAI(base_url="http://localhost:3000/openai/v1", api_key="not-used")

response = client.chat.completions.create(
    model="tensorzero::model_name::anthropic::claude-sonnet-4-6",
    messages=[
        {
            "role": "user",
            "content": "Share a useful fact about LLM gateways.",
        }
    ],
)
```

## Supported Provider Families

The gateway includes integrations for Anthropic, AWS Bedrock, AWS SageMaker, Azure, DeepSeek, Fireworks, GCP Vertex AI, Google AI Studio, Groq, Hyperbolic, Mistral, OpenAI, OpenRouter, SGLang, TGI, Together AI, vLLM, xAI, and OpenAI-compatible APIs such as Ollama.

See the local `docs/` directory for provider setup and configuration details.

## Maintenance Status

Agentify is currently focused on conservative maintenance:

- security fixes
- provider compatibility fixes
- build and CI continuity
- documentation and example repairs
- small, well-tested bug fixes

Release publishing, package namespaces, Docker image names, and deeper runtime renames are being handled separately because they affect existing users and automation.

## Attribution

Agentify Gateway is derived from TensorZero and preserves the upstream Apache-2.0 license, source history, and attribution.
Historical TensorZero documentation, blog posts, examples, package names, and protocol names may still appear where they are required for attribution, compatibility, or migration.

Upstream project:

- Repository: `tensorzero/tensorzero`
- License: Apache-2.0
- Archived: June 12, 2026
