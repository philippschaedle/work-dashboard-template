# {{cookiecutter.project_name}} — Operational Rules

This file defines how Claude Code manages work in this repo. Follow these rules automatically when working with files here.

## Core Principle: {{cookiecutter.primary_tracker_name}} + GitHub are primary, TASKS.md is secondary

**Source of truth, in order:**

1. **{{cookiecutter.primary_tracker_name}}** (the [main tracker]({{cookiecutter.primary_tracker_url}}) page and related pages) — tracked initiative work, its sections and task checkboxes.
2. **GitHub issues/PRs** in the key repos (`{{cookiecutter.key_repo_1}}`, `{{cookiecutter.key_repo_2}}`, and this repo's own `{{cookiecutter.github_username}}/{{cookiecutter.project_slug}}`) — tracked repo work.
3. **`TASKS.md`** — additional tasks and personal add-on information that exist **only here**, not on {{cookiecutter.primary_tracker_name}} or GitHub.

**TASKS.md is not a mirror of {{cookiecutter.primary_tracker_name}} or GitHub.** If a task is already a tracked checkbox or a GitHub issue/PR, it does not get a corresponding entry in TASKS.md — querying the tracker/GitHub directly (or checking DASHBOARD.md) is how you check its status. Copying it into TASKS.md would create two places that can drift out of sync, which is exactly what this rule prevents.

**What belongs in TASKS.md:**

- Personal/admin tasks with no project tracker at all
- Logistics/prep for an event that isn't itself a tracked deliverable
- A separate initiative the primary tracker doesn't cover at all (verify this — don't assume; check first)
- Personal context, decisions, or analysis that supplements a tracked item without duplicating the task itself — keep this in `notes/`, not as a duplicate TASKS.md task line

**Before adding anything to TASKS.md, check whether it already exists in the tracker or as a GitHub issue.** If it does, don't add it — if it needs more visibility, that's a DASHBOARD.md update, not a TASKS.md entry.

**This dashboard is a unified work dashboard** that integrates:

- **Key repos** — links to GitHub issues from your tracked repos (DASHBOARD.md)
- **Additional/personal tasks** — work with no tracker coverage (TASKS.md)
- **Meeting notes** — one file per event, captured under `notes/`
- **Progress log** — dated, one-line record of completed items (PROGRESS.md)

## Task Management Rules

1. **TASKS.md holds only what the primary tracker and GitHub don't.** Never create alternative task files, and never duplicate a tracked task or GitHub issue into TASKS.md.
2. **Organize by priority:**
   - **P1 (Immediate / Blockers)** — needs to happen now or blocks other work. Tag with time estimate: `[30m]`, `[2h]`.
   - **P2 (Scheduled / High Value)** — important, not urgent. Has a plan but no immediate deadline.
   - **P3 (Backlog / Someday)** — worth doing eventually, not scheduled.
3. **Group by topic**, matching tracker naming where the topic overlaps. Purely personal/admin items go under "Other."
4. **When a new task doesn't clearly map to an existing sub-heading, initiative, project, or repo — ask.** Don't silently default it to "Other."
5. **Before adding a task, check the tracker and GitHub first.**
6. **When tasks are complete:** check them off (`- [x]`), then remove from TASKS.md. Add a one-line entry to `PROGRESS.md` instead of a detailed archive.
7. **Other meaningful completed activity also gets a `PROGRESS.md` line** — e.g. filing/assigning a batch of GitHub issues, a sync that changed real state. Skip it for routine single actions.

## "What should I work on next?" Protocol

When asked this (or equivalent), DASHBOARD.md is a same-day cached index, not the live source:

1. Query GitHub live (assignee filter across your tracked repos)
2. Check the relevant tracker page(s) live
3. Check DASHBOARD.md's Blocking Issues and Key Repos for context — verify against live sources, don't substitute for them
4. Check `TASKS.md` P1 section for anything additional/personal
5. Cross-reference blockers — flag stuck work explicitly
6. Check for hard deadlines within the next 14 days
7. If nothing urgent, move to P2/backlog, favoring items with a time estimate that fits what's available
8. Present 1-3 concrete items — task, source, time estimate if known, why it matters
9. Sanity-check DASHBOARD.md freshness (Daily Sync) before answering

## Daily Sync

**DASHBOARD.md must be refreshed at least once per day.** If its "Last updated" date isn't today, run the sync: fetch the tracker pages, pull open issues/PRs for each key repo, update DASHBOARD.md, bump "Last updated," and reconcile TASKS.md against the refreshed state.

## Meeting & Note-Taking Rules

1. **Every event gets its own file in `notes/`**, named `notes/YYYY-MM-DD-event-title-in-kebab-case.md`, using the event's actual date.
2. Start each note with `# YYYY-MM-DD — Event Title`, then freeform notes below.
3. **Analysis and decision context belongs in `notes/`, not TASKS.md** — TASKS.md tracks the task, `notes/` holds the reasoning.
4. **Action items from notes:** check the tracker/GitHub before adding to TASKS.md.

## Repository & Issue Tracking

1. **DASHBOARD.md is the primary index** — links to GitHub issues/PRs from key repos and tracker pages.
2. **"Add"/"tag" someone on an issue means `@mention` them, not assign them.** Only touch the assignee field when explicitly told to "assign."
3. **For a larger topic, file a parent issue and hang concrete items off it as sub-issues**, instead of a flat list of similarly-named top-level issues.

## Git Workflow

**Do not commit automatically.** `git commit` is not run on your behalf in this repo.

Instead, track pending work as ready-to-run commands in `.claude/PENDING_COMMIT.sh` (gitignored — a working script, never part of history):

1. Whenever a change is finished, append a block: a `#` comment describing the change, then the `git add`/`git commit` lines for it. Keep each logical change as its own block.
2. Don't run `git add`/`git commit` or execute the script yourself — unless explicitly asked to in that moment.
3. **One block per file.** Stacking a second block for a file already targeted by an earlier, uncommitted block corrupts the intended diff — consolidate into the existing block instead.
4. At the end of a session, point the user at `.claude/PENDING_COMMIT.sh` so they can review and run it themselves.
5. Once a block has actually been run/committed, delete that block.

## Dates & Formatting

- **Always use absolute dates:** `2026-09-09`, not "Thursday" or "next week."
- **Time estimates on P1 tasks:** `[30m]`, `[1h]`, `[2h]`, etc.
- **Newest entries first** in chronological lists; `notes/` files sort by filename date.

## File Permissions

- `README.md` — do not edit (it documents the system)
- `CLAUDE.md` — this file; update only with new operational rules
- `.claude/settings.json` — pre-configured MCP tool access
- All other files (`DASHBOARD.md`, `TASKS.md`, `PROGRESS.md`, and everything under `notes/`) — edit freely to track work
