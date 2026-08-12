---
name: audit
description: Use when someone asks for an AIOS audit, asks to score their setup against The Stack, or says "is my AIOS working" / "audit my setup" / "find gaps in my AIOS" / "what's my score". Produces a Stack scoreboard (Memory, Reach, Skill, Judgment, Initiative) with the top 3 fixes ranked by leverage.
---

## What this skill does

Scores the current Claude Code project against **The Stack** — the five-layer model in `references/the-stack.md`. Reads widely, writes almost nothing. Each layer is worth 20 points. Reports a total out of 100, names what's strong, and ranks the gaps by how much they're costing.

**This is a structural audit.** It answers *"is this thing built right?"* — are the files, registries, guardrails, and triggers in decent shape. It does not answer *"what should I build next?"* That's `/level-up`. Keep the two separate; a structural fix list and a capability wishlist are different conversations and mixing them produces neither.

The first run is a baseline, and it will be low. That's fine and expected. The value is in the second run, and the eighth.

## Today's context

- **Date:** !`date +%Y-%m-%d`
- **Project root:** the current working directory

## The Stack (20 points each, 100 total)

| Layer | What it asks |
|---|---|
| **Memory** | Does it know the business? |
| **Reach** | Can it touch live tools and data? |
| **Skill** | Does it know how to do the work? |
| **Judgment** | Does it know what it may decide alone? |
| **Initiative** | Does it move before being asked? |

Full definitions, build order, and per-layer failure modes live in `references/the-stack.md`. Read it if a scoring call is ambiguous.

## Execution

### Step 1 — Find the shape of the project

Look for **intent, not exact filenames.** People name things differently and shouldn't lose points for it. If the equivalent information is captured somewhere sensible, credit it.

Use Glob and Read to check for:

**Operating manual** — `CLAUDE.md` at root, plus `CLAUDE.local.md` if present.
**Persistent memory** — `MEMORY.md`, a `memory/` folder, or `~/.claude/projects/<id>/memory/`.
**Skills** — `.claude/skills/*/SKILL.md`. Count them and read the frontmatter only.
**Agents** — `.claude/agents/*.md`. Count them.
**Live connections** — any of these counts as reachable:
- a thin CLI or `curl` wrapper the user calls on demand
- a script in `scripts/` that hits an API, documented in `CLAUDE.md`
- an MCP server in `.mcp.json` or the `mcpServers` key of `.claude/settings.json`
- an export pipeline (`data/`, `imports/`, `exports/`) with a refresh script and a recent run
- a `.env` key paired with a `references/{tool}-api.md` guide

**Connections registry** — `connections.md`, wherever it lives.
**Reference guides** — `references/{tool}-api.md`, `references/{tool}-cli.md`, or equivalent.
**Decisions** — `decisions/log.md`, `decisions.md`, or any append-only decision record.
**Guardrails** — a permissions/authority section in `CLAUDE.md`, a `references/guardrails.md`, `.claude/rules/*.md`, or `rollout-phase` / autonomy-level frontmatter inside skills.
**Templates** — `templates/` or `.claude/templates/`.
**Triggers** — the `hooks` key in `.claude/settings.json`, scheduled jobs, or skills named `morning-*`, `daily-*`, `weekly-*`, `monthly-*`, `standup`.
**Unprompted output** — a folder like `briefs/`, `reports/`, `digests/`, or `audits/` holding files nobody asked for by hand.

### Step 2 — Score the five layers

#### Memory — 20 pts

| Criterion | Pts | How to detect |
|---|---|---|
| Operating manual exists and says something (>200 words) | 4 | Read `CLAUDE.md`, count words |
| Identity, role, and voice captured | 4 | Manual names who the user is and what they do, or `references/voice.md` exists |
| Persistent memory with real entries | 4 | `MEMORY.md` or `memory/` with more than 3 entries |
| Reference material exists | 4 | `references/`, `docs/`, or `sops/` holds at least one substantive file |
| Decisions are being recorded | 4 | Decision log has at least one real entry |

#### Reach — 20 pts

A connection counts through **any** mechanism. This kit is API-first and does not prefer MCPs — a `curl` wrapper the user understands scores the same as a server.

**The seven Tier-1 domains:**

| # | Domain | Examples |
|---|---|---|
| 1 | Revenue / financials | Stripe, Xendit, QuickBooks, a billing sheet |
| 2 | Customer interactions | HubSpot, Salesforce, Gmail-as-CRM, DMs |
| 3 | Calendar | Google Calendar, Outlook, Calendly |
| 4 | Communication | Gmail, Outlook, Slack, Teams, Viber |
| 5 | Project / task tracking | ClickUp, Asana, Linear, Notion, Jira |
| 6 | Meeting intelligence | Granola, Otter, Fireflies, Fathom |
| 7 | Knowledge / files | Drive, Dropbox, Notion, SharePoint |

| Criterion | Pts | How to detect |
|---|---|---|
| Tier-1 domain coverage | 8 | ~1.15 pts per domain reachable, rounded to the nearest 0.5, capped at 8 |
| Every connected tool has a written guide | 4 | Subtract 1 per connected tool with no `references/{tool}-*.md`. Floor 0. |
| Connections are actually alive | 3 | Subtract 1 per connection marked expired or needing auth, or any script with no run in 30 days. Floor 0. |
| The registry is filled in | 3 | 0 missing, 1 sparse, 2 mostly current, 3 covers everything reachable |
| It can write, not only read | 2 | At least one connection can send, post, or update. 0 if everything is read-only. |

#### Skill — 20 pts

| Criterion | Pts | How to detect |
|---|---|---|
| 3 or more skills installed | 7 | Count `.claude/skills/*/SKILL.md` |
| At least one skill the user wrote | 7 | Any skill outside the shipped set — `onboard`, `audit`, `level-up` — and outside common third-party skills |
| At least one agent defined | 3 | `.claude/agents/*.md` count ≥ 1 |
| Templates in use | 3 | `templates/` or `.claude/templates/` holds at least one file |

The second row is the one that matters. A kit running only its own three skills has not turned this layer on.

#### Judgment — 20 pts

The layer nobody builds until something goes wrong. Score it honestly — an ungoverned setup that scores well everywhere else is not a good setup, it's a fast one.

| Criterion | Pts | How to detect |
|---|---|---|
| Workflows declare an autonomy level | 6 | `rollout-phase` or an L0-L4 level in skill frontmatter. Full marks if most skills carry one, partial if some do. |
| Guardrails are written down | 5 | A section in `CLAUDE.md` (or `references/guardrails.md`, `.claude/rules/`) stating what the AIOS may never do unreviewed |
| Credentials are scoped and separate | 4 | `.env` uses service-specific keys, `.gitignore` covers them, and nothing suggests the user's personal passwords are in play |
| At least one human-review step exists | 3 | Any skill that explicitly drafts for approval instead of sending, or a stated "show me first" rule |
| There's a trail | 2 | Decision log, audit reports, or run logs showing what the system actually did |

If nothing at all is found here, score 0 and say so plainly. This is the highest-leverage zero in the whole audit.

#### Initiative — 20 pts

| Criterion | Pts | How to detect |
|---|---|---|
| At least one thing fires without a prompt | 8 | A hook in `.claude/settings.json`, a scheduled job, or a skill named `daily-*` / `weekly-*` / `morning-*` / `standup` |
| The system is in active use | 6 | Skills or context files modified in the last 30 days, or a decision logged in the last 30 days |
| Unprompted work has actually landed | 6 | A `briefs/`, `reports/`, `digests/`, or `audits/` folder holding recent generated output |

A schedule that exists but has never produced anything scores the first row and not the third. Say that in the report — it's the most common form of fake autonomy.

### Step 3 — Rank the gaps by leverage

For every criterion that lost points: **leverage = points lost × multiplier.**

| Situation | Multiplier | Why |
|---|---|---|
| Judgment scored 0 | **4x** | Something is running with nobody accountable for it |
| No Tier-1 domain reachable | **4x** | The system is blind to the business |
| Operating manual missing or thin | **3x** | Every layer above it inherits the gap |
| 2 or fewer Tier-1 domains reachable | **3x** | Reach is the gateway to everything live |
| Zero skills | **2x** | Nothing to run |
| Initiative running above proven Judgment | **2x** | Unattended work with no review path |
| Nothing fires unprompted | **2x** | Still an assistant, not an OS |
| Everything is read-only | **2x** | A viewer, not an operating system |
| Connected tools with no written guide | **1.5x** | Every future skill re-researches the same API |
| No decision record | **1.5x** | The reasoning evaporates |
| Everything else | 1x | |

Sort descending, take the top three, and write one concrete next step for each. Point at real actions:

- **Missing guardrails?** *"Add an 'Authority' section to `CLAUDE.md`: what it may send unreviewed, what it must draft, what it may never touch."*
- **Skills with no autonomy level?** *"Add `rollout-phase: 1` to each skill's frontmatter and move it up only after it's proven."*
- **Can't reach a Tier-1 domain?** *"Write `scripts/{tool}_api.py`, then save what you learned to `references/{tool}-api.md`."*
- **Connected tool with no guide?** *"Research the API once. Save the endpoints, auth flow, and the two queries you actually use."*
- **Nothing unprompted?** *"Add a hook to `.claude/settings.json`, or write a `daily-brief` skill and run it every morning until it earns a schedule."*
- **No decisions?** *"Append today's call to `decisions/log.md` — decision, why, alternatives, owner."*

### Step 4 — Print the report

Output in chat, as Markdown:

```
# AIOS Audit — {date}
**Score: {total}/100** — {stage}

## Scoreboard

Memory      {bar}  {n}/20  {label}
Reach       {bar}  {n}/20  {label}
Skill       {bar}  {n}/20  {label}
Judgment    {bar}  {n}/20  {label}
Initiative  {bar}  {n}/20  {label}

## What's working
- {1-3 bullets, drawn from the highest-scoring criteria}

## Top 3 gaps, by leverage
1. **{gap}** (-{pts} × {multiplier})
   → {concrete next step}
2. **{gap}** (-{pts} × {multiplier})
   → {concrete next step}
3. **{gap}** (-{pts} × {multiplier})
   → {concrete next step}

## Do this first
{the single highest-leverage action}

---
Structure only. For what your AIOS could DO but can't yet, run /level-up.
```

**Bar:** two hash marks per 4 points. **Label:** "Strong" at 16+, "Solid" 12-15, "Thin" 6-11, "Missing" below 6.

**Stages:** 0-39 Foundation · 40-69 Trained · 70-89 Trusted · 90-100 Autonomous.

### Step 5 — Offer to save it

Ask once: *"Save this to `audits/audit-{date}.md` so you can watch the score move?"* If yes, write it and create `audits/` if needed. This is the only file this skill is allowed to create.

## Rules

1. **Read-only, with one exception.** Never touch `CLAUDE.md`, memory, skills, or context. The saved audit report is the sole write.
2. **Be honest, not kind.** Most real setups land between 30 and 65. A 95 should be rare enough to be a story. Inflated scores make the second run meaningless.
3. **Judgment gets scored even when it's uncomfortable.** Do not soften a zero here. Name it and put it at the top of the gap list.
4. **Credit intent over filenames.** Different names, same substance, full points.
5. **Don't recommend skills that don't exist.** Point at what's actually installed or what the user can write.
6. **Finish in under a minute.** Read targeted files. Count skill folders without reading each one in full.
7. **Fuzzy detection is fine.** Where hooks or schedules aren't cleanly visible, infer from naming and say you inferred it.

## Verification (for the implementer)

- **Fresh clone.** Expected: roughly 15-30/100, Judgment and Initiative near zero, top gap is Memory or Reach. A fresh clone scoring 60 means the rubric is too generous.
- **Guardrails test.** Take a mature setup and delete every autonomy declaration. Expected: Judgment collapses and moves to the top of the gap list at 4x.
- **Fake autonomy test.** A project with a scheduled hook that has produced nothing. Expected: 8 points in Initiative, not 20, and the report says so.
- **Renamed-files test.** A project using `docs/` instead of `references/` and `decisions.md` instead of `decisions/log.md`. Expected: no points lost.
