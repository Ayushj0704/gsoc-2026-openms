# Week 1 Progress

## What I Did
- Raised PR #8778 — macOS Homebrew LLVM fix
- Understood maintainer feedback from jpfeuffer
- Closed PR gracefully with workaround note on issue #8776
- Joined OpenMS Discord, introduced myself
- Connected with mentor timosachsenberg
- Analyzed all CI workflow files
- Checked all dependencies on conda-forge
- Enabled and ran CI on my fork successfully
- Found Windows CI crash bug with ghostscript

## Key Learnings
- OpenMS uses 3 different package managers across platforms
- pixi/conda-forge can unify all of them
- Windows CI is already broken with choco — migration is urgent
## Day 2 — Feb 26, 2026

### Completed
- Created pixi.toml with all OpenMS dependencies
- Discovered apache-arrow correct name is `libarrow` on conda-forge
- Got `pixi install` working successfully for linux-64, osx-arm64, win-64
- Modified CI yaml — replaced apt-get with pixi for Ubuntu
- Fixed cmake_prefix to include lib/cmake subdirectory
- Created pixi-migration branch on fork
- Pushed changes and triggered openms-ci-full

### Key Findings
- apache-arrow → libarrow on conda-forge
- qt6-main resolves fine
- coin-or-clp works as coinor replacement
- ghostscript crashed on Windows choco (exit code 139) — confirms pixi need

### CI Status
- cppcheck ✅ passing
- openms-ci-full 🔄 in progress on pixi-migration branch