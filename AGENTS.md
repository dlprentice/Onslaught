# Onslaught (fork): agent guide

Read this before changing anything. It is the only instruction file in the repo; `CLAUDE.md` just points here.

## What this is

David's fork of Stuart Gillam's `stuart73/Onslaught`: the original C++ source of *Battle Engine Aquila*
(Lost Toys), published by Stuart under GPL-3.0 (`LICENSE`). It is 108 files, about 50,900 lines, in one flat
directory: the game and engine, the PC layer (`PC*.cpp`, `DX*.cpp`, `d3dapp.cpp` from Microsoft's Direct3D 8
sample framework) and the Xbox layer (`XBoxMemoryCard.cpp`, `_XBOX` blocks). There is no build system: no
solution, makefile or CMake file exists, and the code needs DirectX 8 and the Xbox SDK, so it is not built on
this laptop. It is reference material, read and cited, never run.

Remotes: `origin` is `dlprentice/Onslaught` (branch `main`, the only branch), `upstream` is
`stuart73/Onslaught`. As of 2026-09-04 the fork is identical to `upstream/main`; every commit is Stuart's.

## How it is used

`~/Projects/game-dev/Onslaught-Career-Editor` vendors this fork as the submodule `references/Onslaught`, pinned
at `5352a81`. That repo treats it as its `SOURCE` evidence tier: its docs, C# rebuild and tests cite
`references/Onslaught/<file>:<line>` (see `DOCUMENTATION.md`, `rebuild/PARITY.md`, `rebuild/PROVENANCE.md`,
`patches/catalog/patches.v2.json`), `tools/aya_extractor_source_audit.py` refuses to run unless the submodule
is at its `ONSLAUGHT_PIN`, and `npm run test:safety` scans the submodule files. Its `CONTRIBUTING.md` says to
keep the pin unless a source-reference update is separately authorised.

## Rules

- Treat this as upstream code. No reformatting, renaming, translating or "fixing": line numbers are
  load-bearing citations in the editor repo.
- A change that is genuinely needed goes on this fork's `main` and is pushed to `origin`. Then, in
  Onslaught-Career-Editor, check out the new commit inside `references/Onslaught`, commit the pointer, update
  `ONSLAUGHT_PIN` in `tools/aya_extractor_source_audit.py`, and re-run that audit and `npm run test:safety`.
- Never rewrite history here: the submodule pin must always resolve. Take upstream changes with
  `git fetch upstream` and a merge of `upstream/main` into `main`, not a rebase.
- Keep `LICENSE` and provenance intact; nothing from this tree is copied into the MIT-licensed parts of the
  editor repo.
- Nothing here needs `local-data/`; the repo has no generated output.
