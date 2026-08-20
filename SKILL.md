---
name: hindsight
description: Reviews everything accomplished in the current session end-to-end, distills genuine process lessons (not one-off content specifics), and saves the durable ones as persistent memory — updating an existing related memory in place rather than duplicating it. Trigger on "get some hindsight," "run a hindsight pass," "what should we improve," "review today and notate lessons," "what did you learn today," "save what's worth remembering from this session." Does not redo or re-open any of the session's actual work, and never fabricates a lesson just to have something to report.
allowed-tools: Read, Write, Edit, Glob, Grep
disable-model-invocation: true
---

# Hindsight

A session-end self-improvement pass. Read-only against the session's actual
work — it never redoes or re-opens a task — and write-only against memory.
User-triggered only: a hindsight pass writes persistent memory, so timing
stays the user's call, never something run on a hunch.

## When this fires

On-demand only: "get some hindsight," "run a hindsight pass," "what should
we improve," "review today and notate lessons," "what did you learn today,"
"save what's worth remembering from this session."

## Process

Review the full body of work completed in this session — every task,
decision, correction, and course-change from start to finish, not just the
most recent exchange. Then produce a structured hindsight report covering
the following:

1. **Identify genuine process failures, not just outcomes.** For each
   meaningful mistake, inefficiency, or round of back-and-forth correction,
   name the root cause — not the surface symptom. If something took multiple
   attempts to get right, ask what specifically caused each failed attempt,
   and whether a single upstream fix (a question asked earlier, a check
   performed differently, a different verification method) would have
   prevented the whole chain. Distinguish between mistakes that were
   reasonable given the information available at the time, and mistakes
   that came from skipping a step, assuming instead of asking, or verifying
   the wrong thing.

2. **Separate durable lessons from one-off noise.** A lesson is worth
   keeping only if it would change how a future task gets handled — not
   just this one. Discard anything that's purely specific to this session's
   content and has no bearing on method or process going forward. For each
   lesson that survives that filter, state it as a concrete, actionable
   rule — not a vague sentiment like "be more careful." Say precisely what
   should happen differently: what question should be asked, at what point,
   or what check should be performed, and why the check that was actually
   used wasn't sufficient.

3. **Verify claims before writing them down.** If a lesson references
   specific behavior, a tool's output, a file, or a technical constraint,
   confirm it against what actually happened in this session rather than
   reconstructing it from memory. Don't generalize from a single data point
   into a universal rule — note when something might be a one-time fluke
   versus a confirmed, repeatable pattern (e.g., something that failed
   identically on a second attempt is a stronger signal than something that
   failed once).

4. **Persist the lessons, don't just narrate them.** If a persistent memory
   or notes system is available, write each surviving lesson into it as a
   discrete, well-labeled entry — check first whether an existing note
   already covers the same topic and update it in place rather than
   creating a near-duplicate. If no persistent memory system exists,
   produce the hindsight report as a clearly organized, standalone document
   the user can save themselves, written so it remains useful without the
   original conversation as context.

5. **Keep the scope honest.** A handful of well-reasoned, specific lessons
   is more useful than a long list of shallow ones. If a session genuinely
   went well with nothing worth changing, say so plainly rather than
   manufacturing findings to fill space. If real infrastructure or
   environment constraints were discovered (a tool that doesn't work as
   documented, a permission that's more restrictive than expected, a
   connector that failed to connect), record those as factual findings
   distinct from process lessons about how the work itself was approached.

6. **Report back concisely.** After persisting or writing up the hindsight
   report, summarize for the user in a few short sections what was learned
   and what will change — not a restatement of the whole session, just the
   lessons and their practical effect on future work.

## In this environment

Check whether a persistent memory system is actually available before
assuming step 4's fallback — most agent harnesses that have one expose it
distinctly from ordinary project files:

- **Claude Code** keeps per-project memory under
  `~/.claude/projects/<project-slug>/memory/` (the slug is derived from the
  project's working-directory path — different per project, not a fixed
  path), one markdown file per fact, each with `name`/`description`/
  `metadata.type` frontmatter. `type: feedback` fits nearly every hindsight
  lesson — it's guidance on how to work, with a why. That same folder's
  `MEMORY.md` is the index loaded into every session.
- **Whatever the mechanism, the same rule applies:** read the index or
  browse existing entries first, to find one that already covers the
  lesson's topic. Existing topic → edit that file (append a dated addendum
  or finding, matching its existing structure) rather than creating a new
  one. New topic → new atomic file, one fact per file, cross-linked to
  related entries if the system supports it.
- Every new or newly-relevant file needs a matching entry added to whatever
  serves as the index — a memory nothing points to is easy to miss next
  session.
- If no such system exists in the current environment, fall back to step
  4's standalone-document path — write the hindsight report as one
  self-contained file the user can save wherever they keep notes.

## Definition of done

- Every persisted lesson traces to a real, specific event from this
  session — not a generic best practice restated.
- Nothing written duplicates an existing memory's topic; existing entries
  were checked and updated in place where one already applied.
- The memory index (or equivalent) reflects every new file.
- The final report to the user is a few short sections, not a full session
  recap — lessons and their practical effect, nothing else.
- If nothing genuinely durable came up, the report says so plainly instead
  of manufacturing filler.

## Scope boundary

This skill does not redo, re-verify, or re-open any task from the session —
it only reviews and reports on work already done. It does not edit project
code or content as part of running; its only writes are to memory (and the
memory index).
