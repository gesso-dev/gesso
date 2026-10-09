# Security policy

## Supported versions

Gesso is in early development. Until 1.0, only the latest release receives security fixes: a fix lands in `main` and ships in the next release, and older releases are not patched. Reports against `main` are welcome.

| Version            | Supported |
| ------------------ | --------- |
| Latest 0.x release | Yes       |
| Older releases     | No        |

Support for older versions will be defined with the 1.0 release.

## Reporting a vulnerability

Do not report vulnerabilities in public issues, discussions or pull requests. Use **Report a vulnerability** on the repository's [Security tab](https://github.com/gesso-dev/gesso/security) instead. The report becomes a private security advisory that only you and the maintainer can see.

Include as much of this as you can:

- the affected version or commit;
- the operating system and runtime identifier (for example, `win-x64`), and whether the app ran on JIT or NativeAOT;
- what the vulnerability is and what an attacker could do with it;
- steps to reproduce or a proof of concept;
- a suggested fix, if you have one.

## What happens next

Gesso has a single maintainer, so response times are best effort.

1. You get a reply within 14 days. If you do not, comment on the advisory.
2. The maintainer confirms the issue and agrees on its severity with you in the advisory.
3. The fix is prepared in the advisory’s temporary private fork and released.
4. The advisory is published after the release, with a CVE where warranted. You are credited unless you ask not to be.

Please keep the details private until the advisory is published. If the fix takes long, the maintainer will agree on a disclosure date with you in the advisory.

## Scope

Report privately anything in this repository or its published packages that lets untrusted input cross a security boundary, for example:

- memory corruption or code execution when loading files such as asset packs, images, models, fonts or audio;
- reading or writing files outside the intended locations through the virtual file system or user data storage;
- a compromise of the build, CI or release pipeline, or of the published NuGet packages.

These are not security vulnerabilities:

- a malformed file that causes an exception or a crash, without memory corruption or code execution — open a regular issue;
- cheating, modding or other tampering with a game on the player's own machine — Gesso does not protect a game from its own player;
- problems in a game built with Gesso — contact its developers;
- problems in console backends — they are maintained outside this repository, so report them where you obtained the backend.

### Dependencies

Report vulnerabilities in SDL3, the .NET runtime and other dependencies to their own projects. Report them here as well if a Gesso package ships an affected version, or if the way Gesso uses the dependency makes the issue exploitable. SDL3 is linked statically, so its fixes reach users only through a Gesso release.