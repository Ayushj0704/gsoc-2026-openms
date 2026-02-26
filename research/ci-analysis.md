# CI File Analysis

## File: openms_ci_matrix_full.yml

### What It Does
This is the main CI file that builds and tests OpenMS 
automatically on GitHub's servers whenever code is pushed.
It runs on 5 platform/compiler combinations:
- windows-2025 + cl.exe (MSVC)
- macos-14 + xcode 15.4
- ubuntu-24.04 + g++ 13
- ubuntu-24.04-arm + g++ 13
- ubuntu-24.04 + clang++ 17

### Current Dependency Setup (Before Migration)
| Platform | Tool | Script |
|---|---|---|
| Ubuntu | apt-get | tools/ci/deps-ubuntu.sh |
| macOS | brew | tools/ci/deps-macos.sh |
| Windows | choco | inline in CI yaml |

### Problems Found
- Windows: `choco install ghostscript` crashes with 
  exit code 139 (segfault) — build broken!
- 3 different tools = 3 different failure modes
- Hard to maintain and debug

### After Migration (Our Changes)
- Ubuntu now uses pixi instead of apt-get
- cmake_prefix points to pixi environment
- pixi bins added to GITHUB_PATH
- macOS and Windows migration pending

## File: tools/ci/deps-ubuntu.sh
- Installs ~20 packages via apt-get
- Also installs Apache Arrow separately via wget
- Installs uv (Python package manager)
- All packages now mapped to conda-forge equivalents

## File: tools/ci/deps-macos.sh  
- Installs ~15 packages via brew
- Has optional flags: --skip-doc-deps, --skip-gui-deps
- All packages available on conda-forge
- Migration pending