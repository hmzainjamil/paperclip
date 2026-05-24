# paperclip

> **Open-source orchestration for zero-human companies** — run AI agents as digital employees with task assignment, progress tracking, and budget controls

<p align="center">
  <a href="https://github.com/hmzainjamil/paperclip/stargazers"><img src="https://img.shields.io/github/stars/hmzainjamil/paperclip?style=for-the-badge&labelColor=555&color=yellow" alt="Stars"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/network/members"><img src="https://img.shields.io/github/forks/hmzainjamil/paperclip?style=for-the-badge&labelColor=555&color=blue" alt="Forks"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/issues"><img src="https://img.shields.io/github/issues/hmzainjamil/paperclip?style=for-the-badge&labelColor=555&color=red" alt="Issues"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/pulls"><img src="https://img.shields.io/github/issues-pr/hmzainjamil/paperclip?style=for-the-badge&labelColor=555&color=purple" alt="PRs"/></a>
  <a href="https://github.com/hmzainjamil/paperclip/commits/main"><img src="https://img.shields.io/github/last-commit/hmzainjamil/paperclip?style=for-the-badge&labelColor=555&color=green" alt="Last Commit"/></a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/TypeScript-full_stack-blue?style=flat&labelColor=555&logo=typescript"/>
  <img src="https://img.shields.io/badge/Self--hosted-local_first-green?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/Agents-Claude|Hermes|Codex-orange?style=flat&labelColor=555"/>
  <img src="https://img.shields.io/badge/License-MIT-lightgrey?style=flat&labelColor=555"/>
</p>

---

## Why This Exists

Managing AI agents is like managing a team — you need task assignment, progress visibility, budget controls, and audit trails. Paperclip provides the operating system: create a company, hire AI employees, assign tasks via issues, track progress in real time, and review outputs before delivery.

This is the infrastructure layer for zero-human companies — where AI handles all execution and humans only make strategic decisions.

---

## At a Glance

| Feature | Detail |
|---|---|
| Companies | Multi-company — each with own employees, projects, budget |
| AI employees | Hire Claude Code, Hermes Agent, or Codex as team members |
| Issue tracker | GitHub-style issues — task assignment, comments, status |
| Budget controls | Per-employee token budget with overage alerts |
| Audit trail | Full transcript of every agent action |
| Local server | Runs on `http://127.0.0.1:3100` — no cloud required |
| API | REST API for all operations — automate from scripts |
| Adapters | hermes-paperclip-adapter, claude-paperclip, codex-paperclip |
| Wake mechanisms | Comment-driven + assignment-driven agent wakes |
| Skill registry | Company-managed skill library for all employees |

---

## 🧠 CONCEPTS

| Concept | Description |
|---|---|
| **Company** | Organizational unit — has employees, projects, issues, budget |
| **Employee** | AI agent hired into the company — assigned tasks via issues |
| **Issue** | Task unit — title, description, assignee, status, comments |
| **Project** | Collection of issues — represents a product/client/workstream |
| **Wake** | Event that causes an employee to start working — assignment or comment |
| **Transcript** | Full record of everything an employee did on a task |
| **Skill** | Expertise module available to employees via skill registry |
| **Budget** | Token budget per employee per task — enforced at runtime |
| **Adapter** | Bridge between Paperclip and a specific agent runtime |
| **Heartbeat** | Periodic session state save — enables resume after interruption |

### 🔥 Hot

- **Comment-driven wakes** — mention `@employee-name` in any issue comment → agent wakes, reads full thread, continues work
- **Multi-agent projects** — assign different issues to different employees — parallel execution across one project
- **Budget enforcement** — no surprise API bills — every employee has a hard token ceiling per task
- Source → [HMZ](https://github.com/hmzainjamil)

---

## ⚙️ HOW IT WORKS

```
Create company → Hire AI employees → Create project → Create issues
    ↓
Issues assigned to employees
    ↓
Employee adapter polls for assigned issues
    ↓
Agent executes task (Claude Code / Hermes / Codex)
    ↓
Structured transcript → Paperclip issue comments
    ↓
Status: DONE / BLOCKED / IN_PROGRESS
    ↓
Human reviews → approves → invoices client
```

---

## 🚀 INSTALL

```bash
# Clone
git clone https://github.com/hmzainjamil/paperclip
cd paperclip

# Install dependencies
npm install

# Start server
npm start
# Server running at http://127.0.0.1:3100

# Create first company
curl -X POST http://127.0.0.1:3100/api/companies \
  -H "Content-Type: application/json" \
  -d '{"name": "My Agency"}'

# Install employee adapter (Claude)
git clone https://github.com/hmzainjamil/hermes-paperclip-adapter
cd hermes-paperclip-adapter
PAPERCLIP_COMPANY_ID=your-cid python adapter/main.py
```

---

## 📟 USAGE

```bash
# API examples
CID=your-company-id

# Create project
curl -X POST http://127.0.0.1:3100/api/companies/$CID/projects \
  -d '{"name": "Client Website Redesign"}'

# Create issue (task)
curl -X POST http://127.0.0.1:3100/api/companies/$CID/issues \
  -d '{"title": "Build contact form", "projectId": "proj-id", "assignee": "claude"}'

# List issues
curl http://127.0.0.1:3100/api/companies/$CID/issues

# Add comment (wakes agent)
curl -X POST http://127.0.0.1:3100/api/companies/$CID/issues/$ISSUE_ID/comments \
  -d '{"body": "@claude please also add email validation"}'

# Get transcript
curl http://127.0.0.1:3100/api/companies/$CID/issues/$ISSUE_ID/transcript
```

---

## ⚙️ CONFIGURATION

| Variable | Default | Description |
|---|---|---|
| `PORT` | `3100` | Server port |
| `DB_PATH` | `~/.paperclip/db.sqlite` | SQLite database path |
| `AUTH_TOKEN` | none | Optional API authentication token |
| `MAX_COMPANIES` | unlimited | Cap on company count |
| `ISSUE_RETENTION_DAYS` | 90 | Days before old issues archived |
| `TRANSCRIPT_MAX_SIZE` | `10MB` | Max transcript size per issue |
| `BUDGET_DEFAULT_TOKENS` | `100000` | Default token budget per task |
| `WAKE_POLL_INTERVAL` | `10` | Seconds between issue polls for adapters |
| `WEBHOOK_SECRET` | none | Outbound webhook authentication |
| `SKILL_DIR` | `~/.paperclip/skills/` | Company skill library path |

---

## 💡 TIPS AND TRICKS

### Operations
1. **Daily standup automation** — create a daily standup issue assigned to a `reporting` employee — gets status on all in-progress issues. Source → [HMZ](https://github.com/hmzainjamil)
2. **Budget alerts** — set `BUDGET_WARNING_PCT=0.7` in adapters — get Slack alerts when employees hit 70% budget. Source → [HMZ](https://github.com/hmzainjamil)
3. **Issue templates** — create issue templates per project type — employees get consistent task context. Source → [HMZ](https://github.com/hmzainjamil)

### Multi-Employee
4. **Parallel assignment** — assign independent issues to different employees simultaneously — parallel execution. Source → [HMZ](https://github.com/hmzainjamil)
5. **Handoff issues** — employee A creates issue for employee B when it depends on their output. Source → [HMZ](https://github.com/hmzainjamil)
6. **Specialist employees** — hire different agents for different domains: Hermes for code, Claude for writing, Codex for large codebases. Source → [HMZ](https://github.com/hmzainjamil)

### Quality Control
7. **Transcript review** — review agent transcripts after first few tasks per employee type to calibrate prompts. Source → [HMZ](https://github.com/hmzainjamil)
8. **Blocked issues** — agents mark issues BLOCKED when they need human input. Check daily. Source → [HMZ](https://github.com/hmzainjamil)
9. **Comment-driven refinement** — don't reopen issues. Add refinement comments → agent wakes and continues. Source → [HMZ](https://github.com/hmzainjamil)

### Automation
10. **Webhook integration** — `POST /webhooks` → trigger Paperclip issue creation from Slack, email, or any tool. Source → [HMZ](https://github.com/hmzainjamil)
11. **LaunchAgent** — wrap Paperclip server in macOS LaunchAgent for always-on operation. Source → [HMZ](https://github.com/hmzainjamil)
12. **Backup** — `~/.paperclip/db.sqlite` is the full database. Back it up daily. Source → [HMZ](https://github.com/hmzainjamil)

---

## 🔧 TROUBLESHOOTING

| Issue | Cause | Fix |
|---|---|---|
| Server not starting | Port 3100 in use | `lsof -i :3100` → kill process |
| Agents not waking | Adapter not polling | Check adapter process is running |
| Issues stuck in-progress | Agent crashed | Check adapter logs, restart |
| Transcripts empty | Adapter version mismatch | Update adapter to latest |
| Budget overage | Wrong default set | Set `BUDGET_DEFAULT_TOKENS` in adapter |
| DB corruption | Unclean shutdown | `sqlite3 db.sqlite ".recover"` |
| Webhooks not firing | Wrong URL | Test with `curl` before wiring |

---

## 📊 ARCHITECTURE

```
paperclip/
├── src/
│   ├── server.ts          # Express API server
│   ├── db/                # SQLite schema + migrations
│   ├── routes/
│   │   ├── companies.ts
│   │   ├── issues.ts
│   │   ├── projects.ts
│   │   └── webhooks.ts
│   └── types/             # Shared TypeScript types
├── adapters/
│   └── (see separate adapter repos)
└── client/                # Optional web UI
```

---

## 🗺️ ROADMAP

- [ ] Web UI — visual dashboard for companies, employees, issues
- [ ] Slack integration — create/update issues from Slack
- [ ] GitHub sync — bidirectional sync with GitHub Issues
- [ ] Time tracking — log hours per issue for client billing
- [ ] Invoice generation — auto-generate invoices from completed issues
- [ ] Multi-tenant cloud — hosted Paperclip for teams

---

## ☠️ STARTUPS / BUSINESSES

Paperclip is the operating system for running a digital business with AI employees. Every client deliverable becomes an issue. Every AI action is tracked and auditable. Every employee has a budget ceiling. You get the output of a 10-person team at the cost of API tokens.

**Agency math:** 50 client issues/month × 30min human time without Paperclip = 25hrs. With Paperclip: 50 issues × 2min review = 1.7hrs. Same output, 93% time reduction.

---

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=hmzainjamil/paperclip&type=Date)](https://star-history.com/#hmzainjamil/paperclip&Date)

---

<p align="center">
  Built by <a href="https://github.com/hmzainjamil">HMZ</a> · <a href="https://paperclip.ing/docs">Docs</a> · <a href="https://discord.gg/m4HZY7xNG3">Discord</a> · <a href="https://x.com/papercliping">Twitter</a>
</p>
