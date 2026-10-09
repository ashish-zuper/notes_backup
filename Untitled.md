# Personal Coding Guidelines

## Database access

Never run a database query without explicit user approval — this
covers reads as well as writes, every environment (local, staging,
production), every store (MongoDB, MySQL, Redis), and every access
path (`mongosh`/`mysql` CLIs, one-off scripts, migrations, MCP or
other tooling).

Instead: show the exact query you intend to run and wait for the
user to approve it. Approval is per-query — an earlier "yes" does
not carry over to the next one.


## Changelog tracking (Obsidian daily log)

After every `git commit` made on the user's behalf, append a single entry to
today's Obsidian daily note:

- **File:** `/home/ashishbinu/Documents/Notes/notes/Daily Logs/<YYYY-MM-DD>.md`
  - `<YYYY-MM-DD>` is today's **local** date — the same file the Obsidian
    daily-notes button opens (the plugin's folder is `Daily Logs`).
  - Create the file if it does not exist.
- This is the single source of truth — do **not** write `~/.claude/CHANGELOG.md`
  or any per-repo `CHANGELOG.md` anymore.

### Format

- The daily note also holds the user's own hand-written notes. Append only
  inside a dedicated `## Dev log` section — never touch anything outside it.
  - If a `## Dev log` heading already exists in the file, append to the end of
    that section.
  - If it does not exist, add `## Dev log` at the end of the file and start it.
- Group a session's related commits under a `### <ticket-or-branch> — <short
  theme>` subheading so the day is scannable, then write a few short, meaningful
  bullets that capture *what was done and why* — the way the user would jot it.
  No file lists, no release-note prose, no one-bullet-per-commit.
- Directly under each subheading, add a single compact metadata line carrying
  the traceability (Obsidian renders this as one wrapped line):
  - `*Repo:* `<basename>` · *Branch:* `<branch>` · *Ticket:* [<id> — <title>](<linear-url>) · *Commits:* `<sha>` `<sha>` ...`
  - Repo basename: `basename "$(git rev-parse --show-toplevel)"`. Branch:
    `git rev-parse --abbrev-ref HEAD`. List every short SHA the bullets cover.
  - Ticket: derive the Linear id from the branch/commit prefix (e.g. branch
    `API-4458` → ticket `API-4458`); fetch its title + URL via the Linear MCP
    (`get_issue`). If there's no ticket or Linear is unreachable, drop the
    `*Ticket:*` field.
- Append newer work below older work so the section reads top-to-bottom as the
  day progressed.

### Summary rules

The summary must be self-contained — a teammate reading it cold, with no access
to the conversation that produced the change, should understand it.

- Write like a short release note: what changed and the user-visible effect or
  motivation.
- No internal session terminology — phase names, variable names, map names,
  function names that aren't part of the public API.
- No "as discussed", "as requested", "per our chat", or other references to the
  conversation.
- No spec-ID anchors that decay over time.

### Do not append for

- Read-only exploration (grep, file reads, planning sessions).
- Failed or reverted attempts that left no committed diff.
- Trivial cosmetic edits the user did not ask for.
- Commits the user explicitly tagged as no-log.

### Pure reverts

If a commit is a pure revert that cancels out an earlier entry in the **same
day's** `## Dev log`, remove the original entry rather than appending a new
"reverted X" line — the two would cancel out on review anyway. If the original
entry is in an earlier day's note, leave that note alone and add a normal
"reverted X" entry to today's Dev log.
