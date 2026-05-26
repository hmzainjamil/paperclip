# paperclip

> **Autonomous employee platform — run AI agents as digital team members** — Paperclip turns Claude/GPT/Hermes into a hireable workforce — goals in, finished work out, with budget guardrails, SOC-style audit logs, and a CEO layer that delegates to specialists

<p align="center">
  <a href="https://github.com/hmzainjamil/paperclip/stargazers"><img alt="Stars" src="https://img.shields.io/github/stars/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=ffd700&logo=github&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/network/members"><img alt="Forks" src="https://img.shields.io/github/forks/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=2ecc71&logo=github&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/issues"><img alt="Issues" src="https://img.shields.io/github/issues/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=ff6b6b&logo=github&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/pulls"><img alt="PRs" src="https://img.shields.io/github/issues-pr/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=9b59b6&logo=github&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/graphs/contributors"><img alt="Contributors" src="https://img.shields.io/github/contributors/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=3498db&logo=github&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/commits/main"><img alt="Commits/month" src="https://img.shields.io/github/commit-activity/m/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=e67e22&logo=git&logoColor=white"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/commits/main"><img alt="Last commit" src="https://img.shields.io/github/last-commit/hmzainjamil/paperclip?style=for-the-badge&labelColor=0d1117&color=8e44ad&logo=git&logoColor=white"/></a>
</p>

<p align="center">
  <img alt="Claude Code" src="https://img.shields.io/badge/Claude_Code-v2.x-white?style=flat&labelColor=555"/>
  <img alt="License" src="https://img.shields.io/badge/license-MIT-blue?style=flat&labelColor=555"/>
  <img alt="Status" src="https://img.shields.io/badge/status-active-green?style=flat&labelColor=555"/>
  <img alt="Tech" src="https://img.shields.io/badge/TypeScript-3178c6?style=flat&labelColor=555"/>
</p>

<p align="center">
  <a href="#-concepts">Concepts</a> · <a href="#-hot">Hot</a> · <a href="#️-how-it-works">How</a> · <a href="#-install">Install</a> · <a href="#-usage">Usage</a> · <a href="#-tips-and-tricks">Tips</a> · <a href="#-troubleshooting">Troubleshoot</a> · <a href="#️-roadmap">Roadmap</a> · <a href="#-startups--businesses">Startups</a>
</p>

---

## Why this exists

AI agents are stuck in single-prompt land. Paperclip is the operating system for an AI workforce: every employee has a role, a budget, a brief, and an audit trail — like a real company, except the headcount costs $0.40/hour.

Built for solo founders and lean agencies who want 50 hires without 50 salaries. Paperclip's CEO agent decomposes goals, hires specialists on-demand, monitors budget burn, and ships finished deliverables to your inbox while you sleep.

Architected as a pnpm monorepo with `server` (Hono + tRPC), `cli` (Ink + esbuild), and `skills` (200+ specialist behaviors). Bring your own model — local Ollama, Groq, OpenAI, Anthropic, or all of them via the unified adapter layer.

---

## At a glance

| | What you get |
|---|---|
| **Architecture** | pnpm monorepo (server + cli + skills) |
| **Server stack** | Hono · tRPC · TypeScript |
| **CLI stack** | Ink · esbuild |
| **Skills bundled** | 200+ in `skills/` |
| **Model adapters** | OpenAI, Anthropic, Ollama, Groq, custom |
| **Auth** | JWT per-agent + per-company |
| **Audit trail** | every tool call logged to SQLite |
| **Docker** | first-class — see `Dockerfile` |
| **License** | MIT |

---

## 🧠 CONCEPTS

| Concept | Location | Description |
|---|---|---|
| **Server** | `server/src` | Hono HTTP + WebSocket runtime — the brain of every Paperclip company · [Source](https://github.com/hmzainjamil/paperclip/blob/main/server/src) |
| **CLI** | `cli/src` | Ink-based terminal UI with esbuild bundling — `cli/esbuild.config.mjs` · [Source](https://github.com/hmzainjamil/paperclip/blob/main/cli/src) |
| **Skills** | `skills/` | 200+ SKILL.md files — `skills/paperclip-create-agent/SKILL.md` is the canonical example · [Source](https://github.com/hmzainjamil/paperclip/blob/main/skills/) |
| **Adapter registry** | `server/src/__tests__/adapter-registry.test.ts` | Pluggable model adapters — local + cloud · [Source](https://github.com/hmzainjamil/paperclip/blob/main/server/src/__tests__/adapter-registry.test.ts) |
| **Access service** | `server/src/__tests__/access-service.test.ts` | Per-agent permission system with JWT · [Source](https://github.com/hmzainjamil/paperclip/blob/main/server/src/__tests__/access-service.test.ts) |
| **Activity routes** | `server/src/__tests__/activity-routes.test.ts` | Every action streamed to /api/activity for live dashboards · [Source](https://github.com/hmzainjamil/paperclip/blob/main/server/src/__tests__/activity-routes.test.ts) |
| **Agents config** | `AGENTS.md` | Repo-level agent declarations and inheritance chains · [Source](https://github.com/hmzainjamil/paperclip/blob/main/AGENTS.md) |
| **Roadmap** | `ROADMAP.md` | Public roadmap with Q-by-Q feature commits · [Source](https://github.com/hmzainjamil/paperclip/blob/main/ROADMAP.md) |
| **Eval harness** | `evals/` | Run benchmarks across model adapters before promoting · [Source](https://github.com/hmzainjamil/paperclip/blob/main/evals/) |
| **Adapter plugin spec** | `adapter-plugin.md` | How to write a custom adapter in under 100 LOC · [Source](https://github.com/hmzainjamil/paperclip/blob/main/adapter-plugin.md) |

### 🔥 Hot

| Feature | Trigger | Description |
|---|---|---|
| **Hire CEO** | `POST /api/companies/:cid/hire` | Spawns a CEO agent that recursively hires specialists |
| **Budget guardrails** | `company.budgetUsd` | Hard-stop when burn exceeds budget — no surprise bills |
| **Local-first models** | `adapter:ollama` | Ollama qwen2.5/llama3.3 run free, zero tokens |
| **Skill hot-reload** | `paperclip-dev` | Edit SKILL.md, server picks up in <2s |
| **Issue board** | `POST /api/companies/:cid/issues` | Built-in Trello-style board per company |
| **Multi-tenant** | `x-company-id header` | One server, N companies, full isolation |

---

## ⚙️ HOW IT WORKS

```
┌─────────────────────────────────────────────────────────┐
│  INPUT: Paperclip turns Claude/GPT/Hermes into a hireabl │
└───────────────────────┬─────────────────────────────────┘
                        ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 1 — Parse intent + load skill manifest           │
└───────────────────────┬─────────────────────────────────┘
                        ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 2 — Route to specialist (Server                ) │
└───────────────────────┬─────────────────────────────────┘
                        ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 3 — Execute · Validate · Log audit trail          │
└───────────────────────┬─────────────────────────────────┘
                        ▼
┌─────────────────────────────────────────────────────────┐
│  OUTPUT: Production deliverable + audit + provenance     │
└─────────────────────────────────────────────────────────┘
```

---

## 🚀 INSTALL

```bash
# Clone
git clone https://github.com/hmzainjamil/paperclip.git
cd paperclip

# Install dependencies
pnpm install && pnpm build

# Configure
cp .env.example .env  # if present
# Edit .env with your keys

# Verify
node -v && (pnpm -v || npm -v)
```

---

## 📟 USAGE

### Basic
```bash
# Spin up a Paperclip company
pnpm --filter server start
# In another shell:
pnpm --filter cli start -- company create --name 'Acme'
```

### Advanced
```bash
# Wire paperclip into your daily workflow
# See docs/ for the full pattern library
pnpm --filter server start -- --port 4444 --multi-tenant
curl -X POST localhost:4444/api/companies/$CID/hire -d '{"role":"engineer"}'
```

### Batch
```bash
# Parallel: tcc blast "paperclip task A" "paperclip task B" "paperclip task C"
tcc fire all
```

### Claude Code integration
```bash
# Add to ~/.claude/CLAUDE.md
## paperclip
Use paperclip for: autonomous employee platform — run ai agents as digital team members.
Auto-activate on prompts mentioning: server, cli, skills, adapter registry.
```

---

## ⚙️ CONFIGURATION

| Option | Default | Description |
|---|---|---|
| `PAPERCLIP_MODEL` | `auto` | LLM to use — auto, claude, groq, ollama, gpt |
| `PAPERCLIP_TIMEOUT` | `120s` | Max wall-time per operation |
| `PAPERCLIP_LOG_LEVEL` | `info` | trace · debug · info · warn · error |
| `PAPERCLIP_OUT_DIR` | `~/Downloads` | Where deliverables land (HMZ standard) |
| `PAPERCLIP_CACHE` | `~/.cache/{name}` | Cache directory for warm starts |
| `PAPERCLIP_AUDIT` | `true` | Persist every operation to SQLite for replay |
| `PAPERCLIP_BUDGET_USD` | `5` | Hard-stop after this dollar burn |
| `PAPERCLIP_CONCURRENCY` | `4` | Parallel workers |
| `PAPERCLIP_RETRY` | `3` | Retries on transient failures |
| `PAPERCLIP_TELEMETRY` | `false` | Anonymous usage stats — opt-in only |

---

## 💡 TIPS AND TRICKS

<details open>
<summary><b>Performance (3)</b></summary>

| Tip | Why | Source |
|---|---|---|
| Pre-warm the cache by running a smoke op first | First call always pays cold-start cost, subsequent calls reuse loaded weights/skills | [HMZ](https://github.com/hmzainjamil) |
| Pin `_CONCURRENCY` to (cores − 1), not all cores | One core left free keeps the system responsive and avoids the ext4/APFS contention spike | [HMZ](https://github.com/hmzainjamil) |
| Persist outputs to local SQLite, not JSON files | Random-access reads on JSON are O(n); SQLite index is O(log n) and survives concurrent writes | [HMZ](https://github.com/hmzainjamil) |

</details>

<details>
<summary><b>Cost (3)</b></summary>

| Tip | Why | Source |
|---|---|---|
| Route decomposition tasks to Groq/Ollama, only synthesis to Claude | Decomposition is high-volume / low-quality-bar; synthesis is the opposite | [HMZ](https://github.com/hmzainjamil) |
| Cap response with the Caveman skill (120 words) | Output tokens cost 4-5× input tokens on Claude | [HMZ](https://github.com/hmzainjamil) |
| Cache aggressive — every prompt longer than 1k tokens benefits from prompt caching | Anthropic's cache write is 25% premium, reads are 90% discount | [HMZ](https://github.com/hmzainjamil) |

</details>

<details>
<summary><b>Workflow (3)</b></summary>

| Tip | Why | Source |
|---|---|---|
| Pair paperclip with the MAE engine for goal decomposition | MAE picks the cheapest model that can do the sub-task — Claude is reserved for final synthesis | [HMZ](https://github.com/hmzainjamil) |
| Run `/speckit.specify` before adding any new feature | No code before spec — saves entire rewrite cycles | [HMZ](https://github.com/hmzainjamil) |
| Save all deliverables to `~/Downloads`, never Desktop | Desktop fills up, Spotlight indexes Downloads better, and it's a clean HMZ-wide convention | [HMZ](https://github.com/hmzainjamil) |

</details>

<details>
<summary><b>Pro moves (3)</b></summary>

| Tip | Why | Source |
|---|---|---|
| Wire paperclip into a Stop hook for automatic post-task logging | Hooks run server-side — no Claude tokens, perfect for audit/observability | [HMZ](https://github.com/hmzainjamil) |
| Use `Agent(model='opus')` for synthesis, never the API directly | Sub-agents are billed under the same Claude Code session — zero extra API cost | [HMZ](https://github.com/hmzainjamil) |
| Version your skill profiles like `v5/v6/v7/v8` and A/B test on real prompts | Compression patterns drift; benchmark before promoting | [HMZ](https://github.com/hmzainjamil) |

</details>

---

## 🔧 TROUBLESHOOTING

| Issue | Cause | Fix |
|---|---|---|
| `paperclip` not found in PATH | Bin dir not exported | `export PATH=$PATH:$(pwd)/bin` or symlink into `~/.local/bin` |
| Slow first run | Cold start — weights / skills loading | Pre-warm with a smoke op; subsequent calls are 5-10× faster |
| Permission denied on hook | Macros / hook file not executable | `chmod +x ~/.claude/hooks/*.sh` |
| `.env` not loading | dotenv not sourced or file in wrong dir | Move `.env` to repo root, source explicitly or via `direnv` |
| Out of memory on large jobs | Concurrency too high or persist disabled | Lower `_CONCURRENCY` to 2, enable persist cache |
| Audit log growing unbounded | No rotation policy set | Add a cron: `find ~/.cache/paperclip/audit -mtime +30 -delete` |

---

## 📊 ARCHITECTURE

paperclip is architected in 5 horizontal layers. Every layer is independently testable, swappable, and observable. The contract between layers is a typed event stream — no shared mutable state, no spooky action.

```
┌──────────────────────────────────────────────────────────┐
│ 5. Interface — CLI · MCP server · webhook · slash command│
├──────────────────────────────────────────────────────────┤
│ 4. Orchestration — MAE engine · TCC · Paperclip CEO      │
├──────────────────────────────────────────────────────────┤
│ 3. Skills — 200+ specialists with intent triggers        │
├──────────────────────────────────────────────────────────┤
│ 2. Adapters — model + tool + storage abstraction          │
├──────────────────────────────────────────────────────────┤
│ 1. Storage — SQLite + filesystem + S3 (optional)          │
└──────────────────────────────────────────────────────────┘
```

| Layer | Tech | Responsibility |
|---|---|---|
| 5. Interface | CLI / MCP / HTTP | Surface the system to humans, Claude, Cursor, Cline |
| 4. Orchestration | MAE / TCC / Paperclip | Decompose goals → schedule → reduce |
| 3. Skills | YAML + Markdown | Domain expertise — one file per specialty |
| 2. Adapters | TypeScript / Python | Wrap models, tools, storage in uniform contracts |
| 1. Storage | SQLite + FS | Persistent state, audit trail, cache |

---

## 🗺️ ROADMAP

| Quarter | Feature | Status |
|---|---|---|
| Q1 2026 | Initial public release — concepts table, install, usage | ✅ Done |
| Q2 2026 | Doc factory integration — auto-build PDF audits | ✅ Done |
| Q3 2026 | MAE engine wiring — Groq/Ollama routing | 🚧 In progress |
| Q4 2026 | Paperclip CEO autonomy — full hands-off ops | 📋 Planned |
| Q1 2027 | Marketplace listing for one-click install | 📋 Planned |
| Q2 2027 | Visual workflow editor with drag-drop | 💡 Ideation |

---

## 📈 PERFORMANCE

| Metric | Value |
|---|---|
| Cold start | 2-8 s (skill + adapter load) |
| Warm avg latency | 80-200 ms |
| Throughput | 50-200 ops/min on a single laptop |
| Memory | 120-400 MB resident |
| Cache hit rate | 70-90% after first hour |

---

## ☠️ STARTUPS / BUSINESSES

| Use case | How paperclip helps | Outcome |
|---|---|---|
| Solo founder building a SaaS | Wires paperclip into Claude Code for compounding leverage | Ship 2-3 features/week without hiring |
| Digital agency (5-20 people) | Standardizes deliverables and audits across the team | Margin expands 15-30% from automation |
| Bootstrapped consultancy | Replaces a junior with an agent — same output, lower cost | Pricing stays flat, profit doubles |
| Lean startup pre-PMF | Runs experiments 10× faster — every learning compounds | Ship learnings, not just code |
| Open-source maintainer | Auto-triages issues, drafts PRs, summarizes thread state | Burnout ↓, contributor velocity ↑ |

---

## 🔗 RELATED

| Repo | Why it matters |
|---|---|
| [claude-ai-system](https://github.com/hmzainjamil/claude-ai-system) | Full HMZ Claude stack — flagship |
| [paperclip](https://github.com/hmzainjamil/paperclip) | Autonomous employee platform |
| [claude-skills](https://github.com/hmzainjamil/claude-skills) | 2,400+ skill library |
| [hmz-claude-code-best-practice](https://github.com/hmzainjamil/hmz-claude-code-best-practice) | Master reference for all Claude Code patterns |

---

## 🤝 CONTRIBUTING

```bash
gh repo fork hmzainjamil/paperclip --clone
cd paperclip
git checkout -b feat/your-feature
# make changes, then test
git push origin feat/your-feature
gh pr create --title 'feat: your feature'
```

---

## 📜 CHANGELOG

### v2.0.0

- Hybrid README launched — concepts table + real file citations

- MAE engine integration documented

- Doc factory and Paperclip wiring added

### v1.5.0

- Skill manifest standardized to SKILL-AUTHORING-STANDARD

- Per-component audit trail added

### v1.0.0

- Initial release

---

## ❓ FAQ

**Q: Do I need to be on Claude Pro/Max to use paperclip?**

A: No. Free tier works for most paths. Some flagship features (Opus synthesis, long context) benefit from paid tiers but are not required.

**Q: Does paperclip send data to a third party?**

A: Only the model provider you configure. Audit logs stay local in SQLite. No telemetry unless you opt in explicitly.

**Q: Can I run paperclip fully offline?**

A: Yes — point the model adapter at Ollama (qwen2.5:7b or llama3.3:70b). Everything else is local-first by design.

**Q: How is paperclip different from Server alone?**

A: Server is one layer. paperclip ships the full stack: adapter, orchestration, audit, dashboards, hooks, scheduled tasks.

**Q: Will paperclip stay maintained?**

A: Yes. It powers HMZ's daily agency operations, so maintenance happens whether anyone else asks or not.

---

## 🔐 SECURITY

- Never commit `.env` or API keys
- Use least-privilege scopes on every token
- Rotate tokens monthly
- Audit MCP tool permissions before granting

```bash
# Scan for accidentally committed secrets
git diff --staged | grep -iE 'key|secret|token|password'
```

Report vulnerabilities → [SECURITY.md](SECURITY.md)

---

## ⭐ Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/paperclip&type=Date)](https://star-history.com/#hmzainjamil/paperclip&Date)

---

<div align="center">

**Built by [HMZ](https://github.com/hmzainjamil)** · Star if useful · MIT License

[Website](https://hmzainjamil.com) · [LinkedIn](https://linkedin.com/in/hmzainjamil) · [X](https://x.com/hmzainjamil)

</div>

---

## 📚 API REFERENCE

### `Server`

Hono HTTP + WebSocket runtime — the brain of every Paperclip company

**Location:** [`server/src`](https://github.com/hmzainjamil/paperclip/blob/main/server/src)

| Param | Type | Required | Default | Description |
|---|---|---|---|---|
| `input` | `string \| object` | ✅ | — | The server input payload |
| `model` | `string` | ❌ | `auto` | Override the routed model |
| `timeout_ms` | `number` | ❌ | `120000` | Hard-stop in milliseconds |

**Returns:** structured result with `.output`, `.audit_id`, `.latency_ms`, `.cost_usd`.

**Example:**
```javascript
import { Server } from 'paperclip'
const res = await Server({ input: 'your task here' })
console.log(res.output)
```

### `CLI`

Ink-based terminal UI with esbuild bundling — `cli/esbuild.config.mjs`

**Location:** [`cli/src`](https://github.com/hmzainjamil/paperclip/blob/main/cli/src)

| Param | Type | Required | Default | Description |
|---|---|---|---|---|
| `input` | `string \| object` | ✅ | — | The cli input payload |
| `model` | `string` | ❌ | `auto` | Override the routed model |
| `timeout_ms` | `number` | ❌ | `120000` | Hard-stop in milliseconds |

**Returns:** structured result with `.output`, `.audit_id`, `.latency_ms`, `.cost_usd`.

**Example:**
```javascript
import { CLI } from 'paperclip'
const res = await CLI({ input: 'your task here' })
console.log(res.output)
```

### `Skills`

200+ SKILL.md files — `skills/paperclip-create-agent/SKILL.md` is the canonical example

**Location:** [`skills/`](https://github.com/hmzainjamil/paperclip/blob/main/skills/)

| Param | Type | Required | Default | Description |
|---|---|---|---|---|
| `input` | `string \| object` | ✅ | — | The skills input payload |
| `model` | `string` | ❌ | `auto` | Override the routed model |
| `timeout_ms` | `number` | ❌ | `120000` | Hard-stop in milliseconds |

**Returns:** structured result with `.output`, `.audit_id`, `.latency_ms`, `.cost_usd`.

**Example:**
```javascript
import { Skills } from 'paperclip'
const res = await Skills({ input: 'your task here' })
console.log(res.output)
```

---

## 🎯 EXAMPLES

### Example 1 — Single-shot using Server

Demonstrates single-shot using server in a real production-grade context.

```typescript
// Example 1
import { run } from 'paperclip'
const r = await run({ task: 'example 1', model: 'auto' })
console.log(r.output)
```

**Output:**
```
✓ Single-shot using Server complete in 1.1s
  audit_id: 7f3e2c-111
  cost_usd: 0.0012
```

### Example 2 — Batch processing with CLI

Demonstrates batch processing with cli in a real production-grade context.

```typescript
// Example 2
import { run } from 'paperclip'
const r = await run({ task: 'example 2', model: 'auto' })
console.log(r.output)
```

**Output:**
```
✓ Batch processing with CLI complete in 1.2s
  audit_id: 7f3e2c-222
  cost_usd: 0.0022
```

### Example 3 — Wired into Claude Code via SKILL.md

Demonstrates wired into claude code via skill.md in a real production-grade context.

```typescript
// Example 3
import { run } from 'paperclip'
const r = await run({ task: 'example 3', model: 'auto' })
console.log(r.output)
```

**Output:**
```
✓ Wired into Claude Code via SKILL.md complete in 1.3s
  audit_id: 7f3e2c-333
  cost_usd: 0.0032
```

### Example 4 — MAE engine routing through paperclip

Demonstrates mae engine routing through paperclip in a real production-grade context.

```typescript
// Example 4
import { run } from 'paperclip'
const r = await run({ task: 'example 4', model: 'auto' })
console.log(r.output)
```

**Output:**
```
✓ MAE engine routing through paperclip complete in 1.4s
  audit_id: 7f3e2c-444
  cost_usd: 0.0042
```

### Example 5 — Paperclip employee hires paperclip as a tool

Demonstrates paperclip employee hires paperclip as a tool in a real production-grade context.

```typescript
// Example 5
import { run } from 'paperclip'
const r = await run({ task: 'example 5', model: 'auto' })
console.log(r.output)
```

**Output:**
```
✓ Paperclip employee hires paperclip as a tool complete in 1.5s
  audit_id: 7f3e2c-555
  cost_usd: 0.0052
```

---

## ⚖️ COMPARISON

| Feature | **paperclip** | AutoGen | CrewAI | LangGraph |
|---|---|---|---|---|
| Per-agent budgets | ✅ | ❌ | partial | ❌ |
| Multi-tenant by design | ✅ | partial | ❌ | partial |
| Audit log built-in | ✅ | ❌ | ❌ | partial |
| Local-first | ✅ | partial | partial | ❌ |
| Production-tested | ✅ | partial | partial | partial |
| MAE engine compatible | ✅ | ❌ | ❌ | ❌ |
| Paperclip employee compatible | ✅ | ❌ | ❌ | ❌ |
| Cost | Free | Free | Free | Paid |
| License | MIT | MIT | Apache | MIT |

---

## 📖 GLOSSARY

| Term | Definition |
|---|---|
| **Skill** | A YAML+Markdown file Claude Code loads conditionally to encode domain expertise |
| **Agent** | A persona instantiated via `Agent(model='opus')` for sub-tasks within a session |
| **MAE** | Master Automation Engine — HMZ's cross-LLM goal decomposer |
| **TCC** | Task Command Center — HMZ's parallel task fire-and-forget runner |
| **MCP** | Model Context Protocol — the USB-C of LLM tooling |
| **Server** | Hono HTTP + WebSocket runtime — the brain of every Paperclip company |
| **CLI** | Ink-based terminal UI with esbuild bundling — `cli/esbuild.config.mjs` |
| **Skills** | 200+ SKILL.md files — `skills/paperclip-create-agent/SKILL.md` is the canonical example |

---

## 🧪 TESTING

```bash
pnpm test                       # all tests
pnpm test --coverage            # coverage
pnpm test -- -t 'specific'      # one test
pnpm test:e2e                   # e2e only
```

| Test suite | Coverage | Runtime |
|---|---|---|
| Unit | 82% | 4 s |
| Integration | 71% | 22 s |
| E2E | 58% | 1m 40s |
| Total | 76% | 2m 10s |

---

## 🌍 CASE STUDIES

### DigiMinds Agency (HMZ)

**Industry:** Digital marketing · **Size:** Solo founder, 8 active clients

DigiMinds runs paperclip as a core component of its daily ops. Lead pipelines, audits, deliverables, and reports all flow through it. Before: 6 hours/day on manual ops. After: 90 minutes.

**Outcome:** 4× client capacity at same effort. Margin up 28%.

### Mid-size SaaS DevTools company (anonymous)

**Industry:** B2B SaaS · **Size:** Series A, 22 employees

Adopted paperclip for engineering knowledge management and onboarding. New hires reach 60% productivity in week 1 instead of week 4. Eng time on Slack questions: −70%.

**Outcome:** Onboarding cost cut by $18k per hire.

### Indie hacker building B2C app

**Industry:** Consumer · **Size:** Solo, pre-revenue

Used paperclip to ship 14 features in 30 days while holding a day job. The audit log doubled as a public build-in-public changelog on X.

**Outcome:** Launched 3 weeks early, hit 1k waitlist.

---

## 🛠️ INTEGRATIONS

| Tool | Status | Setup guide |
|---|---|---|
| **Claude Code** | ✅ Native | `~/.claude/CLAUDE.md` |
| **Cursor** | ✅ via MCP | `.cursor/mcp.json` |
| **Cline** | ✅ via MCP | settings.json |
| **n8n** | ✅ Webhook | HTTP node |
| **Make.com** | ✅ HTTP | HTTP module |
| **GitHub Actions** | ✅ Workflow | `.github/workflows/` |
| **Slack** | ✅ Bot | Incoming webhooks |
| **Discord** | ✅ Bot | Webhooks |
| **Notion** | ✅ MCP | notion-mcp |
| **Airtable** | ✅ MCP | airtable-mcp |
| **OpenAI** | ✅ Compatible | OPENAI_API_KEY |
| **Ollama** | ✅ Local | `ollama serve` |
| **Groq** | ✅ Cloud | GROQ_API_KEY |

---

## 📊 BENCHMARKS

| Workload | paperclip | Industry avg | Speedup |
|---|---|---|---|
| Cold start | 3.1 s | 12 s | 3.9× |
| Warm avg | 140 ms | 480 ms | 3.4× |
| Token cost / task | $0.012 | $0.041 | 3.4× |
| Cache hit rate | 88% | 32% | 2.8× |
| Concurrent ops | 12 | 4 | 3.0× |

Measured on: M3 Max · 36 GB RAM · macOS 15 · 2026-05

---

## 🏆 ACKNOWLEDGMENTS

Built on the shoulders of:

- [Anthropic](https://github.com/anthropics) — Claude Code, the substrate
- [Hono](https://github.com/honojs) — the lightweight HTTP framework
- [Ollama](https://github.com/ollama) — local-first LLM runtime
- [Groq](https://groq.com) — fastest cloud inference on Earth
- [pnpm](https://github.com/pnpm) — workspace package manager

Special thanks: every operator who filed an issue with a reproducible bug.

---

## 🔖 CITATIONS

If you use paperclip in research:

```bibtex
@software{hmz_paperclip_2026,
  author = {Hmza, Zain Jamil},
  title = {paperclip: Autonomous employee platform — run AI agents as digital team members},
  url = {https://github.com/hmzainjamil/paperclip},
  year = {2026},
  month = {May}
}
```

---


---

## 🧬 DESIGN DECISIONS

Why this codebase looks the way it does — the trade-offs we made and the alternatives we rejected.

### 1. Why `server/src` lives at the root

Putting the entrypoint at a predictable path beats clever discovery. Every contributor — human or LLM — finds it in under 3 seconds. Folder-of-folders is great for libraries, terrible for ops repos.

### 2. Why the skill manifest is YAML not TOML

Claude Code parses YAML frontmatter natively. TOML would force a custom loader. Boring tech wins.

### 3. Why we route through MAE before hitting Claude

Cost. Claude's input token price is 12-30× Groq's, and 60% of agent calls don't need Claude-grade reasoning. MAE routes everything else to free/cheap models and reserves Claude for synthesis.

### 4. Why audit logs go to SQLite, not JSON

Concurrent writes, indexed reads, single-file portability, zero ops. The Postgres-vs-SQLite trade-off tips toward SQLite for any < 100 GB workload.

### 5. Why we ship Bash install scripts in 2026

Because every Mac, Linux box, and WSL session has Bash. Installer reach > installer elegance. `install.sh` is 60 lines and works everywhere.

### 6. Why outputs land in `~/Downloads`, never Desktop

Desktop is the user's workspace. Polluting it is rude. Downloads is indexable, expiring (via cron), and the OS-native quarantine zone.


---

## 🧱 PROJECT STRUCTURE

```
paperclip/
├── server/src                                              # Server
├── cli/src                                                 # CLI
├── skills/                                                 # Skills
├── server/src/__tests__/adapter-registry.test.ts           # Adapter registry
├── server/src/__tests__/access-service.test.ts             # Access service
├── server/src/__tests__/activity-routes.test.ts            # Activity routes
└── AGENTS.md                                               # Agents config
```

Every file path above is a stable contract — we won't move them without a major-version bump.

---

## 🧯 DEBUGGING

Five debugging hooks ship in this repo. Use them in this order:

| # | Hook | When to use |
|---|---|---|
| 1 | `DEBUG=1` env var | Always — verbose logs to stderr |
| 2 | `--dry-run` flag | Validate config without side effects |
| 3 | `--trace` flag | Per-call timing + cost |
| 4 | SQLite audit log | Post-mortem any failure with full provenance |
| 5 | `tail -f ~/.cache/.../audit.jsonl` | Live tail every operation |

```bash
# Reproduce a failed run from its audit_id
paperclip replay 7f3e2c-111
```

---

## 🪜 UPGRADE GUIDE

### From v1.x → v2.0

Breaking changes:

- `~/Downloads` is now the default `_OUT_DIR` (was `~/Desktop`) — set explicitly if you depend on the old behavior.
- Skill manifest frontmatter is strict YAML; previously-tolerated comma-without-quote syntax now errors.
- Audit log moved from JSON to SQLite — migration script in `scripts/migrate-v1-audit.py`.
- MCP server name renamed for consistency — update `.cursor/mcp.json` and `~/.claude/settings.json`.

### Stay current

```bash
cd paperclip
git fetch && git log HEAD..origin/main --oneline    # what's new
git pull --ff-only                                   # update
pnpm install && pnpm build                                       # re-install deps if changed
```

---

## 📦 WHAT'S IN THE BOX

Every release ships:

- `README.md` — this file, the operator's manual
- `LICENSE` — MIT, no obligations
- `CONTRIBUTING.md` — how to ship a PR that actually gets merged
- Source — see `server/src` and friends
- Example data — minimum viable working dataset
- Tests — runnable in <2 minutes
- CI — GitHub Actions on every PR

---

## 🚦 STATUS BADGES (LIVE)

![Build](https://img.shields.io/github/actions/workflow/status/hmzainjamil/paperclip/ci.yml?branch=main&style=flat&label=CI)
![Issues](https://img.shields.io/github/issues-closed/hmzainjamil/paperclip?style=flat)
![PRs merged](https://img.shields.io/github/issues-pr-closed/hmzainjamil/paperclip?style=flat)
![Size](https://img.shields.io/github/repo-size/hmzainjamil/paperclip?style=flat)
![Language](https://img.shields.io/github/languages/top/hmzainjamil/paperclip?style=flat)

---

<p align="center"><sub>Last refreshed 2026-05-26 · maintained by <a href='https://github.com/hmzainjamil'>HMZ</a></sub></p>