# Contributing to Gesso

Thanks for your interest in Gesso. The project is in early development and has a single maintainer. Until 1.0, the public API can change between any two releases.

## Before you start

- **Small fixes** — bugs, typos, documentation — can go straight to a pull request.
- **Anything larger** — a feature, a public API change, a refactoring, a new dependency — starts with an issue or a discussion. Wait for agreement before writing code: a pull request that does not fit the plan will be closed, however good it is.
- **Questions** go to [Discussions](https://github.com/gesso-dev/gesso/discussions), not issues.

## Licensing

- **Contributions** are accepted under the MIT License (see [LICENSE](LICENSE)), the same license the project is distributed under. By opening a pull request you confirm that you have the right to submit the change under this license. This is the usual inbound = outbound rule, also stated in section D.6 of the [GitHub Terms of Service](https://docs.github.com/en/site-policy/github-terms/github-terms-of-service#6-contributions-under-repository-license). You are responsible for everything you submit, however it was produced.
- **Code copied or ported from elsewhere** keeps its original copyright notice and license in the file itself, and that license must be allowed by the [dependency policy](DEPENDENCY_POLICY.md). Files without such a notice are covered by [LICENSE](LICENSE). Say where the code came from in the pull request.
- **Sample assets** follow the asset rules in the [dependency policy](DEPENDENCY_POLICY.md).
- **Never submit material under NDA** — console SDKs, their documentation, or code derived from them. Console backends are maintained outside this repository.

## Dependencies

Read [DEPENDENCY_POLICY.md](DEPENDENCY_POLICY.md) before adding a NuGet package, a native library, vendored code or a tool. A pull request that adds a dependency states its license and why it is needed.

## Engine rules

These rules hold everywhere in the engine. Review and, where possible, the build enforce them.

- **AOT first.** Trimming and AOT warnings (IL2xxx, IL3xxx) are errors, and every library is marked `IsAotCompatible`. No reflection at runtime: use source generators instead.
- **No allocations per frame.** Code on the frame path does not allocate once the game reaches a steady state.
- **SDL stays in the backend.** SDL types and concepts never appear in the public API; Gesso has its own key codes, events and formats.
- **Minimal public API.** Types are `internal` by default. A pull request that changes the public API updates the PublicApiAnalyzers baseline (`PublicAPI.Unshipped.txt`) and explains the change.

## Building and testing

You need the .NET 10 SDK and the [NativeAOT prerequisites](https://learn.microsoft.com/dotnet/core/deploying/native-aot/#prerequisites) for your operating system.

<!-- TODO: build, test and publish commands, once the M0 skeleton is in place. -->

CI runs on every pull request: a NativeAOT publish and smoke test on Windows, Linux and macOS, and reference-screenshot tests on WARP (Windows) and Lavapipe (Linux). Only pull requests with green CI are merged.

- If a change alters rendering on purpose, update the reference images in the same pull request and say why.
- macOS CI builds and publishes but does not render. If you change anything on the Metal path, describe how you tested it.

## Pull requests

- One logical change per pull request.
- Describe what changes and why, and link the issue.
- Changes in behavior come with tests.

## Security issues

Do not report vulnerabilities in public issues. Use **Report a vulnerability** on the repository's Security tab.