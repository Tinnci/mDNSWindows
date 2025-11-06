# mDNSWindows

mDNSWindows is a fork of Apple's mDNSResponder code to improve and maintain
Windows support. See [APPLE_README.txt](./APPLE_README.txt) for the original
README that accompanied this project.

Most of the files in this repository are verbatim as they appeared in the
tarball version 878.70.2 obtained from Apple's
[download page](https://opensource.apple.com/tarballs/mDNSResponder/). Files
and projects not relevant to mDNS/DNS-SD support on Windows have been removed.
Legacy build projects have been removed and replaced with a CMake system. Any
source files modified by ETC contain comments at the top of the file describing
the modification.

## Repository Structure

This repository is organized as follows:

- **Upstream Repository:** [ETCLabs/mDNSWindows](https://github.com/ETCLabs/mDNSWindows)  
  Official ETC Labs project repository for Windows mDNS support.

- **Development Fork:** [Tinnci/mDNSWindows](https://github.com/Tinnci/mDNSWindows)  
  Fork used for feature development and testing. Changes are developed and tested here before being contributed back upstream.

### Git Remote Configuration

```bash
# Upstream (official repository - no direct push)
git remote -v | grep upstream
# upstream  https://github.com/ETCLabs/mDNSWindows.git (fetch)
# upstream  DISABLED (push)

# Origin (development fork)
git remote -v | grep origin
# origin  https://github.com/Tinnci/mDNSWindows.git (fetch)
# origin  https://github.com/Tinnci/mDNSWindows.git (push)
```

## Building

### Prerequisites
- Windows (tested on Windows Server 2025)
- Visual Studio 2022 or later
- CMake 3.4+

### Build Instructions

```bash
mkdir build
cd build
cmake -G "Visual Studio 17 2022" -A x64 ..
cmake --build . --config Release
```

Supported architectures: `Win32` (x86) and `x64`

## Continuous Integration

This project uses GitHub Actions to automatically build and test on every push to `main` and pull requests.

**Workflow:** `.github/workflows/windows-build.yml`
- Builds for both Win32 (x86) and x64 architectures
- Tests both Debug and Release configurations
- Artifacts are retained for 7 days

## About this ETCLabs Project

mDNSWindows is official, open-source software developed by ETC employees and is
designed to interact with ETC products. For challenges using, integrating,
compiling, or modifying this software, we encourage posting on the
[issues page](https://github.com/ETCLabs/mDNSWindows/issues) of this project.
