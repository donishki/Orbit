<div align="center">

# Orbit

**Your favorite websites, a little more organized.**

A Windows website launcher with collections, custom icons, and light and dark themes.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](LICENSE)
[![Windows](https://img.shields.io/badge/Windows-x64%20%7C%20x86-0078D4)](#quick-start)
[![Version](https://img.shields.io/badge/Version-1.1.4-466853)](https://github.com/donishki/Orbit/releases/latest)

[Download — GitHub](https://github.com/donishki/Orbit/releases/latest) · [Download — Gitea](https://git.ptbox.org/dasp/Orbit/releases/latest) · [Screenshots](#screenshots) · [Build from source](#development)

</div>

![Orbit in charcoal mode with website cards, collections, and search](docs/screenshots/orbit-dark.png)

Keep the websites you use every day in one place. Group them into collections, give them recognizable icons, and open a single website or a whole collection in your browser. Install Orbit or run it from a portable folder.

## What you can do

| | Features |
| --- | --- |
| **Collect** | Add website cards with automatic icons, or choose your own images. |
| **Organize** | Create collections and drag websites or collections into your preferred order. |
| **Find and open** | Search your library, launch a website, or open a collection together. |
| **Make it yours** | Switch between light and charcoal themes and customize website cards. |
| **Undo** | Restore a deleted shortcut during the current session. |
| **Take it with you** | Export and import libraries, including custom icons and collection order. |

## Screenshots

The screenshots show Orbit with public example websites.

### A calmer view of your websites

The charcoal theme keeps your website cards, search, and collections together in one window, as shown above.

### A lighter workspace

Switch to the light theme from the sidebar whenever you prefer.

![Orbit in light mode with website cards and the collection sidebar](docs/screenshots/orbit-light.png)

## Quick start

**You need:** Windows 10 or 11. The downloads include the .NET runtime; no separate installation is needed.

### 1. Choose your download

Get the latest release from **[GitHub](https://github.com/donishki/Orbit/releases/latest)** or **[Gitea](https://git.ptbox.org/dasp/Orbit/releases/latest)**.

| Download | Best for |
| --- | --- |
| **Orbit-Setup-win-x64.exe** | Installing on 64-bit Windows 10/11, with a Start menu shortcut and optional desktop shortcut. |
| **Orbit-Portable-win-x64.zip** | Running on 64-bit Windows without installing. |
| **Orbit-Setup-win-x86.exe** | Installing on 32-bit Windows 10. Also works on 64-bit Windows. |
| **Orbit-Portable-win-x86.zip** | Running the 32-bit version without installing. |

Most Windows 10/11 PCs should use **x64**. Orbit's executables are currently unsigned.

### 2. Open Orbit

- **Installer:** run the setup file, then open Orbit from the Start menu. Installation is for your Windows account and does not require an administrator password.
- **Portable:** extract the ZIP into a folder, then run `Orbit.exe`.

### 3. Make it yours

Choose **Add website** to save a link. Use **Collections** to group your websites, drag cards to reorder them, and use the search box to find what you need. Toggle **Dark mode** at the bottom of the sidebar to change the theme.

## Your library and settings

Links, custom icons, collection order, and preferences are stored locally in:

```text
%LOCALAPPDATA%\Orbit\settings.json
```

Use **Open settings** in the sidebar to open that folder. The previous save is retained as `settings.json.bak`, and older Orbit registry or sidecar settings migrate automatically.

Installed and portable copies use the same library for your Windows account. Copying only the executable to another PC does not transfer your saved websites.

Use **Import / Export** to transfer or share a library. Exports include website addresses, custom icons, and collection order; the theme stays local. Review your library before sharing it.

## Updates and uninstalling

Download the latest package from either release page. For an installed copy, run the new installer. For a portable copy, close Orbit and extract the new package into its folder.

The installer preserves your library during upgrades and uninstall. Remove the installed app through **Windows Settings → Apps**.

The x64 installer uses `%LOCALAPPDATA%\Programs\Orbit`. The x86 installer uses `%LOCALAPPDATA%\Programs\Orbit-x86` and creates **Orbit (32-bit)** shortcuts, so both versions can coexist.

## Development

Use **Windows and the .NET 8 SDK**.

### Get the source

```powershell
git clone https://github.com/donishki/Orbit.git
cd Orbit
```

You can also clone from [Gitea](https://git.ptbox.org/dasp/Orbit), or download the matching source ZIP from the release page.

### Build a portable version

```powershell
dotnet publish Orbit.csproj -c Release -r win-x64 --self-contained true -p:PublishSingleFile=true -p:IncludeNativeLibrariesForSelfExtract=true -p:DebugType=None -p:DebugSymbols=false -o release/portable-x64
Copy-Item README.txt, LICENSE release/portable-x64
```

Package the contents of `release/portable-x64` together. For a 32-bit build, replace `win-x64` with `win-x86` and use `release/portable-x86` as the output folder.

### Build the installers

Install **Inno Setup 7**, then run:

```powershell
./installer/Build-Installer.ps1
./installer/Build-Installer.ps1 -Architecture x86
```

Use `-IsccPath` if the compiler is installed elsewhere. The installers are written to `release/Orbit-Setup-win-x64.exe` and `release/Orbit-Setup-win-x86.exe`.

### Run the checks

```powershell
dotnet run --project tests/StorageChecks.csproj
dotnet run --project tests/FeatureChecks.csproj
dotnet run --project tests/ThemeChecks.csproj
```

Theme checks include live icon downloads; unavailable sites use fallback icons.

## Links

[GitHub](https://github.com/donishki/Orbit) · [Gitea](https://git.ptbox.org/dasp/Orbit) · [Report an issue](https://github.com/donishki/Orbit/issues) · [Detailed controls and release notes](README.txt)

## License

Copyright © 2026 Dario P.

Orbit is licensed under the **GNU General Public License v3.0** (`GPL-3.0-only`). See [LICENSE](LICENSE) for the full terms.
