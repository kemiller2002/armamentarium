# Armamentarium

**Echelon Foundry's versioned, verifiable engineering build kit.**

Armamentarium will assemble compatible Echelon tools, libraries, WASM assets, schemas and templates into a signed, platform-specific distribution. Agents will verify and extract one kit, run a mandatory strict preflight, and only then begin application development.

**Current status: requirements and architecture drafted. No build-kit release or binary verification has been completed.**

- [Normative requirements](requirements/MASTER.md)
- [Component inventory worksheet](requirements/component-inventory.md)
- [Packaging architecture](docs/architecture.md)

Key design constraints: F# first, immutable version locks, no skipped required systems, cryptographic verification before extraction, no secrets in artifacts, explicit supported platforms, measured rather than assumed speed/token savings.

Next milestone: audit actual Echelon repositories and published assets, then finalize the compatibility lock and release manifest. Do not represent candidate components as already packaged.
