# FemboyLose

Releases are built automatically from source hosted at [git.femboy.tw](https://git.femboy.tw/root/FemboyLose).

This repository contains no source code — only the CI workflow and release artifacts.

## Download

Grab the latest release from the [Releases](../../releases/latest) page. Extract the zip and place all three files in the same folder.

| File | Description |
|------|-------------|
| `neverlose.dll` | Main module — x86 |
| `injector.exe` | DLL injector — x86, requires administrator |
| `neverlose-server.exe` | Local server — x64 |

## Verifying the build

Every release is built by GitHub Actions directly from the source repository. No binaries are uploaded manually.

**Steps:**

1. Open the Actions run linked in the release notes
2. In the build log, find the `Clone source` step — confirm the commit SHA matches a commit on [git.femboy.tw/root/FemboyLose](https://git.femboy.tw/root/FemboyLose)
3. Download `SHA256SUMS.txt` from the release and compare against the files in the zip:
   ```
   # PowerShell
   Get-FileHash neverlose.dll, injector.exe, neverlose-server.exe -Algorithm SHA256
   ```

**To build it yourself:**

Requirements:
- [Visual Studio 2022 Build Tools](https://aka.ms/vs/17/release/vs_BuildTools.exe) with the v144 MSVC toolset and Windows 10 SDK
- [Rust 1.87.0](https://static.rust-lang.org/rustup/dist/x86_64-pc-windows-msvc/rustup-init.exe) (x64)
- Python 3 + `pip install msvcpp-normalize-pe`

```powershell
git clone https://git.femboy.tw/root/FemboyLose.git
cd FemboyLose

# Build C++ (x86 Release)
msbuild neverlose.sln /p:Configuration=Release /p:Platform=Win32 /p:PlatformToolset=v144 /p:AdditionalOptions="/Brepro" /p:AdditionalLinkerOptions="/BREPRO"

# Normalize PE headers
msvcpp-normalize-pe Win32\Release\neverlose.dll
msvcpp-normalize-pe Win32\Release\injector.exe

# Build server (x64)
cd server\rust-server
cargo build --release --locked

# Compare hashes against SHA256SUMS.txt from the release
Get-FileHash ..\..\..\Win32\Release\neverlose.dll, ..\..\..\Win32\Release\injector.exe, target\release\neverlose-server.exe -Algorithm SHA256
```

If your hashes match `SHA256SUMS.txt`, the release binary is identical to what you built from source.

## Source

All source code lives at [git.femboy.tw/root/FemboyLose](https://git.femboy.tw/root/FemboyLose).
