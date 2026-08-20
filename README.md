# Hindsight
### By Jeffrey Smith - efficientstreet.com

A self-improvement skill for AI coding assistants. At the end of a session,
it reviews everything that actually happened — the tasks, the corrections,
the dead ends — pulls out the lessons that would genuinely change how future
work gets handled, and saves the durable ones as persistent memory. Not a
journal of what got done; a filter for what's worth remembering.

**Read [GUIDE.md](GUIDE.md) for the full walkthrough of how it thinks
through a session and what it will and won't write down.**

---

## What you get

- **One trigger, one pass** — "get some hindsight" (or equivalent phrasing)
  reviews the whole session end-to-end, not just the last exchange.
- **Root causes, not symptoms** — for anything that took multiple attempts,
  it asks what single upstream fix would have prevented the whole chain,
  instead of just noting that a mistake happened.
- **A real filter, not a transcript** — one-off content specifics get
  discarded; only lessons that would change how a *future* task gets handled
  get kept. A clean session gets told "nothing to report," not padded
  filler.
- **Updates in place** — before writing a new memory entry, it checks
  whether an existing one already covers the topic and extends that instead
  of creating a near-duplicate.
- **Never redoes work** — strictly read-only against the session's actual
  tasks. Its only writes are to memory (and whatever indexes that memory).
- **Portable** — no project-specific content baked in. It works the same way
  regardless of what the session was actually about.
- **Pays for itself in tokens, not just tidiness** — a lesson written down
  once means a future session doesn't re-spend tokens rediscovering it
  through the same trial and error, re-litigating a question that was
  already settled, or repeating a correction you already made. The saving
  compounds: the more sessions an assistant runs, the more that accumulated
  memory shortens the average one.

## Requirements

- An AI coding assistant with some form of persistent, file-based memory
  across sessions (this was built for and tested against **Claude Code**'s
  per-project memory folder). It also degrades gracefully — see
  [GUIDE.md](GUIDE.md) — to a standalone written report if no such memory
  system is present.
- Nothing else. No API keys, no external services, no dependencies.

## Install

Copy `SKILL.md` into your assistant's skills folder.

**Claude Code:**
```bash
mkdir -p .claude/skills/hindsight
cp SKILL.md .claude/skills/hindsight/SKILL.md
```

Or install it once at the user level so it's available in every project:
```bash
mkdir -p ~/.claude/skills/hindsight
cp SKILL.md ~/.claude/skills/hindsight/SKILL.md
```

## Use it

Trigger it in conversation any time you want a session reviewed:

> "Get some hindsight."
> "What should we improve?"
> "Review today and notate lessons."
> "What did you learn today?"
> "Save what's worth remembering from this session."

It's deliberately **on-demand only** (`disable-model-invocation: true` in
the frontmatter) — a hindsight pass writes persistent memory, so timing
stays your call, never something the assistant decides to run on its own.

## Tuning it to your own setup

The "In this environment" section of `SKILL.md` names Claude Code's memory
layout specifically (`~/.claude/projects/<project-slug>/memory/`,
`MEMORY.md` as the index). If your assistant or harness stores persistent
memory somewhere else, or under a different format, replace that section
with the equivalent path/convention for your setup — the rest of the skill
(steps 1–6, the definition of done, the scope boundary) is assistant-agnostic
and shouldn't need to change.

## License

MIT — see [LICENSE](LICENSE).

## Credits

**Jeffrey Smith**
Email: jeffrey@efficientstreet.com
YouTube: https://youtube.com/@JeffreyEntrepreneur
Website: https://efficientstreet.com
