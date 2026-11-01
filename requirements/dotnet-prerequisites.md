# ARM-019: External .NET SDK and runtime prerequisites

Status: APPROVED architectural direction, implementation NOT VERIFIED.

Armamentarium SHALL NOT bundle .NET SDKs, shared .NET runtimes, ASP.NET Core runtimes, or .NET workload installers. These are external prerequisites acquired from official Microsoft distribution channels.

## Requirements

1. The kit manifest MUST specify required .NET SDK feature bands, runtime major/minor versions, and workload identifiers by capability profile and platform.
2. Conditor MUST detect installed SDKs and runtimes with `dotnet --list-sdks`, `dotnet --list-runtimes`, and `dotnet --info`. It MUST check SDK requirements separately from runtime requirements. F# compilation requires an SDK, not just a runtime.
3. When prerequisites are missing, Conditor MAY install the minimum required versions using official Microsoft distribution channels, but only when installation is authorized by the execution environment. No silent privilege escalation or untrusted download-and-execute.
4. All installers MUST be obtained over authenticated channels and verified according to the official Microsoft distribution's published integrity/provenance mechanism. Pin requested versions or feature bands and record installed versions in preflight evidence.
5. Preflight MUST fail closed if a required SDK, runtime, or workload is missing or incompatible, including when automatic installation is disabled, unsupported, or unsuccessful.
6. Self-contained .NET executables MAY be consumed when upstream already publishes them, but Armamentarium SHALL NOT independently package a shared .NET runtime as a kit component.
7. The kit release archive MUST remain independent of .NET SDK/runtime installer payloads. Any external download costs and time MUST be included in bootstrap performance measurements.
8. Profiles MUST support multiple SDK versions when required, rather than assuming a single SDK can build all components. Avoid installing redundant versions.

## Verification
- Clean Linux x64 runner with required SDK installed: preflight passes.
- Runner with runtime only: F# build profile fails or installs SDK when authorized.
- Runner with wrong SDK feature band: preflight rejects or repairs.
- Offline runner with missing SDK: clear BLOCKED status, not PASS.
- Installer source or verification failure: fail closed.
- Audit evidence records exact versions and acquisition provenance.

This requirement supersedes any recommendation to include the .NET SDK/runtime in the Armamentarium archive.
