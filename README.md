# GSoC 2026 — OpenMS Contribution Journal

**Applicant:** Ayush Kumar Jha  
**GitHub:** github.com/Ayushj0704  
**Organization:** OpenMS  
**Project:** Unify development dependencies using pixi/conda-forge

## What This Repo Is
This repo tracks all my research, contributions and proposal 
drafts for Google Summer of Code 2026 with OpenMS.

## Project Goal
OpenMS currently uses 3 different package managers:
- Windows → choco
- macOS → brew  
- Linux → apt

Goal is to replace all of them with a single pixi/conda-forge 
setup that works on all platforms.

## Contributions
| Date | Contribution |
|---|---|
| Feb 21 | PR #8778 — macOS Homebrew LLVM fix |
| Feb 26 | Full conda-forge dependency analysis |
| Feb 26 | CI successfully running on fork |
| Feb 26 | Found Windows CI crash bug (ghostscript) |
| Feb 28 | PR #8823 — full pixi migration for all 5 CI platforms |
| Mar 1  | Fixed macOS cmake segfault — pinned cmake <4.0 |
| Mar 1  | Addressed 11-point mentor review on PR #8823 |
| Mar 2  | Diagnosed Windows BLAS failure — VCPKG_TOOLCHAIN guard incompatible with pixi |
| Mar 2  | Added OPENMS_LINK_COIN_BLAS cmake option to FindCOIN.cmake per mentor direction |

## Links
- OpenMS GitHub: github.com/OpenMS/OpenMS
- My Fork: github.com/Ayushj0704/OpenMS
- GSoC 2026 Ideas: openms.de/news/gsoc2026
- CI Actions: github.com/Ayushj0704/OpenMS/actions
* Pixi Migration PR: github.com/OpenMS/OpenMS/pull/8823
