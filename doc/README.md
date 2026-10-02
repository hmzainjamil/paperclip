# Documentation map

Use this page to find the maintained project guidance. The docs under `doc/` have different roles; product vision, implementation contracts, operational instructions, and plans are not interchangeable.

## Product and implementation

| Document | Role |
|---|---|
| [GOAL.md](./GOAL.md) | Product vision and control-plane goal |
| [PRODUCT.md](./PRODUCT.md) | Product concepts, principles, and user model |
| [SPEC.md](./SPEC.md) | Long-horizon technical and product context |
| [SPEC-implementation.md](./SPEC-implementation.md) | Concrete V1 implementation contract; repository guidance says this controls when it conflicts with the long-horizon spec |
| [TASKS.md](./TASKS.md) | Task model and hierarchy |
| [execution-semantics.md](./execution-semantics.md) | Issue ownership, checkout, execution, and recovery behavior |

## Setup and operations

| Document | Role |
|---|---|
| [DEVELOPING.md](./DEVELOPING.md) | Local prerequisites, development runner, and checks |
| [CLI.md](./CLI.md) | Command-line reference |
| [DATABASE.md](./DATABASE.md) | Database modes, migrations, backups, and secret storage |
| [DEPLOYMENT-MODES.md](./DEPLOYMENT-MODES.md) | Auth, exposure, and bind model |
| [DOCKER.md](./DOCKER.md) | Docker and Compose workflows |
| [SECRETS-AWS-PROVIDER.md](./SECRETS-AWS-PROVIDER.md) | AWS-backed secret provider |
| [UNTRUSTED-PR-REVIEW.md](./UNTRUSTED-PR-REVIEW.md) | Isolated review workflow |

## Release, plugins, and integrations

| Document | Role |
|---|---|
| [RELEASING.md](./RELEASING.md) | Release procedure |
| [PUBLISHING.md](./PUBLISHING.md) | Package publication |
| [RELEASE-AUTOMATION-SETUP.md](./RELEASE-AUTOMATION-SETUP.md) | Release automation setup |
| [TASKS-mcp.md](./TASKS-mcp.md) | MCP and task integration notes |
| [OPENCLAW_ONBOARDING.md](./OPENCLAW_ONBOARDING.md) | OpenClaw adapter onboarding |
| [CLIPHUB.md](./CLIPHUB.md) | ClipHub product context |

Plugin design documents are grouped under [plugins/](./plugins/). Plans are grouped under [plans/](./plans/), and specifications under [spec/](./spec/).

## Status and source of truth

For a code change, check the relevant implementation and tests as well as its documentation. A proposal, inventory, roadmap, or specification describes intent or scope; it does not establish that behavior is implemented or verified. Some documents contain dates and evolving deployment, dependency, or provider details. Confirm current source and manifests before relying on them.

[`README-draft.md`](./README-draft.md) is explicitly a draft. Do not treat it as canonical guidance.
