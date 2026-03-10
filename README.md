# GSoC 2026 — OpenMS Contribution Journal

**Applicant:** Ayush Jha
**GitHub:** [github.com/Ayushj0704](https://github.com/Ayushj0704)
**Organization:** [OpenMS](https://github.com/OpenMS/OpenMS)
**Application Period:** March 16 – March 31, 2026

---

## Projects Being Pursued

### Project 1 — Unify Development Dependencies (pixi/conda-forge)
**Mentor:** jpfeuffer
**Difficulty:** Medium | **Duration:** 175 hours

Replace platform-specific package managers (apt-get, brew, choco, conda) with a single
`pixi.toml` that works consistently across linux-64, linux-aarch64, osx-arm64, and win-64.

**PR:** [OpenMS#8823](https://github.com/OpenMS/OpenMS/pull/8823) — Draft, 43 commits
**Status:** Closed by mentor pending a working solution on at least one platform.
Mentor's exact words: *"Feel free to reopen when you have something that is 100% working on at least one platform."*

**Current focus:** Linux-only fix. The configure failure was `Qt6Gui` not found due to missing
OpenGL dev packages (`libgl-devel`, `libegl-devel`) on the headless CI runner. Fix applied,
pending CI verification.

**Key technical findings from this work:**
- conda-forge `libsvm` uses integer version numbers (321, 337), not semantic versioning — upper bound `<4.0` excludes all available versions
- `cmake >=4.0` segfaults on osx-arm64 GitHub Actions runners — pinned to `<4.0`
- `coin-or-cbc` on Windows ships as a static `.lib` with unresolved Fortran symbols (`DGETRF`/`DGETRS`) in MSVC uppercase convention — only `mkl_rt.lib` exports them correctly
- `OPENMS_LINK_COIN_BLAS` cmake option is the correct hook for pixi/Windows BLAS detection — must not be removed
- `LD_LIBRARY_PATH` / `DYLD_LIBRARY_PATH` env var hacks are not acceptable — RPATH set at cmake configure time is the correct approach
- coinmp removal must be scoped to pixi-only files, not documentation or scripts covering other build paths

---

### Project 2 — Accelerating OpenSwathWorkflow for Large-Scale In Silico Spectral Libraries
**Mentor:** Joshua Charkow
**Difficulty:** Medium | **Duration:** 200 hours

OpenSwathWorkflow is OpenMS's core DIA analysis pipeline. Large in silico spectral libraries
(millions of precursors) expose memory and runtime bottlenecks in candidate selection and scoring.
This project profiles the pipeline, identifies algorithmic bottlenecks, and implements optimizations
validated against the original results.

**Status:** Environment set up (reusing OpenMS build from Project 1). Profiling in progress.
**Dataset:** [PASS00779 — Mtb SWATH](https://db.systemsbiology.net/sbeams/cgi/PeptideAtlas/PASS_View?identifier=PASS00779) (477k transitions, 32 SWATH windows)
**Additional angle:** Ion mobility data profiling (MobiDIK) as suggested by mentor.

---

## Repository Structure

```
progress/     — weekly progress logs, profiling results, CI run notes
proposal/     — draft proposals for both projects
research/     — technical notes, mentor conversation summaries, findings
```

---

## Progress Log

### Week of March 9, 2026
**Project 1 (pixi):**
- CI run revealed actual configure error: `Qt6Gui` fails because `WrapOpenGL` not found on headless runner
- Root cause: missing `libgl-devel` and `libegl-devel` in Linux platform sections of `pixi.toml`
- Fix: added both packages to `linux-64` and `linux-aarch64` sections
- Also fixed: `libsvm` pin had wrong upper bound `<4.0` — removed it since conda-forge uses integer versioning (current: 337)
- PR closed by mentor — will reopen once Linux CI passes

**Project 2 (OpenSwath):**
- Selected project based on algorithmic optimization fit with C++ problem-solving background
- Messaged mentor Josh on Discord
- Setting up profiling environment with tutorial dataset

---

## Honest Assessment

The pixi migration PR was closed due to accumulated complexity across 43 commits — changes
touching coinmp documentation, workflow hacks, and FindCOIN.cmake in ways the mentor didn't
agree to. The lesson: make smaller, focused, mentor-approved changes. Don't touch files outside
the agreed scope.

The Linux OpenGL fix is narrow, safe, and directly addresses the actual error without any
workflow hacks or FindCOIN.cmake changes. That is the right kind of fix.

---

## Contact

- Discord: ayushjha_14102
- Email: [jhakrayush2007@gmail.com]
