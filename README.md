# AIOS — an AI Operating System starter kit for Claude Code

A free, MIT-licensed kit that turns Claude Code into your personal **AI Operating System**.

Not a chatbot you visit. A system that knows your business, reaches your tools, does your repeatable work, and eventually runs some of it without being asked.

Built for operators — solo founders, small-business owners, managers, consultants, creators. You do not need to be a developer. If you can clone a folder and answer seven questions out loud, you can run this.

---

## The one test that matters

> **While you're away from your desk, your AIOS notices one real event and produces an output faster and more accurate than what you'd have produced yourself.**

Every decision in this kit rolls up to that sentence. If a layer, skill, or file doesn't move you toward it, it doesn't ship.

---

## How you'll know it's working

There's no clean metric for this. But three things start happening in your week, and you feel all three.

**Someone asks you a question, and you ask your AIOS too.** Not because you're busy. Because you know it'll answer better, faster, and with the actual source. That's the day you stop being the bottleneck for your own knowledge.

**You stop opening tabs.** Something lands, and your first move is to ask, not to go hunting across six apps. The default surface for thought work quietly changes.

**You stop trying to remember things.** What you decided last quarter, what the client said in that meeting. You trust the retrieval. It holds the facts, you hold the questions.

---

## Two frameworks

**The Shift first. The Stack second.** Without the rewire, the architecture is just a folder structure.

### The Shift — the operator brain (how you think)

| Move | One-liner |
|---|---|
| **Question** | Stop asking *"how do I do this?"* Start asking *"can AI do this faster than me?"* Break the job into pieces. Never accept output blindly. |
| **Cut** | Find the constraint → eliminate before you automate → map the process → lowest autonomy that works → tie it to a number. |
| **Build** | Context before tools. Small blocks, validate each step, simplest connection that holds, roll it out like training wheels. *Boring wins.* |

Full breakdown in [`references/the-shift.md`](references/the-shift.md). `/level-up` walks you through it weekly until it's reflex.

### The Stack — the architecture (what you build)

Five layers. Read them as the five things you'd assess in someone you just hired, because that's what they are.

| # | Layer | It means | You'll know it's in place when |
|---|---|---|---|
| 1 | **Memory** | It knows your business | A cold session answers *"what do we do, who works here, what did we decide in June?"* |
| 2 | **Reach** | It touches your tools and data | *"What's due this week?"* returns live data — and it can write, not just read |
| 3 | **Skill** | It knows how to do the work | A short phrase produces a finished artifact, the same shape every time |
| 4 | **Judgment** | It knows what it may decide alone | Every workflow has a named autonomy level, and nothing runs above the level you proved |
| 5 | **Initiative** | It moves before you ask | You didn't prompt it. The work was done anyway |

Build order: **Memory first** — everything above inherits its quality. Reach and Skill in parallel. **Judgment before Initiative** — decide what it's allowed to do before you let it act unwatched. Reverse those two and you've handed a new hire the company card and gone on holiday.

Full breakdown in [`references/the-stack.md`](references/the-stack.md). `/audit` scores all five, 20 points each.

---

## What ships — 3 skills

Lean on purpose. One sets you up, two keep you compounding.

| Skill | Type | When to run |
|---|---|---|
| `/onboard` | Setup wizard, one-time | Day 1, right after you clone. A 7-question interview, ~15 minutes. Writes your Day-1 files and fills `CLAUDE.md`. |
| `/audit` | Recurring, structural | Day 7, then weekly. Scores the five layers out of 100 and ranks your gaps by leverage. Read-only. |
| `/level-up` | Recurring, functional | Day 14, then weekly. The Shift interview. One run = one shipped automation. |

`/audit` asks *"is this built right?"* `/level-up` asks *"what leverage am I still missing?"* Run them in that order — fixing structure first makes the capability planning worth doing.

You add every skill after these three yourself, through `/level-up`. That's the design.

---

## Quick start

1. **Install [VS Code](https://code.visualstudio.com)** and add the **Claude Code** extension. Sign in.
2. **Clone this repo** into a folder you'll actually keep, and open it in VS Code.
3. **Run `/onboard`.** Answer the seven questions honestly. Voice samples get pasted, not typed — that rule is real, see below.
4. **Use it for a week.** Bring it real questions and real decisions. Log the decisions in `decisions/log.md`.
5. **Day 7 — run `/audit`.** Take the score. Close the top gap.
6. **Day 14 — run `/level-up`.** Ship the one automation it surfaces.
7. **Every week after** — `/level-up` on a Friday. One shipped thing per week. A year of that compounds into something no SaaS subscription gives you.

**About the voice samples:** `/onboard` will ask you to paste two things you've written recently — an email, a post, a DM. Paste them raw. Don't type fresh prose into the chat, because anything you write mid-conversation is already shaped by the conversation, and you'll teach it a voice that isn't yours.

---

## Repo layout

```
AIOS/
├── README.md
├── CLAUDE.md                     ← Your operating manual. Filled by /onboard.
├── EXPANSIONS.md                 ← What to add as you outgrow the base
├── LICENSE
├── .gitignore
├── aios-intake.md                ← Source of truth for /onboard. Edit + re-run any time.
├── connections.md                ← Registry of every system your AIOS can reach
├── context/                      ← About you, your business, your quarter
├── references/
│   ├── the-shift.md              ← The operator brain (Question · Cut · Build)
│   └── the-stack.md              ← The architecture (Memory · Reach · Skill · Judgment · Initiative)
├── decisions/
│   └── log.md                    ← Append-only: what was decided, and why
├── archives/                     ← Old stuff. Don't delete. Move it here.
└── .claude/
    └── skills/
        ├── onboard/SKILL.md
        ├── audit/SKILL.md
        └── level-up/SKILL.md
```

[`EXPANSIONS.md`](EXPANSIONS.md) covers what to add later — `projects/`, `templates/`, `scripts/`, `.claude/agents/`, sub-OS folders — and, just as usefully, what never to add.

---

## A note on wiring tools

The kit ships with nothing connected. That's deliberate — Day 1 is Memory, Day 2 is Reach.

When you do wire something, prefer a thin command or script you call on demand over a heavy integration that loads its entire toolset into every session. One costs you tokens when you use it. The other charges rent on every conversation you ever have. Then write down what you learned in `references/{tool}-api.md`, so the next skill you build doesn't have to figure out the same API twice.

---

## License

MIT. See [`LICENSE`](LICENSE). Use it, fork it, teach it, sell what you build with it.

---

Built by [Toffer Lorenzana](https://post205.com) — POST205, Manila.
