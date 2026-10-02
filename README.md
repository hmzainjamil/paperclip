# Paperclip

Paperclip is a control plane for AI-agent companies. It gives a human operator a place to organize companies, goals, agents, issues, budgets, approvals, and execution status. Agents run through configured local adapters, commands, HTTP integrations, gateways, or plugins; Paperclip coordinates and records that work.

## Repository status

This checkout is a TypeScript and React pnpm monorepo. The root manifest requires Node.js 20 or newer and pins pnpm 9.15.4. Workspace packages are versioned separately. Several package manifests point to the upstream repository `paperclipai/paperclip`; verify provenance and release status from the checkout and package metadata you use.

This README describes repository structure and commands. It does not certify a release, production deployment, security review, or passing test suite.

## Capabilities in the codebase

- Company, goal, agent, issue, project, comment, and activity management.
- Agent adapters for local coding tools and other supported execution paths.
- Heartbeat runs with status and transcript/activity visibility.
- Budget tracking, approvals, and operator controls.
- PostgreSQL-backed persistence, with embedded PostgreSQL available for local development.
- React board UI and a `paperclipai` command-line interface.
- Plugin SDK, plugin host packages, examples, and MCP server package.

See [doc/SPEC-implementation.md](./doc/SPEC-implementation.md) for the concrete V1 contract and [doc/PRODUCT.md](./doc/PRODUCT.md) for product concepts. These documents describe intended behavior; check implementation and verification evidence for current runtime guarantees.

## Local development

Prerequisites: Node.js 20+ and pnpm 9+.

```sh
pnpm install
pnpm dev
```

The development runner starts the API and serves the UI from the same origin at `http://localhost:3100`. With `DATABASE_URL` unset, local development uses embedded PostgreSQL and stores data under the Paperclip instance directory. Review [doc/DATABASE.md](./doc/DATABASE.md) before changing database mode or handling persisted data.

For first-run setup and diagnostics:

```sh
pnpm paperclipai onboard
pnpm paperclipai doctor
```

Onboarding writes instance configuration and can select reachability and authentication settings. Read [doc/DEPLOYMENT-MODES.md](./doc/DEPLOYMENT-MODES.md) before exposing the server beyond a trusted local machine.

## Deployment and security

Paperclip supports `local_trusted` and `authenticated` runtime modes. Authenticated mode supports private or public exposure policies. The bind address is configured separately. The default local-trusted mode is intended for local loopback use and does not require human login.

Do not expose a local-trusted instance to a network. For shared or public access, configure authenticated mode and review the deployment, authentication, secrets, and database guidance first.

Paperclip can start local agent CLIs or send data to remote adapters, model providers, MCP servers, and plugins. Those systems may receive prompts, issue content, credentials, files, or other configured data. Use least-privilege credentials, inspect adapter/plugin configuration, and protect the instance database, secret key, workspaces, and logs. See [SECURITY.md](./SECURITY.md).

## Repository map

| Path | Purpose |
|---|---|
| `server/` | API server and orchestration services |
| `ui/` | Board application |
| `cli/` | `paperclipai` command-line application |
| `packages/db/` | Drizzle schema, migrations, and database client |
| `packages/shared/` | Shared types, API paths, and validation |
| `packages/adapters/` | Built-in execution adapters |
| `packages/plugins/` | Plugin SDK, host integration, and examples |
| `packages/mcp-server/` | MCP wrapper over the Paperclip REST API |
| `doc/` | Product, implementation, operator, deployment, and release documentation |
| `evals/` | Agent behavior evaluation configuration |

Start at [doc/README.md](./doc/README.md) for the canonical documentation map. Package READMEs describe their individual adapters, CLI, UI, plugin, and evaluation surfaces.

## Checks

The root scripts define the available commands:

```sh
pnpm typecheck
pnpm test
pnpm build
```

Browser and release smoke suites are separate opt-in commands. A checked-in script or workflow is not evidence that it passed. No install, build, test, or deployment was run for this documentation change.

## License and contribution

The root [LICENSE](./LICENSE) is MIT. Follow [CONTRIBUTING.md](./CONTRIBUTING.md) for contribution guidance and [SECURITY.md](./SECURITY.md) for vulnerability reporting.
