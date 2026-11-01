# Release metadata audit results — 2026-11-01

Source: user-provided `release-metadata-audit.zip` containing `releases.csv`, produced by Armamentarium GitHub Actions. Observations are **GitHub latest-release API metadata**, not downloaded, hashed or executed assets.

## Totals
- 16 repositories queried
- 11 with latest release found
- 5 with no latest release confirmed (this status also includes API/access errors)
- 84 release assets reported across the 11 found releases
- 0 asset contents or Linux x64 compatibility verified

| Repository | Latest tag | Asset count | Status |
|---|---|---:|---|
| conditor | v0.10.18 | 10 | FOUND |
| praxis | v3.24.0 | 14 | FOUND |
| ordo | v1.19.0 | 10 | FOUND |
| dokimos | dokimos-v0.9.0 | 11 | FOUND |
| aegis | — | — | UNKNOWN_OR_NO_LATEST_RELEASE |
| vigila | — | — | UNKNOWN_OR_NO_LATEST_RELEASE |
| vitium | — | — | UNKNOWN_OR_NO_LATEST_RELEASE |
| fides | v0.2.0 | 7 | FOUND |
| strata | v0.1.1 | 6 | FOUND |
| arca | v0.7.0 | 5 | FOUND |
| percepta | percepta-semantic-v0.3.0 | 6 | FOUND |
| limen | v0.9.1 | 5 | FOUND |
| forma | v0.13.0 | 7 | FOUND |
| forma-studio | — | — | UNKNOWN_OR_NO_LATEST_RELEASE |
| folio | v0.4.1 | 3 | FOUND |
| iter | — | — | UNKNOWN_OR_NO_LATEST_RELEASE |

## Important limits
- The audit only checks `releases/latest`; this can fail for repositories with only prereleases, tags without releases, missing permissions or transient API errors.
- It does not identify asset names, architecture, package type, digest, signature, license or download URL.
- GitHub Releases are not the only distribution mechanism. NuGet/npm may have valid packages even for repositories without a latest GitHub release.
- This is not yet a compatibility lock. Do not equate these tags with a tested compatible version set.

## Next verification
1. Enumerate asset names, download URLs, sizes, digest metadata and attestations for the 11 releases.
2. Query npm/NuGet metadata for browser/F# libraries, including five unknown GitHub-release statuses.
3. Check redistribution and commercial licensing.
4. Select exact Linux x64 CLI assets and platform-independent packages, download and SHA-256 verify in CI.
5. Exercise actual commands and Conditor integration; publish a signed kit only after strict gates pass.

**Current build readiness: BLOCKED (asset identity, integrity, licensing and runtime checks not complete).**
