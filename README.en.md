<div align="center">

# RedWine 🍷
**A modern, native Wine launcher for macOS built with SwiftUI**

[![License: GPL-3.0](https://img.shields.io/badge/license-GPL--3.0-blue.svg)](LICENSE)
[![Platform: macOS](https://img.shields.io/badge/platform-macOS%20(Apple%20Silicon)-lightgrey.svg)](#system-requirements-and-compatibility)
[![SwiftLint CI](https://github.com/IlyMooon/RedWine/actions/workflows/SwiftLint.yml/badge.svg)](https://github.com/IlyMooon/RedWine/actions/workflows/SwiftLint.yml)

**[🇬🇧 English](README.en.md)** | [🇫🇷 Français](README.md)

</div>

---

## 1. Overview

**RedWine** is a native macOS application designed to create and manage isolated Windows environments (Wine "bottles") and run Windows executables and games (`.exe`, `.msi`, `.bat`) directly on macOS—without the overhead of a full virtual machine or a complete Windows installation.

Built with SwiftUI and designed to blend seamlessly into macOS, RedWine prioritizes usability, streamlined bottle management, and direct integration with modern Apple graphics technologies.

---

## 2. Features

All features listed below are backed by code in this repository:

- **Bottle Management**:
  - Create, configure, reset, and delete independent Wine bottles.
  - Choose the target Windows version (Windows 7, Windows 10, Windows 11).
  - Quick shortcuts to drive `C:`, user folders, and the Wine configuration panel (`winecfg`).
- **File Execution & Handling**:
  - Full support for Windows executables (`.exe`), Windows installers (`.msi`), and batch scripts (`.bat`).
  - Open via Finder double-click, drag-and-drop onto the window, or through the manual file picker.
- **3D Graphics Acceleration**:
  - Direct3D 9/10/11 translation to Vulkan via **DXVK**, translated to Metal via **MoltenVK**.
  - Integration with Apple's **D3DMetal** (Game Porting Toolkit).
  - Multithreaded **msync** synchronization toggle for reduced CPU bottlenecks.
  - Built-in toggle for Apple's Metal Performance HUD to display real-time graphics metrics in games.
- **Integrated Winetricks**:
  - Graphical manager to install essential Windows components (Visual C++ runtimes, .NET Framework, Microsoft Core Fonts).
- **Live Debug Log Console**:
  - Instant access via `Cmd + L` to inspect Wine `stdout` and `stderr` execution streams in real time.
- **Finder Thumbnail Extension**:
  - Integrated `WhiskyThumbnail` QuickLook extension that parses PE headers to display actual Windows executable icons directly in the Finder.
- **Command Line Interface (CLI)**:
  - Bundled `WhiskyCmd` CLI utility for scripting and headless bottle management from the Terminal.

---

## 3. System Requirements and Compatibility

The requirements below are verified in the Xcode project configuration:

| Component | Requirement |
| :--- | :--- |
| **Operating System** | **macOS 14.0 (Sonoma)** or later (`MACOSX_DEPLOYMENT_TARGET = 14.0`). |
| **Processor Architecture** | **Apple Silicon only (M1, M2, M3, M4)** (`ARCHS = arm64`). Intel Macs (x86_64) are not supported by this build target. |
| **Rosetta 2** | Required to enable x86_64 and 32-bit execution via WoW64. |
| **Storage** | 2 GB to 5 GB of free disk space recommended, depending on the number of bottles and installed runtimes. |

---

## 4. Installation

### Prebuilt Releases
If precompiled releases are published, visit the [RedWine Releases](https://github.com/IlyMooon/RedWine/releases) page, download the disk image (`.dmg`) or archive, and drag `RedWine.app` into your `/Applications` folder.

> [!NOTE]
> Do not use the Homebrew command from the original upstream project (`brew install --cask whisky`), as it will install the archived original application rather than RedWine.

### Building from Source
If no prebuilt release is currently available, or if you prefer running from the latest code, follow the instructions in [Building from Source](#6-building-from-source).

---

## 5. Getting Started

1. **First Launch**: Open the application. If the Wine runtime is not yet initialized, the setup assistant will guide you through setting up the necessary runtime libraries.
2. **Creating a Bottle**:
   - Click `+` or "Create Bottle".
   - Name your bottle (e.g. *Gaming*, *Utilities*) and choose the emulated Windows version (e.g. *Windows 10*).
3. **Running an Application**:
   - Click "Run..." and select an installer (`setup.exe`) or executable.
   - Installed programs will automatically pin to the bottle view for quick access.
4. **Configuring Graphics Options**:
   - Open bottle configuration to toggle DXVK, msync, or the Metal Performance HUD according to your application's needs.
5. **Debugging & Troubleshooting**:
   - If an application encounters an error, press `Cmd + L` to open the log console and inspect live Wine execution output.

---

## 6. Building from Source

### Required Tools
- An Apple Silicon Mac running macOS 14.0 Sonoma or higher.
- **Xcode 15** or later (from the Mac App Store or Apple Developer portal).
- Xcode Command Line Tools:
  ```bash
  xcode-select --install
  ```
- **SwiftLint** (required by the Xcode project build phase):
  ```bash
  brew install swiftlint
  ```

### Build Instructions

1. **Clone the repository**:
   ```bash
   git clone https://github.com/IlyMooon/RedWine.git
   cd RedWine
   ```

2. **Package Dependency Resolution**:
   Swift Package Manager dependencies (`Sparkle`, `swift-argument-parser`, `SwiftyTextTable`, `Progress.swift`, `SemanticVersion`) are resolved automatically when building via Xcode or the command line.

3. **Build via Command Line**:
   ```bash
   # Build Release version
   xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Release

   # Or build for Debug without code signing:
   xcodebuild build -project Whisky.xcodeproj -scheme Whisky -configuration Debug CODE_SIGNING_ALLOWED=NO
   ```

4. **Run SwiftLint Checks**:
   ```bash
   swiftlint --strict
   ```

---

## 7. Repository Structure

```text
├── Whisky/                 Main macOS application (SwiftUI views, ViewModels, AppDelegate, assets)
├── WhiskyKit/              Internal core framework (Wine lifecycle, bottle management, PE parsing, configuration)
├── WhiskyCmd/              Command-line interface (CLI) tool
├── WhiskyThumbnail/        QuickLook / Thumbnail extension for Finder
├── Libraries/              Bundled third-party binaries (cabextract)
├── images/                 Local repository assets
├── .github/                Issue templates, PR template, and CI workflows
├── LICENSE                 Full GNU General Public License v3.0 text
├── CONTRIBUTING.md         Contribution guidelines, branch & commit conventions
├── CODE_OF_CONDUCT.md      Community Code of Conduct
├── SECURITY.md             Responsible security disclosure policy
└── CHANGELOG.md            Release history following Keep a Changelog
```

> [!NOTE]
> *Why do internal targets and folders still use the name "Whisky"?*
> These names originate from the parent project. To preserve codebase integrity, avoid breaking build references, and maintain compatibility across Xcode project schemes, internal identifiers have intentionally been kept unchanged.

---

## 8. Limitations and Compatibility

Because RedWine is a compatibility translation layer, not all Windows software is supported:

- **Kernel-level Anti-Cheat**: Games requiring Windows kernel drivers (such as Riot Vanguard, BattlEye, Easy Anti-Cheat, Ricochet) cannot run under Wine.
- **Aggressive DRM**: Certain digital rights management schemes actively refuse to execute in virtualized or translated environments.
- **16-bit DOS / Windows 3.1 Software**: Unsupported by the 64-bit WoW64 translation subsystem.
- **DirectX 12**: Compatibility varies depending on Metal hardware features and the state of D3DMetal / VKD3D translation.
- **Upstream Data Servers**: The original runtime download servers from the parent project are offline. Automatic runtime downloading requires an active replacement hosting server or manual runtime setup.

---

## 9. Security

> [!WARNING]
> **Wine is not a security sandbox.**
> Windows processes executed through RedWine inherit the full system and file permissions of your macOS user account. Never run executables from unknown, unverified, or suspicious sources.

For responsible vulnerability reporting, please review our [Security Policy](SECURITY.md).

---

## 10. Contributing and Community

We welcome contributions, bug reports, and suggestions:

- Review our [Contributing Guide](CONTRIBUTING.md) before submitting code.
- To report bugs, use the [Bug Report](https://github.com/IlyMooon/RedWine/issues/new?template=bug.yml) template.
- To suggest ideas, open a [Feature Request](https://github.com/IlyMooon/RedWine/issues/new?template=feature-request.yml).
- Community interactions are governed by our [Code of Conduct](CODE_OF_CONDUCT.md).

---

## 11. Credits & Acknowledgments

RedWine builds upon the work of several open source projects:

- [msync](https://github.com/marzent/wine-msync) by marzent
- [DXVK-macOS](https://github.com/Gcenx/DXVK-macOS) by Gcenx and doitsujin
- [MoltenVK](https://github.com/KhronosGroup/MoltenVK) by KhronosGroup
- [Sparkle](https://github.com/sparkle-project/Sparkle) by the Sparkle project
- [swift-argument-parser](https://github.com/apple/swift-argument-parser) by Apple
- [SwiftyTextTable](https://github.com/scottrhoyt/SwiftyTextTable) by scottrhoyt
- [Progress.swift](https://github.com/jkandzi/Progress.swift) by jkandzi
- [SemanticVersion](https://github.com/SwiftPackageIndex/SemanticVersion) by SwiftPackageIndex
- [CrossOver](https://www.codeweavers.com/crossover) and [WineHQ](https://www.winehq.org/) by CodeWeavers and the Wine community
- D3DMetal by Apple

We extend our sincere thanks to **CodeWeavers** for their long-standing dedication to the Wine ecosystem.

---

## 12. Project Origin

**RedWine** is an independent fork of [Whisky-App/Whisky](https://github.com/Whisky-App/Whisky), originally created by Isaac Marovitz and community contributors.

- **Upstream Project Status**: The original repository was archived and is no longer actively maintained by its author.
- **Purpose of RedWine**: This fork was created to maintain and carry the project forward by refreshing its documentation, cleaning obsolete upstream dependencies, and supporting community development.
- **Independence**: RedWine is an autonomous initiative and is neither affiliated with, sponsored by, nor endorsed by the authors of Whisky.

---

## 13. License

RedWine is released under the **GNU General Public License v3.0 (GPL-3.0)**.  
See the [LICENSE](LICENSE) file for the full license terms.
