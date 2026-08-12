# The Stack — Memory · Reach · Skill · Judgment · Initiative

> *"You are not installing software. You are onboarding a hire who will never forget anything and never ask for a raise. Train it in that order."*

The Shift is how you think. The Stack is what you build.

Five layers. Read them as the five things you'd assess in a person you just hired — because that's exactly what they are. A new staff member has to learn the business before they can be useful, has to be given access before they can act, has to be taught the work before they can do it alone, has to know where their authority ends, and only then, eventually, starts moving without being told.

Skip a layer with a person and you get a confident employee doing damage. Same here.

---

## Layer 1 — MEMORY (it knows your business)

Everything stands on this. A model with perfect tool access and no memory of your business produces output that is fast, fluent, and generic. That's the worst combination there is, because it's wrong in a way that reads as right.

**What lives here:** who you are, what you sell, who you sell it to, who's on the team, what you decided last quarter and why, and how you sound when you write.

**In this kit:** `context/`, `references/voice.md`, `decisions/log.md`, and the root `CLAUDE.md`.

**The test:** open a cold session. Ask *"what does this business do, who works here, and what did we decide in June?"* If it answers correctly without browsing or guessing, Memory is in place.

**How it fails:** context that lives in your head and was never written down. If you've explained the same thing three times, that isn't a bad memory — that's a missing file. Write it once.

---

## Layer 2 — REACH (it touches your tools and data)

Memory makes it smart about your business. Reach makes it current.

**What lives here:** the paths to live data — calendar, email, revenue, tasks, files, meeting notes — plus a written guide for each one so no future skill has to rediscover the same API.

**In this kit:** `connections.md` as the registry, and `references/{tool}-api.md` as the researched-once guides.

**The test:** ask *"what's due this week?"* If you get live data with nothing pasted in, and it can also send, post, or update something — Reach is in place.

**Build rule:** climb the reliability ladder only as high as you need. Direct API, then a thin CLI, then browser automation, then scraping. And prefer a command you call on demand over a heavy integration that loads its entire toolset into every session. One charges you per use. The other charges rent on every conversation you ever have.

**How it fails:** all reads, no writes. If nothing can leave the building, you built a very well-informed viewer.

---

## Layer 3 — SKILL (it knows how to do the work)

Memory and Reach are nouns. Skill is the verb — your repeatable work, written down once so it runs the same way every time instead of depending on how well you phrased the prompt that morning.

**What lives here:** skills and sub-agents. A skill is any process you'd otherwise have to re-explain — how you write a proposal, how you prep a client call, how you turn a transcript into a follow-up.

**In this kit:** `.claude/skills/`. And `/level-up` exists for one reason: to add one more, every week.

**The test:** a short phrase produces a finished artifact — a file, a draft, a report. Not advice about the artifact. The artifact. And it comes out the same shape on Tuesday as it did on Friday.

**Build rule:** one skill, one job. A narrow skill you can debug beats a clever one you can't.

**How it fails:** three skills installed, none of them yours. The kit's own skills don't count. This layer switches on the day you write one from your actual week.

---

## Layer 4 — JUDGMENT (it knows what it may decide alone)

This is the layer most people skip, and it's the one that decides whether any of this survives contact with a real client.

You would never give a new hire your bank login on day one. You'd give them a scoped account, have them draft things for review, and widen their authority as they earned it. Nothing about that changes because the hire is a model.

**What lives here:** the autonomy level attached to each workflow, the written rules about what it may never touch, its own scoped credentials, and a trail of what it actually did.

**In this kit:** the `rollout-phase` frontmatter `/level-up` stamps on every artifact it scaffolds, the guardrails section of your `CLAUDE.md`, and `decisions/log.md` as the record.

**The test:** point at any running workflow and say what happens if it's wrong. If you can name the autonomy level, the review step, and who finds out — Judgment is in place. If the honest answer is *"I'd probably notice eventually"* — it isn't.

**The autonomy ladder:**

| Level | What happens |
|---|---|
| L0 — Manual | No AI. A person does it. |
| L1 — Suggested | AI suggests, a human decides every step. |
| L2 — Drafted | AI drafts, a human reviews and edits before it goes out. |
| L3 — Supervised | Rules set, AI runs, a human spot-checks. |
| L4 — Autonomous | AI runs end to end. |

**Build rule:** default to the lowest level that solves the problem, and move up only after the level below has proven itself in real use. If a decision doesn't *have* to be made by AI, don't let AI make it. Predictable beats clever.

**The day-one hire rules:** its own credentials, never yours. Read-only until write access is earned. Never signs as you. No personal logins, no banking. Scoped keys with the minimum permissions the job needs. A full trail of everything it did, spent, created, and deleted.

**How it fails:** silently. Nothing breaks on the day you skip this layer. It breaks three months later, in front of a client, in an email you never saw.

---

## Layer 5 — INITIATIVE (it moves before you ask)

The first four layers give you a very good assistant. This one is what makes it an operating system.

Note the word. Not cadence — cadence is just tempo, and a cron job that fires at 9am every morning has perfect tempo and zero initiative. The point of this layer isn't *how often* it runs. It's that the work happened and you didn't ask.

**What lives here:** anything that fires on a schedule or an event instead of on your prompt — a morning brief, a weekly review, a hook that runs when a file lands, a teammate who messages it directly and gets a real answer.

**In this kit:** hooks in `.claude/settings.json`, scheduled runs, and the weekly `/level-up` ritual that keeps the whole thing compounding.

**The test:** laptop closed. Something useful got done anyway, and it was right.

**Build rule:** last. Always last. Never put a schedule on something that doesn't already work reliably by hand — you'll automate a mistake and then go to sleep.

**How it fails:** built too early. An unproven workflow on a timer isn't autonomy, it's an unattended error running on a loop.

---

## Build order

```
MEMORY  ──▶  REACH  ┐
                    ├──▶  JUDGMENT  ──▶  INITIATIVE
             SKILL  ┘
```

**Memory first.** Non-negotiable. Every layer above it inherits its quality.

**Reach and Skill in parallel.** They feed each other — a new connection suggests a new skill, and a half-finished skill tells you which connection you actually needed.

**Judgment before Initiative.** This is the ordering that matters most and the one people get wrong. Deciding what the system is allowed to do has to come before letting it act unwatched. Reverse those two and you've hired someone, handed them the company card, and gone on holiday.

---

## Scoring yourself

`/audit` scores each layer out of 20 and ranks your gaps by leverage. Run it on Day 7 for a baseline, then weekly.

Expect a low first number. Most honest setups start in the 20s. The score is a direction, not a grade — the only thing that matters is that it moves.

| Total | Stage | What it means |
|---|---|---|
| 0-39 | **Foundation** | It knows some things. It can't do much yet. |
| 40-69 | **Trained** | Real memory, live data, a couple of workflows that hold. |
| 70-89 | **Trusted** | You reach for it first. Its authority is defined and it stays inside it. |
| 90-100 | **Autonomous** | Work gets done while you're not at the desk, and you sleep fine. |

Those stage names are the hire, all the way through. That's the point.

---

## The one test that matters

> **While you're away from your desk, your AIOS notices one real event and produces an output faster and more accurate than what you'd have produced yourself.**

Every layer exists to serve that sentence. Memory so it knows what the event means. Reach so it sees the event at all. Skill so it can act. Judgment so you can live with it acting. Initiative so it acts without you.

If something you're about to build doesn't move you toward that sentence, don't build it.
