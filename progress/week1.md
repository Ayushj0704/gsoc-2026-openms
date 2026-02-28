# Week 1 Progress (Feb 21 - Feb 28, 2026)

## Day 1 — Feb 21, 2026

### What I Did
- Discovered issue #8776 — macOS arm64 build failing with 
  Homebrew LLVM due to missing `std::__1::__hash_memory`
- Investigated the root cause — libc++ mismatch between 
  Homebrew LLVM and system libraries
- Fixed it by adding macOS/Clang block in CMakeLists.txt 
  that injects `-L` flag for Homebrew's libc++
- Opened PR #8778 with fix and tested on macOS arm64

### Feedback Received
- jpfeuffer (core maintainer) reviewed and said approach 
  was unstable — manually touching link flags could break 
  other setups
- Understood his point — someone might intentionally mix 
  Homebrew LLVM with system libs
- Closed PR gracefully and left workaround note on #8776 
  for others hitting same issue

### Key Learning
- Always think about other people's setups not just your own
- Upstream bugs should be fixed upstream, not patched downstream
- Closing gracefully > arguing with maintainer

---

## Day 2 — Feb 25, 2026

### What I Did
- Joined OpenMS Discord, introduced myself in #gsoc-students
- Read GSoC 2026 ideas page on openms.de
- Identified best project fit: "Unify development dependencies 
  using pixi/conda-forge"
- Connected with mentor timosachsenberg
- He personally suggested a task — explore replacing 
  choco/brew/apt with pixi/conda-forge

### Key Learning
- OpenMS uses 3 different package managers across platforms
- This fragmentation is the ROOT CAUSE of issues like PR #8778
- pixi can unify all platforms with one tool

---

## Day 3 — Feb 26, 2026

### What I Did
- Read and analyzed CI files:
  - `.github/workflows/openms_ci_matrix_full.yml`
  - `tools/ci/deps-ubuntu.sh`
  - `tools/ci/deps-macos.sh`
- Checked ALL dependencies on conda-forge (prefix.dev)
- Created `pixi.toml` with all OpenMS dependencies
- Got `pixi install` working for linux-64, osx-arm64, win-64
- Enabled GitHub Actions on fork
- Triggered CI — cppcheck passed ✅
- Modified CI yaml — replaced apt-get with pixi for Ubuntu
- Created `pixi-migration` branch
- Triggered openms-ci-full on pixi-migration branch

### Key Findings
- apache-arrow → `libarrow` on conda-forge
- coinor → `coin-or-clp` on conda-forge  
- qtbase → `qt6-main` on conda-forge
- Windows CI already broken — ghostscript crashed 
  with exit code 139 on choco (confirms pixi need!)
- cmake_prefix must include lib/cmake subdirectory

### CI Status
- cppcheck ✅ passing
- openms-ci-full 🔄 running on pixi-migration branch# Week 1 Progress

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
### Debugging Session — CI Failures

#### Root Cause Found
cmake_prefix paths were correct but COIN-OR packages 
were incomplete. pixi.toml had only coin-or-clp but 
OpenMS CMake requires:
- coin-or-cbc (CBC solver)
- coin-or-cgl (Cut Generation Library)  
- coin-or-clp (LP solver)
- coin-or-osi (Open Solver Interface)

coin-or-coinutils not needed explicitly — pulled in 
automatically as dependency of coin-or-cbc.

#### How We Found It
CDash build logs showed exact CMake error:
"Could NOT find COIN (missing: COIN_CBC_LIBRARY COIN_CGL_LIBRARY)"
ninja: build.ninja error was a consequence, not root cause.
## Week 1 - Day 4-5 Progress

### CI Pipeline Status
| Platform | Status | Notes |
|----------|--------|-------|
| Ubuntu clang++17 | ✅ PASSING | 2466 tests |
| Ubuntu g++13 | ✅ PASSING | Fixed LD_LIBRARY_PATH |
| Ubuntu ARM64 | ✅ PASSING | |
| macOS-14 | 🔄 Debugging | cmake segfault on osx-arm64 |
| Windows-2025 | 🔄 Debugging | LAPACK linking for CoinOR |

### Technical Fixes Applied
- Migrated all 5 platforms to pixi-based dependency management
- Fixed runtime library path issues (LD_LIBRARY_PATH/DYLD_LIBRARY_PATH)
- Fixed KNIME CTD generation step for all platforms
- Made Apple certificate import conditional on secret availability
- Scoped LAPACK/BLAS to win-64 only
- Investigating cmake 4.2.x segfault on osx-arm64 runner
