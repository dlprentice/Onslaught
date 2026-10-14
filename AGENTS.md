# Onslaught (fork): agent guide

Read this before changing anything. It is the only instruction file in the repo; `CLAUDE.md` just points here.

## What this is

David's fork of Stuart Gillam's `stuart73/Onslaught`: the original C++ source of *Battle Engine Aquila*
(Lost Toys), published by Stuart under GPL-3.0 (`LICENSE`). The source is in one flat
directory: the game and engine, the PC layer (`PC*.cpp`, `DX*.cpp`, `d3dapp.cpp` from Microsoft's Direct3D 8
sample framework) and the Xbox layer (`XBoxMemoryCard.cpp`, `_XBOX` blocks). There is no build system: no
solution, makefile or CMake file exists, and the code needs DirectX 8 and the Xbox SDK, so it is not built on
this laptop. It is reference material, read and cited, never run. Stuart's October 14, 2026
update (`b3b771091fd1c5a4708c1762d8472e7ca565f599`) adds 21 mesh source/header files;
none of the previously published files changed in that update.

Remotes: `origin` is `dlprentice/Onslaught` (default branch `main`), `upstream` is
`stuart73/Onslaught`. The fork is `upstream/main` plus this guide and `CLAUDE.md`; every source commit is Stuart's.

## How it is used

`~/Projects/game-dev/Onslaught-Career-Editor` vendors this fork as the submodule `references/Onslaught`, pinned
at an exact commit recorded by the consuming repository's Git link. That repo treats it as its
`SOURCE` evidence tier: its docs, C# rebuild and tests cite
`references/Onslaught/<file>:<line>` (see `DOCUMENTATION.md`, `rebuild/PARITY.md`, `rebuild/PROVENANCE.md`,
`patches/catalog/patches.v2.json`), `tools/aya_extractor_source_audit.py` refuses to run unless the submodule
is at its `ONSLAUGHT_PIN`, and `npm run test:safety` scans the submodule files. Its `CONTRIBUTING.md` says to
keep the pin unless the authorized task includes that source-reference update. An instruction-only edit
to this standalone fork does not require advancing the consuming project's pinned source snapshot.

## Rules

- Treat this as upstream code. No reformatting, renaming, translating or "fixing": line numbers are
  load-bearing citations in the editor repo.
- Useful feature branches and repo-local worktrees are allowed. Push small verified changes to the existing
  origin; do not force-push. An instruction-only change does not advance a consuming source pin.
- If the authorized task also adopts changed source in Onslaught-Career-Editor, update its
  `references/Onslaught` pointer and `ONSLAUGHT_PIN` in `tools/aya_extractor_source_audit.py`, then run
  that audit and `npm run test:safety`. Coordinate adoption with the consuming repository's owner;
  a standalone fork edit does not authorize changing the consumer.
- Never rewrite history here: the submodule pin must always resolve. Take upstream changes with
  `git fetch upstream` and a merge of `upstream/main` into `main`, not a rebase.
- Keep `LICENSE` and provenance intact; nothing from this tree is copied into the MIT-licensed parts of the
  editor repo.
- Nothing here needs `local-data/`; the repo has no generated output.
