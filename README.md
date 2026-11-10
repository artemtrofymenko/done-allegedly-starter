# Done, Allegedly: the starter

Operating rules and a plain-file memory for Claude Code and Codex, for people who run agents
on their own projects and do not write code. Your agents start each session from the same
notes, write a handoff when they changed something, check results where they land, and ask
before anything irreversible. No server, no plugins, no scripts. It is text files, which is
both the point and the limit.

This is the free base of a larger kit. What the full kit adds is at the end.

## What is in the folder

```
AGENTS.md          the rules; Codex reads it directly, Claude Code through CLAUDE.md
CLAUDE.md          two import lines plus a few Claude Code notes
memory/            PROJECT-STATE, HANDOFFS, DECISIONS, INCIDENTS
TEST-RESULTS.md    how these files were tested, and what the numbers do not show
LICENSE.md         free to use and change; not for resale
```

## Was it tested?

Yes, and the method and limits are in `TEST-RESULTS.md`. Every claim there is a count of test
runs on small planted situations, three runs each. Three runs show whether a behaviour is
stable. They do not measure how often it fails in everyday work.

## What you need

- **Claude Code**, which needs a paid Claude plan (Pro or higher) or an API (Console) account;
  the free plan does not include it. Plans: https://claude.com/pricing
  Install: https://code.claude.com/docs/en/setup
- **Codex**, instead of Claude Code or next to it. Codex in the CLI or the IDE extension needs
  ChatGPT Plus or higher, or an OpenAI API key. Plans: https://learn.chatgpt.com/docs/pricing
  Install: https://github.com/openai/codex

Prices and plans change. Check the plan pages before you pay. One of the two tools is enough
for everything in this folder.

## Install

1. Download this repository (Code, then Download ZIP) and unzip it.
2. Copy `AGENTS.md`, `CLAUDE.md` and the `memory` folder into your project folder. If you are
   unsure, start with an empty practice folder. If your project folder already has files:
   - First copy your existing project folder to a backup.
   - If Windows asks to replace any existing file, choose Skip.
   - If your project already has a CLAUDE.md or AGENTS.md, read "Troubleshooting" below.
3. Before you start either agent, open `memory/PROJECT-STATE.md` in a plain text editor such
   as Notepad. Replace the example block, from "EXAMPLE - delete me" to "END OF EXAMPLE",
   including both marker lines, with this:

   ```
   Updated: [today] by me

   ## Current task

   ## Status

   ## Verified

   ## Human queue
   ```

   Put today's date in place of `[today]`. Write your task under "Current task" in one or two
   sentences, and under "Status" write that the work has not started. Save the file.
4. Open `memory/HANDOFFS.md`, `memory/DECISIONS.md` and `memory/INCIDENTS.md` in Notepad. In
   each one, delete everything from "EXAMPLE - delete me" to "END OF EXAMPLE", including both
   marker lines, and save.
5. Start a fresh session of Claude Code or Codex in your project folder (the folder itself, not
   a folder above it).
6. Check that the rules loaded.
   - Claude Code: type `/memory` to list the loaded files. Then ask: "What does AGENTS.md tell
     you to do at the start of a session?"
   - Codex: ask: "Summarize the current instructions." The answer should mention reading
     `memory/PROJECT-STATE.md` at the start of a session.
   - In either tool, ask: "Read memory/PROJECT-STATE.md and the last entry of
     memory/HANDOFFS.md, then quote the Current task." Check that it quotes the task you wrote
     in step 3. If it talks about a product feed or mugs, the example is still in the file.
7. Describe your task. When the work is done, say: "We are stopping here. Write the handoff
   and update the project state." Then open `memory/HANDOFFS.md` and read the new entry.

## What this does NOT do

- It does not enforce anything. The rules are context, and an agent can ignore them.
- It does not back up your files. The rollback line in a handoff is only as good as the backup
  it names.
- Neither tool loads the memory files by itself. Claude Code imports `memory/PROJECT-STATE.md`
  through CLAUDE.md. Codex reads the memory files only because AGENTS.md tells it to, so it can
  skip them.

## Troubleshooting

**The agent seems to have forgotten the project.**
Say: "Read memory/PROJECT-STATE.md and the last entry of memory/HANDOFFS.md first."

**Claude Code does not follow the rules in AGENTS.md.**
Open CLAUDE.md. The first line must be exactly `@AGENTS.md`, on its own line, with no quotes
or backticks around it.

**Your project already had a CLAUDE.md.**
Add the two lines `@AGENTS.md` and `@memory/PROJECT-STATE.md` at the top of your existing
CLAUDE.md instead of replacing it.

**Your project already had an AGENTS.md.**
Keep one file. Paste your old rules into this AGENTS.md, under a heading of your own.

**The agent follows a rule you did not write.**
Both tools also load personal instruction files from your user folder: `~/.claude/CLAUDE.md`
for Claude Code and `~/.codex/AGENTS.md` for Codex. Those combine with this project's rules.

## The full kit

The full kit is a one-time purchase on Whop. The link will be added here when the page is live.

It adds what this base leaves out:
- six skills, each a written procedure the agent follows step by step: spec-first,
  end-of-session, stop-and-audit, verify-where-it-lands, source-every-number, harvest;
- a prompt card with nine tested prompts, one per rule and two for the start and end of a
  session;
- a one-page spec template;
- a 48-page guide: each of the seven rules with the incident that produced it, how two agents
  share one project, Windows traps for non-coders, and a day-one checklist.

`TEST-RESULTS.md` shows the base and the full kit side by side, so you can see what the extra
parts changed in the tests before you decide.
