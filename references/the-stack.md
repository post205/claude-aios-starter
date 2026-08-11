# The Stack — Context · Connections · Capabilities · Cadence

> *"An assistant that knows nothing about you is a stranger with API access. Load the context first. Everything else is plumbing."*

The Shift is how you think. The Stack is what you build. Four layers, in order. Each one is a plain word that says exactly what it is.

Most people build these in the wrong order — they wire a tool first, get a clever demo, and wonder why it never becomes part of their week. The order below is the whole trick.

---

## Layer 1 — CONTEXT (it knows your business)

Everything stands on this. An AI with perfect tool access and no context produces confident, generic, useless output.

**What lives here:** who you are, what you sell, who you sell it to, who's on the team, what you decided last quarter and why, how you sound when you write.

**In this kit:** `context/`, `references/voice.md`, `decisions/log.md`, and the root `CLAUDE.md`.

**The test:** open a brand-new session. Ask *"what does this business do, and who works here?"* If it answers correctly without browsing or guessing, Context is in place.

**Most common failure:** context that exists in your head but was never written down. If you've explained the same thing to Claude three times, that's a missing file, not a bad memory.

---

## Layer 2 — CONNECTIONS (it reaches your tools and data)

Context makes it smart about your business. Connections make it current.

**What lives here:** the paths to live data — calendar, email, revenue, tasks, files, meeting notes. Plus a written guide for each one so no future skill has to re-research the same API.

**In this kit:** `connections.md` (the registry) and `references/{tool}-api.md` (the researched-once guides).

**The test:** ask *"what's on my calendar tomorrow, and what's due this week?"* If you get live data with nothing pasted in, Connections is in place.

**Build rule:** climb the reliability ladder only as high as you need — direct API, then a thin CLI, then browser automation, then scraping. And prefer a command you call on demand over a heavy integration that loads its whole toolset into every session. One pays per use. The other pays rent forever. (The Shift, Move 3.)

**Most common failure:** all reads, no writes. If nothing can send, post, or update, you built a viewer, not an operating system.

---

## Layer 3 — CAPABILITIES (it knows how to do the work)

Context and Connections are nouns. Capabilities are verbs — the repeatable work, written down once so it runs the same way every time.

**What lives here:** skills and sub-agents. A skill is a process you'd otherwise re-explain: how you write a proposal, how you prep for a client call, how you turn a transcript into a follow-up.

**In this kit:** `.claude/skills/` — and `/level-up` exists to add one more, every week.

**The test:** a short phrase triggers a multi-step workflow that ends in a real artifact — a file, a draft, a report. Not advice about the artifact. The artifact.

**Build rule:** one skill, one job. Separate steps are easier to debug, swap, and tune than one clever generalist.

**Most common failure:** three shipped skills, zero of them yours. The kit's own skills don't count — the layer only turns on when you've written one from your actual work.

---

## Layer 4 — CADENCE (it runs without being asked)

The first three layers make a very good assistant. This one makes it an operating system.

**What lives here:** anything that fires on a schedule or a trigger instead of on your prompt — a morning brief, a weekly review, a hook that runs when a file changes.

**In this kit:** hooks in `.claude/settings.json`, scheduled runs, and the weekly `/level-up` ritual.

**The test:** laptop closed. A brief lands in your inbox. Something got handled while you weren't watching.

**Build rule:** last, always. Don't put a schedule on something that doesn't work reliably by hand yet. You'll just automate a mistake and go to sleep.

---

## Build order

```
Context  ──▶  Connections  ┐
                           ├──▶  Cadence
             Capabilities  ┘
```

**Context first.** Non-negotiable. Everything above it inherits its quality.

**Connections and Capabilities in parallel.** They feed each other — a new connection suggests a new skill, and a half-built skill tells you which connection you actually need.

**Cadence last.** Automating something unproven is how you get a system you have to babysit.

---

## Scoring yourself

`/audit` scores each layer out of 25 and ranks your gaps by leverage. Run it on Day 7 for a baseline, then weekly.

Expect a low first number. Most honest setups start between 20 and 40. The score is a direction, not a grade — the point is watching it move.

| Total | Stage | What it means |
|---|---|---|
| 0-39 | **Foundation** | It knows some things. It can't do much yet. |
| 40-69 | **Built** | Real context, live data, a couple of working skills. |
| 70-89 | **Compounding** | You reach for it first. Skills are stacking on each other. |
| 90-100 | **Autonomous** | Work gets done while you're not at the desk. |

---

## The one test that matters

> **While you're away from your desk, your AIOS notices one real event and produces an output faster and more accurate than what you'd have produced yourself.**

Every layer here exists to serve that sentence. If something you're about to build doesn't move you toward it, don't build it.
