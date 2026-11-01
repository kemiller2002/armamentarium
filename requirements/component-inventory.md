# Component inventory and artifact verification worksheet

**Status: discovery required.** These are candidate components from the Echelon architecture, **not evidence that prebuilt binaries exist**. The release builder must inspect actual repos, release tags and downloadable assets before declaring support.

| Component | Intended role | Likely packaging | Artifact verified? |
|---|---|---|---|
| Conditor | Bootstrap / build orchestration | CLI or library, confirm | No |
| Praxis | Engineering work governance | CLI, confirm | No |
| Ordo | Decisions / constraints | CLI/library, confirm | No |
| Dokimos | Tests / verification | CLI/library, confirm | No |
| Aegis | Security controls | Confirm | No |
| Vigila | Monitoring | Confirm | No |
| Tutors | Guidance | Confirm | No |
| Vitium | Defect handling | Confirm | No |
| Fides | Identity | Client library/service contract | No |
| Strata | Schema migrations | CLI/library, confirm | No |
| Arca | Data access | F# library, confirm | No |
| Percepta / Percepta Semantic | Semantic evidence | Library/CLI, confirm | No |
| Limen | F# WASM runtime | WASM/.NET assets | No |
| Forma / Forma Studio | UI components/designer | UI assets/library/tool | No |
| Folio | Print/report output | Library/assets | No |
| Iter | Workflow | Confirm | No |

For each candidate record exact repository, latest stable tag, release asset URL, asset checksum, supported RID, package type, runtime dependencies, licensing, required/optional status, integration contract and actual execution verification. Never infer an executable from a repository name or NuGet package. Additional Echelon systems may be included after verified discovery.

## Preflight audit outputs
- `inventory.json`: installed/required/missing components with provenance.
- `compatibility.json`: dependency constraints and resolved versions.
- `doctor.json`: actual execution results, timestamps, exit codes and evidence references.
- `release-evidence.json`: per-target CI tests, signatures and SBOM status.

## Immediate decisions
1. Confirm initial platform: Linux x64 suggested, not yet validated.
2. Confirm whether Conditor already owns kit composition and bootstrap.
3. Inspect each component's actual build/release packaging and licenses.
4. Freeze initial profile requirements only after inventory.
