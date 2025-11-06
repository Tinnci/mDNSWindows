# mDNSWindows (Tinnci Fork)

This is **Tinnci's development fork** of the [ETCLabs/mDNSWindows](https://github.com/ETCLabs/mDNSWindows) project. 

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

### Upstream vs. Fork

- **Upstream (Official):** [ETCLabs/mDNSWindows](https://github.com/ETCLabs/mDNSWindows)  
  The official ETC Labs project repository for Windows mDNS support.

- **This Fork:** [Tinnci/mDNSWindows](https://github.com/Tinnci/mDNSWindows)  
  **Development fork for feature development and experimentation.** Not affiliated with ETCLabs.
  Changes are developed and tested here independently.

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

## Feature Enhancements (This Fork)

This fork includes the following enhancements beyond the official ETCLabs/mDNSWindows:

### 1. Shared Multicast Socket Support (SO_REUSEADDR)
- **Purpose:** Enable mDNSResponder to coexist on UDP/5353 with other Windows services (Dnscache, Chrome, etc.)
- **Implementation:** 
  - Modified `SetupSocket()` to bind multicast sockets to `INADDR_ANY` instead of specific interface addresses
  - Enhanced `CanReceiveUnicast()` to use `SO_REUSEADDR` socket option
  - Maintains per-interface multicast group memberships for proper mDNS semantics
- **Files Modified:** `mDNSWindows/mDNSWin32.c`

### 2. MSVC Compiler Enhancements
- Added `/utf-8` flag for UTF-8 source encoding support
- Suppressed CRT deprecation warnings (`_CRT_SECURE_NO_WARNINGS`)
- Improved Windows compatibility flags

### 3. GitHub Actions CI/CD
- Automated builds for Win32 (x86) and x64 architectures
- Both Debug and Release configurations
- Runs on every push to `main` and pull requests
- Build artifacts retained for 7 days

## Continuous Integration

This project uses GitHub Actions to automatically build and test on every push to `main` and pull requests.

**Workflow:** `.github/workflows/windows-build.yml`
- Builds for both Win32 (x86) and x64 architectures
- Tests both Debug and Release configurations
- Artifacts are retained for 7 days

## About this Fork

This is an **independent development fork** of ETCLabs/mDNSWindows, not officially affiliated with ETC Labs. 
It is used for experimental feature development and testing Windows mDNS/DNS-SD improvements.

### Relationship to ETCLabs

- This fork is based on the official [ETCLabs/mDNSWindows](https://github.com/ETCLabs/mDNSWindows) project
- This fork maintains its own development branch and CI/CD pipeline
- Features and fixes developed here may be contributed back to the upstream project
- This fork operates independently and is not supported by ETC Labs

## About the Official ETCLabs Project

mDNSWindows is official, open-source software developed by ETC employees and is
designed to interact with ETC products. For challenges using, integrating,
compiling, or modifying the official upstream project, please visit the
[ETCLabs issues page](https://github.com/ETCLabs/mDNSWindows/issues).
