# corpus-keeper — Claude Code notes

## ⚠️ GitHub costs — ask before anything billable (firm policy, 2026-07-07)

**Claude: never trigger anything that can incur GitHub charges without Seth's explicit
approval AND a stated cost estimate first.**

- FREE, always: Actions on **public** repos with **standard** GitHub-hosted runners;
  self-hosted runners; GitHub Pages.
- METERED (free monthly quota, then paid): Actions in **private** repos (2,000 min/mo;
  **Windows counts 2×, macOS 10×**); Codespaces; Packages; Git LFS.
- **ALWAYS billable, even on public repos: larger / GPU runners** (anything beyond the
  standard `ubuntu-latest` / `windows-latest` / `macos-latest` tiers).
- Safety valve: with **no payment method on file, GitHub blocks usage at the quota and
  cannot bill** — keep it that way, or set stop-usage budgets.

So WITHOUT Seth's explicit OK (and cost), do **not**: add or change `.github/workflows/**`;
use a non-standard `runs-on:`; add a `schedule:` (cron) trigger; create Codespaces; use
Git LFS; publish private Packages; or change the plan / budgets. The local
`.git/hooks/pre-push` blocks workflow pushes (override `ALLOW_WORKFLOW_PUSH=1`) and
production-branch pushes (`ALLOW_MAIN_PUSH=1`) — set those flags only after Seth approves
that specific push. This repo is public; a `windows-latest` runner here is free.

## Branches

`main` is the release line; work happens on `dev` (create from `main` on first touch).

## What this is

See README.md and plans/corpus-keeper.md. The FLEx side needs flexlibs2 + LibLCM, Windows only:
verified facts about the FLEx data model go in docs/FACTS.md (the pattern from the flextools repo).
Related work in the FLExText suite (rulingAnts/flextext-editor): #49 (the FLEx-backed audio
segmenter, which uses this library as its sidecar) and the suite changes listed in the plan.
