# DECISIONS

What goes in: every decision where one option was chosen over another, including who owns
which files when two agents share the project. Record what was rejected too, so a later
session does not propose it again as new.
Append-only: add new entries at the bottom. To reverse a decision, add a new entry that says
which one it replaces.
What never goes in: secrets (passwords, keys, tokens, card numbers, private links), raw chat
transcripts. A decision the human made is recorded only after the human made it; an agent's
guess about what the human wants is not a decision.

Format:

    ## [date] | [decision in a few words]
    - Decision:
    - Chosen:
    - Rejected:
    - Why:
    - Who decided:

---

EXAMPLE - delete me

## 2026-03-10 | Who writes the feed and the newsletter
- Decision: which agent writes which folder, now that two agents work on the shop.
- Chosen: Claude Code writes `feed/`. Codex writes `newsletter/`. Both may read everything.
- Rejected: both agents edit both folders. Two writers on one file overwrite each other.
- Why: one writer per file (AGENTS.md, section 3). The feed and the newsletter rarely need the
  same file, so the split costs little.
- Who decided: the shop owner, in chat on 2026-03-10.

END OF EXAMPLE
