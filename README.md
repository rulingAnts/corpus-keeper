# Corpus Keeper

One small program that keeps a language-documentation corpus in step across the tools that each do
one job well: **FLEx** (text and analysis, the source of truth for everything its model holds),
**lameta** (the archive record and the home of the recordings), the **FLExText suite** (recording,
transcription, audio segmentation, consent capture, the researcher panel) and the **corpus
checklist** (genre coverage and workflow progress).

- The plan, approved 2026-09-06: [plans/corpus-keeper.md](plans/corpus-keeper.md).
- Phase 1 is a FLExTools module run on demand with FLEx closed, plus an Outbox and an Inbox folder.
  Phase 2 is a resident tray app with a localhost bridge for the researcher panel; Mac hosts reach
  it through [one Parallels port-forwarding rule](docs/parallels-port-forwarding.md).
- Windows only for the FLEx side (flexlibs2 + LibLCM); the library is plain Python 3.10+.

Copyright © 2026 Seth Johnston. Licensed under the [GNU AGPL v3.0](LICENSE). Other licensing
options are available to partner organisations and individuals for their own work, case by case,
on request, through <https://flextext.app/contact>.
