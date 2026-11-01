# Armamentarium v1: normative build-kit requirements

Status: DRAFT requirements, no executable release or verified binaries yet. Repository: kemiller2002/armamentarium.

## Objective
Distribute a reproducible, versioned, verified Echelon engineering toolchain through a single agent bootstrap, with a mandatory fail-closed preflight before application work. Minimize setup time, tool discovery and token consumption without embedding every system's documentation in the agent context.

## Required behavior and acceptance

**ARM-001 Release identity.** Every kit has immutable release ID, semver, build commit, timestamp, platform target, manifest schema version and complete SHA-256 inventory. Reject missing, mutable or inconsistent metadata.

**ARM-002 Component classification.** Distinguish executable CLI, F# NuGet library, WASM runtime/assets, UI/design assets, schema/template, external service client, and documentation. Never claim every Echelon repository produces a standalone binary. Every required component has source repository, immutable commit, version, artifact reference, artifact digest, license, install path, capabilities and dependency constraints.

**ARM-003 Compatibility lock.** Release producer resolves one tested set of component versions. Consumers never select floating latest or silently substitute versions. Explicit incompatible/missing components fail preflight. Allow app-specific capability profiles resolved from the lock.

**ARM-004 Distribution.** Publish signed platform-specific archives and a small bootstrap manifest via immutable GitHub Releases or equivalent trusted hosting. Download once, verify cryptographic provenance and checksums **before extraction**, extract safely to isolated versioned path. No untrusted archive paths, symlinks escaping root or unsafe executable permissions.

**ARM-005 Offline readiness.** After archive acquisition, local install, manifest inspection, hash verification and executable health checks work without GitHub network access. External services may require network during actual development; report those as separate readiness gates.

**ARM-006 Mandatory preflight.** `armamentarium doctor --json --strict --profile <name>` (proposed CLI) validates integrity, platform/architecture, .NET SDK/runtime, F# tooling, executable invocations, package assets, dependency lock, required capabilities, provider configuration presence, and tool-specific health. Exit nonzero for any mandatory failure. Machine-readable results include PASS/FAIL/BLOCKED/SKIPPED with evidence; SKIPPED never counts as PASS.

**ARM-007 Agent gating.** Agent must run preflight before generating application code. Required tools, including Conditor and Praxis when profile mandates them, cannot be skipped or replaced by textual assurances. No autonomous fallback to ad hoc installation unless policy explicitly authorizes a new kit build.

**ARM-008 Provenance.** CI records source commits, build toolchain, hashes, signatures, SBOM, build logs and verification evidence. An archive is not labeled verified merely because it exists. A release requires clean build and actual execution tests on every advertised target.

**ARM-009 Security.** No secrets, tokens, credentials, financial data, personal data or environment-specific private configuration in archives, logs or source. Runtime credentials come from external secure channels. Pin third-party dependencies and check license/security advisories.

**ARM-010 Reproducibility.** Same lock and build environment yield equivalent functional artifacts; document any nondeterministic bytes. Every published archive can be traced to a tagged source commit and a CI run. Preserve release artifacts and immutable hashes for rollback.

**ARM-011 Incremental profiles.** Define full, web-app, data-app and minimal profiles. Full kit can carry all verified compatible artifacts, but agents load only profile-relevant tools and instructions. Profiles list required/optional components and explicitly identify unsupported targets.

**ARM-012 Performance experiment.** Compare fresh-agent bootstrap using kit versus conventional per-repo installation: wall time, download bytes, commands, token usage, failure/skip rates, reproducibility and completed application milestones. Do not claim savings before controlled measurement.

**ARM-013 Update policy.** New component releases do not mutate old kits. CI builds new candidate lock, validates compatibility and publishes a new version only after gates pass. No 'newest of everything' at runtime.

**ARM-014 Supply-chain safety.** Use signed release metadata and trusted keys or attestations. Fail on signature mismatch, missing digest, expired/revoked trust, or archive contents not in manifest. Avoid unauthenticated curl-to-shell bootstrap.

**ARM-015 Operational clarity.** `inventory` and `doctor` show exactly what is installed, what is not, and what was actually executed. Separate tool presence, tool health, service reachability and application readiness.

**ARM-016 Cross-platform targets.** Start with Linux x64 as an explicitly proposed initial CI target; add Linux arm64/macOS/Windows only when build+runtime verification is available. Do not label unsupported targets as available.

**ARM-017 F# first.** Build orchestration and CLI should use F#/.NET where practical. Prefer existing Conditor capabilities rather than duplicating them. No Kubernetes or Terraform dependency.

**ARM-018 Unit tests and failure tests.** Tests required for manifest parsing, signatures, digest mismatch, malicious archive paths, missing required component, incompatible versions, wrong platform, bad role/profile, unavailable external service, and incomplete verification. No green status on skipped mandatory tests.

## Boundaries
This repo is the release assembly and compatibility contract, not a replacement for component source repos. Source systems retain their own CI and releases. Runtime deployments (e.g. identity/database services) are not automatically bundled as running services. No requirement to expose internal tools to end-user apps.

## Delivery gates
1. Inventory verified from actual repositories/releases, including availability of prebuilt artifacts.
2. Component/profile lock and signed manifest schema reviewed.
3. Bootstrap and preflight implemented and tested.
4. One complete platform kit assembled from actual artifacts.
5. CI verifies every required component and publishes release evidence.
6. Controlled rehearsal measures agent setup effectiveness.

All gates are currently NOT VERIFIED.
