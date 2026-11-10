# AGENTS.md: operating rules for every agent in this project

Codex reads this file directly. Claude Code reads it through the `@AGENTS.md` line in CLAUDE.md.
Each rule has one line of why. Keep this file under 150 lines: a patch that adds a rule removes
the wording it replaces.

## 1. Start of session

Before any other work, read `memory/PROJECT-STATE.md` and the last entry of `memory/HANDOFFS.md`
(entries are appended, so the last one is at the bottom).
Why: you remember nothing from earlier sessions; these two files are the only bridge.

Before you change anything a decision or an incident covers, read `memory/DECISIONS.md` and
`memory/INCIDENTS.md`.
Why: an option that was already rejected looks fresh to a new session; the log says why it lost.

If a memory file is missing or empty, say so and continue. Never invent its contents.
Why: an invented state is worse than a known gap.

## 2. End of session

Before you stop, if this session changed a file, append one entry to `memory/HANDOFFS.md` and
overwrite `memory/PROJECT-STATE.md`.
Follow the format in each file's header. Verified means you saw the result where it lands;
anything unchecked or left incomplete goes under Not verified or Next for human.
A session that only read and changed nothing writes no handoff and leaves `PROJECT-STATE.md`
alone: tell the human what you found instead, including anything in the memory files that is
out of date.
Why: the next session starts from these files; work that is not written down is lost to it.
A read-only entry would push the last real handoff out of the "last entry" the next session reads.

## 3. One writer per file

When two agents share this project, each file has one writer. The human decides who owns what;
record it in `memory/DECISIONS.md`.
Why: two agents editing one file overwrite each other, and neither notices.

- If you need a change in a file you do not own, put the request in your handoff.
- Only one agent writes any file in `memory/` at a time. Sessions end one at a time: the second
  agent starts its end-of-session step only after the first has finished its handoff and state
  update. The second agent then re-reads `HANDOFFS.md` and `PROJECT-STATE.md` before it writes.
- `HANDOFFS.md`, `DECISIONS.md` and `INCIDENTS.md` are shared: add your entry at the end, never
  edit another agent's entry.
- `PROJECT-STATE.md` is written by both: read it right before you overwrite it, and keep the
  other agent's lines that are still true.

Why (for the memory files): a fresh read is not a lock. If two agents read a file and then both
write it, the first write is lost. Append-only describes the record format; it does not prevent
concurrent writes.

## 4. The seven rules

1. **Written is not in effect.** After you change a value, read it back where its consumer reads
   it (the program, the page, the scheduled job), not where you wrote it.
   For things that fail silently (alerts, mail forwarding, scheduled jobs), fire one end to end.
   Why: a write can succeed while the consumer reads a different file, field or copy.

2. **Check where the result lands.** "Done" means you saw the result at its destination: the file
   opened from disk, the page loaded. For a message, "Sent" verifies only the sender side: check
   delivery at the recipient when you can; otherwise write "delivery not verified: recipient
   inbox not checked". Before you rely on a field from someone else's system, compare a few
   records with their original source.
   Why: a success message comes from the same tool that may have failed.

3. **Claims only the human can confirm: ask.** What the human owns, decided, paid, sent or stored
   has no file you can check. Ask, or write it as an open question. Never state it as fact, and
   never write it into memory as fact. If you record what the human told you, write it as their
   words with a mark, for example "Owner says the plan is paid (not confirmed)", and do not
   build on it as settled ("record the paid plan").
   Why: once it is in memory, a guess reads like a verified fact to every later session.

4. **No invented number passes as a finding.** Every number you estimated, guessed or chose,
   rejected options included, is marked guess (what it rests on) or proposal (why). Every price,
   total, rate, limit or date a decision rests on names its source or shows its calculation.
   Why: an unlabelled number you chose gets treated as a finding.

5. **Stop and audit.** Stop when the same approach has failed twice in a row, when you are about
   to make a third attempt at the same artifact, or when the human is frustrated. Then list your
   beliefs, each marked evidence or assumption, and test the cheapest assumption first.
   Why: a third variation built on the same false belief fails the same way.

6. **Approval only for the irreversible.** Ask the human and wait for a clear yes before you
   publish, send, spend money, delete, or change anything outside the project folder (other
   folders, accounts, settings, other people's systems). When you ask, name exactly what the
   step touches: each file, each recipient, each amount. Reading and research are fine, with a
   request cap per website: stop at that site's first refusal (403, 429, captcha, login wall).
   If a program or its docs say it sends, treat running it as sending, even if the code you can
   see only writes a file.
   Everything else inside the project folder: do it, then report it. Having a tool (a browser,
   a terminal, a login) is not permission to use it for an irreversible step.
   Why: these steps cannot be undone by editing a file; everything else can.

7. **No secrets in any file, ever.** Never write passwords, API keys, tokens, card numbers or
   private links into any file in this project, memory and handoffs included. If a task needs
   one, ask the human to supply it outside these files. Never print the contents of a key or
   credential file; check a key by whether the program that needs it works.
   Why: these files get copied, shared and pasted into chats, and a secret leaks with them.

## 5. Size the ceremony to the work

- Small, clear work (a typo, one obvious fix, a value the human already gave): do it, then verify it.
- Bigger work (several steps or files, an unclear goal), work that runs while the human is away,
  or anything irreversible: write a one-page spec first (goal, inputs, output, done-criteria,
  out of scope, rollback), ask about anything unclear, get the human's explicit yes, then start.
  That yes approves the plan; each irreversible step in it still gets its own yes (rule 6).
- If you are unsure which size it is, treat it as bigger.

Why: a one-page spec is short; rebuilding the wrong thing is not.

## 6. Where things go

| What | Where |
|---|---|
| A decision: one option chosen over another | `memory/DECISIONS.md` |
| An incident: something went wrong because of a false belief | `memory/INCIDENTS.md` |
| A lesson worth keeping: hard to learn, or a workflow done twice | a rule in this file, one short line |
| What one session did | `memory/HANDOFFS.md` |
| Current task, status and the human's queue | `memory/PROJECT-STATE.md` |
| A spec for bigger work | `specs/[task-name].md` |

Never in any of these files: secrets, raw chat transcripts.
Why: one place per kind of record means the next session knows where to look.

## 7. The human's queue

The "Human queue" section of `memory/PROJECT-STATE.md` lists only what the human must do: a
decision, an approval for an irreversible step, a login or payment, a physical action.

- One line per item: what to do, and why it needs the human.
- Never in the queue: finished work, explanations, notes for later, anything an agent can do.
- Before you repeat an item, check that it is still open. Remove items that are done.

Why: the human reads this list every session; every line that is stale or agent work hides a real one.
