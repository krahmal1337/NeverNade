# NeverNade release repo

This repository contains no source code.


This repository only exists to provide GitHub-hosted release artifacts, release hashes, and build logs.

## Download

Download the latest release from the [Releases](../../releases/latest) page.

Download all three binaries and place them in the same folder:

| File | Purpose |
|------|---------|
| `neverlose.dll` | Main module with server, x86 |

## About reproducibility

The release workflow is configured to make builds as verifiable as possible:

- releases are built from a public source commit
- the exact source commit is listed for every release
- GitHub Actions logs show the build steps that produced the files
- the workflow uses reproducibility-oriented flags where practical

However, this project does **not** currently guarantee byte-for-byte identical local rebuilds on every machine.

Windows C++ builds can be sensitive to the exact GitHub Actions image, MSVC toolset, Windows SDK, linker behavior, build paths, and project settings. Because of that, a local build may produce working binaries with different hashes from the official release.

The official release artifacts should be treated as the binaries produced by the linked GitHub Actions run from the listed public source commit.

## Building from source

To build the project yourself, clone the source repository:

```powershell
git clone https://git.femboy.tw/root/FemboyLose.git
cd FemboyLose
```

Then follow the build instructions in the source repository README.

Local builds are useful for auditing, modifying, or running your own copy of the project. They are not currently guaranteed to hash-match the official GitHub Actions release artifacts.

## Source

All source code lives here:

https://git.femboy.tw/root/FemboyLose
