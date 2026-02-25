# PR #8778 — macOS Homebrew LLVM Fix

**Date:** February 21, 2026  
**Issue Fixed:** #8776 — Undefined symbol `std::__1::__hash_memory` 
when building OpenMS on macOS arm64 with Homebrew LLVM

## What I Did
- Added macOS/Clang block in `CMakeLists.txt`
- Derived Homebrew LLVM root from `CMAKE_CXX_COMPILER`
- Injected `-L` flag for `libc++` directory
- Build completed successfully on macOS arm64 with Homebrew LLVM 21.1.8

## Maintainer Feedback (jpfeuffer)
- Approach was unstable — manually touching link flags is risky
- Could break setups where someone intentionally mixes 
  Homebrew LLVM with system libs
- This is an upstream bug, not OpenMS's problem to fix

## What I Learned
- Always think about OTHER people's setups, not just your own
- Upstream bugs should be fixed upstream, not patched downstream
- Closing gracefully is better than arguing
- Left workaround note on #8776 for others hitting same issue

## Connection To Current Work
This exact problem (dependency conflicts on macOS) is what 
pixi migration will solve permanently — one package manager, 
no conflicts.
```

---

This is important because **your proposal story is:**
```
Faced build problem → tried to fix it → 
learned why it's deeper → now fixing the ROOT CAUSE