# Dependency admission policy

## Why

Release builds use NativeAOT: the engine and every dependency are linked into one binary that a game ships. Any copyleft component would impose its terms on every game built with Gesso. Gesso's tools — cooker, shader compilers, MSBuild tasks, source generators — run in users' builds and reach users through NuGet packages, so the same rule applies to them.

## Scope

Covered:

- runtime libraries, managed and native;
- tools shipped to users: cooker, shader compilers, MSBuild tasks, source generators and analyzers;
- all transitive dependencies of the above, including third-party code bundled inside a dependency;
- code copied, vendored or ported into the repository. A port to C# is a derivative work: it keeps the original copyright notice and license;
- sample assets (see "Sample assets").

Not covered:

- **Operating system components** that belong to the target platform, are not shipped with the game and are loaded dynamically — for example glibc, or the system libraries SDL3 loads at runtime on Linux for audio, windowing and input. Many of them are LGPL; this is acceptable because Gesso neither distributes nor statically links them.
- **Development-only dependencies**: test frameworks, benchmarks, CI tooling, platform vendor tools (for example WARP, a Windows component that is not open source). They are never redistributed and are not needed to build, publish or run a game. Any OSI-approved license, or vendor tooling free to use for this purpose, is acceptable. A development-only dependency that becomes needed by users goes through the full policy.
- **Platform backends maintained outside this repository** (consoles under NDA). They must not add obligations to the packages published from this repository.

## Allowed licenses

The allowlist is closed: a license that is not on it is rejected until this policy is changed by a pull request that explains why.

`MIT`, `MIT-0`, `0BSD`, `BSD-2-Clause`, `BSD-3-Clause`, `Apache-2.0`, `Zlib`, `ISC`, `BSL-1.0`, `NCSA`

### License expressions

- `A OR B` — accepted if at least one branch is allowed; the registry records the branch Gesso uses.
- `A AND B` — every part must be allowed.
- `A WITH exception`:
    - accepted if `A` is allowed, for example `Apache-2.0 WITH LLVM-exception`;
    - if `A` is copyleft, accepted only when the exception removes the copyleft for the way Gesso uses the component, for example `GPL-3.0-or-later WITH Bison-exception-2.2` on a generated parser. Requires review; the reasoning is recorded in the registry.

### Not allowed

- Copyleft of any strength — GPL, LGPL, AGPL, MPL, EPL, CDDL, EUPL, MS-RL and similar — except through an exception as above.
- Licenses that restrict the field of use, the type of user or revenue: non-commercial, "free for open source", revenue thresholds, source-available. Rejected even when Gesso itself qualifies, because the terms would bind the games and studios that use Gesso.
- Code without a license or with an unclear license: it is all rights reserved. This includes snippets from Q&A sites and forums, which are typically CC-BY-SA.
- CC0-1.0 for code: it explicitly withholds patent rights. CC0-1.0 is accepted for assets only.

## Proposing a dependency

Open an issue, or describe the dependency in the pull request that adds it:

1. **What and why.** Name, version or pinned tag, purpose, and the alternatives considered — including writing or porting the code within Gesso.
2. **License.** SPDX expression of the component, of each transitive dependency and of third-party code bundled inside it; for `OR`, the branch Gesso uses.
3. **Use.** Runtime, tools, or development only; which RIDs or host operating systems.
4. **Maintenance.** Latest release, activity, number of maintainers, how security issues are handled. A small, finished library that is no longer maintained can be vendored if Gesso takes over its maintenance.
5. **AOT compatibility** (runtime dependencies only; tools running inside MSBuild or the compiler run on JIT). Managed: builds without IL2xxx/IL3xxx warnings in Gesso's configuration; no reflection or runtime code generation. Native: builds from a pinned source tag in CI for every required RID and links statically.
6. **Size impact.** Change in the size of the NativeAOT-published reference sample, per RID.
7. **Frame cost** (runtime only). No allocations per frame in steady state.

The maintainer accepts or rejects the proposal. An accepted dependency is added to the registry in the same pull request that adds the dependency.

## Registry of accepted dependencies

Every dependency, transitive ones included, is recorded in the table at the end of this file:

- name and exact version, or tag/commit for native code built from source;
- SPDX expression, and the chosen branch for `OR`;
- copyright notices as they appear in the license;
- source URL;
- scope: runtime, tools, or development;
- link to the proposal.

The .NET runtime and base class libraries are recorded like any other dependency. Development-only dependencies are recorded too. The registry is the input for third-party notices generation in M7, when it may move to a machine-readable file.

Starting with M7, CI checks the restored dependency graph against the registry: a package missing from the registry, or whose license expression differs from the recorded one, fails the build.

## Updates

A version update — including one proposed by Dependabot — whose license expression differs from the recorded one is handled as a new proposal. Projects do relicense between major versions, sometimes to commercial terms.

## Sample assets

Sample assets — textures, models, fonts, audio — are either:

- licensed under CC0-1.0, or
- original work contributed to the repository and dedicated by its authors to CC0-1.0.

Licenses that require attribution or share-alike — CC-BY, CC-BY-SA, OFL-1.1 — are not accepted, so that users can copy anything from the samples into their games with no obligations. Every asset directory lists the source and license of its files.

## Accepted dependencies

| Name | Version | License | Copyright | Scope | Source | Proposal |
|---|---|---|---|---|---|---|
| .NET runtime and base class libraries | 10.0 | `MIT` | Copyright (c) .NET Foundation and Contributors | runtime | https://github.com/dotnet/runtime | #2 |