# Echelon artifact availability audit, 2026-11-01

**Scope:** Read live default-branch README files from 16 component repositories and root package manifests where present. This is a **source and distribution-contract audit**, NOT a GitHub Releases asset enumeration or downloaded binary checksum audit. No artifact was downloaded or executed. Statements about published releases remain unverified unless explicitly described as repository claims.

## Findings

| System | Repository evidence inspected | Distribution classification | Confidence and gap |
|---|---|---|---|
| Conditor | README describes executable CLI, deterministic install plan, pinned registry, component verification and lock.json | Existing bootstrap CLI; likely integration owner | Source confirms documented capability, not release asset or executable validation |
| Praxis | README describes repository OS, native tooling, compatibility npm identity `@echelon-foundry/repository-operating-system` | CLI/tooling | Exact published artifact, RID, digest unverified |
| Ordo | README documents native GitHub Release installer and `ordo init/status/verify`, npm compatibility | Native CLI distribution documented | Need enumerate actual release assets and hashes; installer is curl-pipe-shell and must not be reused unverified |
| Dokimos | README documents F#/.NET implementation and code-quality system | .NET tool/library, packaging unresolved | No release asset proof |
| Aegis | README explicitly documents `EchelonFoundry.Aegis.Core`, Store.GitHub, Integration.GitHub NuGet packages | F# NuGet libraries | Package claims verified from README, exact NuGet versions/assets not verified |
| Vigila | README calls it task organizer/pilot; ROS installed snapshot; PolyForm Noncommercial license | Application/repository, not presumed kit binary | No independent CLI artifact verified; license review required |
| Vitium | README describes defect reporting application, proposed baseline and undeployed machine intake | Application/service, not standalone CLI | Integration likely service contract; no release asset verified |
| Fides | README describes Exchange service and F# client; explicitly says nothing deployed | Client library + deployable service contract | Do not bundle as a running service; release artifacts unverified |
| Strata | README documents PostgreSQL schema tool, GitHub Releases heading, PostgreSQL 16 pilot; root global.json pins SDK 8.0.0 | CLI/tool | Need verify release assets and supported target; SDK 8 differs from proposed .NET 10 standard |
| Arca | README explicitly lists Core, GitHub and Limen NuGet packages; describes attested GitHub release assets/local feed | F# NuGet libraries | Need inspect release assets and attestations; no binaries validated |
| Percepta | README documents UI system and bootstrap via npm/NuGet dependencies | Repository/application | Not proven distributable standalone artifact |
| Limen | README documents `@echelon-foundry/limen`; root package.json version 0.9.1, exports browser kernel and lifecycle CLI | npm package / browser assets / CLI | Source manifest verified, registry publication and exact tarball not checked; PolyForm Noncommercial license in manifest |
| Forma | README documents `@echelon-foundry/design-system`; root package.json version 0.13.0 and CSS/runtime exports | npm CSS/UI asset package | Source manifest verified, registry tarball unverified |
| Forma Studio | README documents app and pinned UI dependencies | Application/tool | Do not presume distributable binary |
| Folio | README and package.json `@echelon-foundry/print-components` version 0.4.2, JS/CSS exports | npm print components and CSS | Source manifest verified, registry tarball unverified |
| Iter | README documents optional .NET library for typed routing | F# library | Package publication/version not verified |

**Naming:** All 16 live repositories inspected are under `kemiller2002/`, including Armamentarium itself. `echelon-foundry` is the product identity, not a verified GitHub organization namespace in this audit.

## Audit conclusions

1. **Packaging needs three main lanes:** native executables (Conditor/Praxis/Ordo/Strata/Dokimos if confirmed), immutable NuGet package artifacts (Aegis/Arca/Iter/Fides client as available), and npm/browser/CSS/WASM assets (Limen/Forma/Folio). Applications/services are represented by client contracts or optional templates, not bundled running processes.
2. **Conditor should remain bootstrap/installation authority**. Armamentarium assembles, locks, signs and distributes a compatible snapshot, not a competing installer. Verify Conditor's real capabilities before integration.
3. **Do not rebuild everything by default.** Prefer attested upstream assets, repackage only when license and provenance allow; if none exists, file a component-specific packaging requirement.
4. **Potential licensing blocker:** Limen's package manifest and Vigila's README declare PolyForm Noncommercial. Commercial redistribution/use requires a deliberate license review and cannot be assumed MIT. Audit every dependency and bundled artifact before public release.
5. **Potential SDK compatibility blocker:** Strata root `global.json` specifies .NET SDK 8.0.0 with latestFeature roll-forward, whereas other Echelon applications target newer SDKs. Resolve toolchain coexistence with isolated SDKs or verified self-contained binaries; do not assume a single SDK works.
6. **Source versions are not released versions.** The observed Limen 0.9.1, Forma 0.13.0 and Folio 0.4.2 values come from default-branch package.json files, not authenticated package registry releases.
7. **Security:** Existing shell installers must be downloaded and authenticated before execution. A signed manifest and archive hash check precede extraction; an internal manifest alone does not establish trust.

## Priority follow-up verification (not yet performed)

- Enumerate actual GitHub Release tags and assets per component, plus npm/NuGet registry versions; record immutable URLs, SHA-256 and signatures/attestations.
- Inspect CI release workflows and platform target matrices, verify Linux x64 first.
- Verify the exact artifact type and startup command per component by downloading into an isolated test environment and executing a non-mutating version/health command.
- Resolve all license obligations, including commercial-use rights, for redistributed components.
- Produce a compatibility lock only from confirmed artifacts; report missing/blocked components rather than substituting guesses.
- Compare Conditor's existing install/verification contract with Armamentarium's proposed preflight, to avoid duplicated orchestration.

## Current evidence classification

- **Observed:** README/package.json/global.json contents read through connected GitHub.
- **Documented claims:** Native releases, NuGet publishing and installers described by READMEs.
- **Not observed:** GitHub Release asset lists, registry download metadata, signatures, hashes, executable health checks, CI green status, complete dependency graph.

No component should be marked `artifact_verified=true` based on this audit alone.
