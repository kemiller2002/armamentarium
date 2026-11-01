# Armamentarium packaging and bootstrap architecture

## Pipeline
Component repositories -> immutable release artifacts -> Conditor-assisted kit assembly -> compatibility lock -> archive + SBOM + signed manifest -> CI verification -> GitHub Release -> agent bootstrap -> strict preflight -> application development.

## Proposed release structure
```text
armamentarium-vX.Y.Z-linux-x64.tar.zst
  manifest.json
  manifest.sig
  lock.json
  sbom.spdx.json
  bin/                  # verified executable tools
  lib/                  # pinned .NET/F# packages and dependencies
  wasm/                 # compatible runtime/assets
  ui/                   # Forma assets and templates
  schemas/              # versioned contracts
  templates/            # optional app profiles
  docs/                 # concise operator instructions, not whole repo dumps
  evidence/             # verification summary
```

The archive signature verification needs a trusted *external* digest/signature statement, since a signature inside an unverified archive cannot itself establish archive integrity. Fetch and validate signed release metadata first, then verify archive SHA-256, then safely extract, then validate each file.

## Manifest schema (requirements sketch)
```json
{
  "schemaVersion": 1,
  "kitVersion": "0.1.0",
  "target": "linux-x64",
  "sourceCommit": "<immutable SHA>",
  "components": [
    {
      "name": "praxis",
      "sourceRepository": "kemiller2002/praxis",
      "sourceCommit": "<immutable SHA>",
      "version": "<verified release version>",
      "kind": "cli",
      "artifactPath": "bin/praxis",
      "sha256": "<64 hex>",
      "capabilities": ["work-governance"],
      "requires": []
    }
  ]
}
```
Values shown in angle brackets are placeholders, not known artifacts.

## Profiles
- `minimal`: bootstrap verifier and mandatory governance tools.
- `web-app`: minimal plus Limen, Forma, Folio and relevant UI/build dependencies.
- `data-app`: minimal plus Strata, Arca, Fides client integration and data tooling.
- `full`: all *verified compatible* supported components, not every repository indiscriminately.

Profile definitions must be generated from the verified inventory and dependency graph, not guessed. External service clients are not equivalent to deployed services.

## Agent bootstrap contract
1. Select target and requested profile from project requirements.
2. Retrieve immutable signed metadata; verify with pinned trust root.
3. Download exact artifact and verify digest.
4. Extract safely into versioned immutable directory.
5. Run `inventory` and strict `doctor`; persist machine-readable evidence.
6. Stop on mandatory failures, do not silently install substitutes.
7. Load only task-relevant concise usage contracts and start development.

## Reproducibility experiment
Run same app specification, same model budget and comparable environment with (A) per-component installation and (B) kit bootstrap. Measure wall clock, tokens, network bytes, setup failures, omitted tools and delivered verified milestones. Report tradeoffs including kit build cost and stale-kit risk.
