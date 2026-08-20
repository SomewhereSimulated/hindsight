# Full Walkthrough

How this skill behaves, start to finish — what it looks at, what it keeps,
what it throws away, and why it's built the way it is.

---

## What it does, in one line

At the end of a session, it separates the handful of lessons that would
genuinely change how future work gets handled from everything else that
just happened — and writes only those down.

## Why a filter, not a log

The easy version of this skill would just summarize the session: what got
built, what broke, what got fixed. That's not what this does. A running
list of "here's everything that happened" gets noisy fast and stops being
useful — nobody re-reads a hundred session summaries looking for the one
rule that mattered. This skill's whole job is compression: read everything,
keep only what would change *future* behavior, and phrase each surviving
lesson as a concrete rule, not a narrated event.

That's also why it's read-only against the actual work. It doesn't
re-verify a fix, re-run a test, or second-guess a decision that was already
made — it only asks "what should be done differently next time," which is a
different question than "was this session's work correct."

---

## The six-step pass

### 1. Find genuine process failures, not surface symptoms

For anything that took more than one attempt, the question isn't "what went
wrong" — it's "what single upstream change would have prevented the *whole*
chain of attempts." A mistake that came from missing information available
at the time is different from one that came from skipping a step, assuming
instead of asking, or checking the wrong thing. Only the second kind
produces an actionable lesson.

### 2. Separate durable lessons from one-off noise

A lesson earns a place in memory only if it would change how a *different*,
future task gets handled — not just re-litigate this one. Anything that's
purely about this session's specific content, with no bearing on method or
process, gets discarded here. What survives gets stated as a precise rule:
what question to ask, at what point, or what check to run — and why the
check that was actually used fell short.

### 3. Verify before writing anything down

Any lesson that references a specific tool behavior, a file, or a technical
constraint gets checked against what actually happened in the session, not
reconstructed from memory. A single failure doesn't get written up as a
universal rule — the pass distinguishes "this happened once, might be a
fluke" from "this failed the same way twice, that's a real pattern."

### 4. Persist, don't just narrate

This is the step that actually writes something down — see "Where lessons
get saved" below for the mechanics. Before creating anything new, it checks
whether an existing memory already covers the same topic; if so, that entry
gets extended in place instead of a near-duplicate getting created next to
it.

### 5. Keep the scope honest

A few well-reasoned, specific lessons beat a long list of shallow ones. A
session that genuinely went fine gets told exactly that — "nothing worth
changing" is a valid, complete result, not a failure to find something. Real
environment findings (a tool that didn't behave as documented, a permission
that turned out more restrictive than expected, a connector that failed)
get recorded as factual findings, kept distinct from process lessons about
how the *work* was approached.

### 6. Report back concisely

The final message to the user is a few short sections — the lessons that
got kept, and their practical effect going forward. Not a restatement of
the whole session.

---

## Where lessons get saved

The skill checks, at run time, whether the current environment actually has
a persistent memory system before deciding how to save anything:

**If one exists** (this skill was built against Claude Code's, but the
principle generalizes): lessons get written as discrete, well-labeled
entries in that system, one topic per entry. The skill browses what already
exists first — an existing entry on the same topic gets a dated addition
appended to it, matching its existing structure, rather than a new
near-duplicate file. Every new or newly-touched entry gets reflected in
whatever serves as that system's index, so nothing written is orphaned and
invisible next session.

**If none exists:** the retrospective gets produced as a single, clearly
organized standalone document instead — written so it stands on its own
without the original conversation as context, ready for the user to save
wherever they keep notes.

## What "done" looks like

- Every lesson kept traces back to a specific, real event from the
  session — not a generic best practice restated because it sounded right.
- Nothing written duplicates a topic an existing memory already covers.
- The memory index (or equivalent) reflects every new or changed file.
- The report to the user is short: lessons and their practical effect, not
  a full recap.
- A session with nothing durable to report says so plainly.

## What it never does

Doesn't redo, re-verify, or re-open any task from the session — it only
reviews and reports on work already done. Doesn't touch project code or
content as a side effect of running. Its only writes, ever, are to memory
(and that memory's index).

## Credits

**Jeffrey Smith**
Email: jeffrey@efficientstreet.com
YouTube: https://youtube.com/@JeffreyEntrepreneur
Website: https://efficientstreet.com
