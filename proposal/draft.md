# GSoC 2026 Proposal — OpenMS

## Personal Info
- **Name:** Ayush Kumar Jha
- **GitHub:** github.com/Ayushj0704
- **Email:** 
- **Discord:** Ayush Jha

## Project
**Unify development dependencies using pixi/conda-forge**  
**Mentor:** timosachsenberg, Peter Jones  
**Duration:** 175 hours

## About Me
Myself Ayush , A CS Sophomore Student @ NSUT'28 , New Delhi, India. My Tech Stack includes Python , Cpp, Java, React Native , CI/CD Pipeline.My Hobbies include reading non- frictional books and playing chess , tennis(nowadays Volleyball).
## Why This Project
I faced a real build failure on macOS (PR #8778) which made me 
realize that OpenMS's fragmented dependency system across 
choco/brew/apt is the root cause of many such issues. 
This project fixes that permanently.

## What I'll Deliver
- pixi.toml working on Ubuntu
- pixi.toml working on macOS  
- pixi.toml working on Windows
- Updated CI workflow using pixi instead of choco/brew/apt
- Documentation

## Timeline
| Week | Task |
|---|---|
| 1-2 | Ubuntu pixi.toml working |
| 3-4 | macOS pixi.toml working |
| 5-6 | Windows pixi.toml working |
| 7 | CI workflow updated |
| 8 | Testing + Documentation |

## Contributions So Far
- PR #8778 — macOS Homebrew LLVM fix
- CI running on fork
- Full dependency analysis on conda-forge
- Found Windows CI crash bug (ghostscript exit code 139)
## Contributions So Far
- PR #8778 — macOS Homebrew LLVM fix
- Full conda-forge dependency analysis
- CI running on fork
- Found Windows CI crash (ghostscript exit code 139)
- Created working pixi.toml for all 3 platforms
- Modified CI yaml to use pixi for Ubuntu
- Active communication with mentor timosachsenberg