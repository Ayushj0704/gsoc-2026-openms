# OpenMS Dependency Analysis — conda-forge Availability

**Date:** February 25, 2026  
**Task:** Check if all OpenMS dependencies can be migrated to pixi/conda-forge  
**Reference files:** `tools/ci/deps-ubuntu.sh`, `tools/ci/deps-macos.sh`

## Results

| Package | conda-forge Name | Status |
|---|---|---|
| cmake | cmake | ✅ Available |
| ninja | ninja | ✅ Available |
| eigen | eigen | ✅ Available |
| boost | boost | ✅ Available |
| xerces-c | xerces-c | ✅ Available |
| sqlite | sqlite | ✅ Available |
| libsvm | libsvm | ✅ Available |
| hdf5 | hdf5 | ✅ Available |
| zlib | zlib | ✅ Available |
| ccache | ccache | ✅ Available |
| doxygen | doxygen | ✅ Available |
| ghostscript | ghostscript | ✅ Available |
| graphviz | graphviz | ✅ Available |
| apache-arrow | apache-arrow | ✅ Available |
| coinor/cbc/clp | coin-or-clp | ⚠️ Different name |
| qtbase | qt6-main | ⚠️ Different name |

## CI Findings
- Ubuntu: ✅ Running perfectly
- Windows: ❌ `choco install ghostscript` crashed with exit code 139 — confirms pixi migration is needed
- macOS: 🔄 Results pending

## Next Steps
- Create `pixi.toml` with above dependencies
- Test Ubuntu first
- Then macOS and Windows
## Final Verified Mapping

| Original | conda-forge Name | Status |
|---|---|---|
| apache-arrow | libarrow | ✅ verified |
| coinor/cbc/clp | coin-or-clp | ✅ verified |
| qtbase | qt6-main | ✅ verified |
| all others | same name | ✅ verified |