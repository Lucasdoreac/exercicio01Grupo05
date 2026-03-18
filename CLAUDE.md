# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**PDMApp** is a .NET MAUI desktop application targeting Windows 10+ (net10.0-windows10.0.19041.0). Early-stage project with a full design system in place but minimal business logic.

## Build & Run Commands

```bash
# Build (debug)
dotnet build PDMApp.sln

# Build (release)
dotnet build PDMApp.sln -c Release

# Run
dotnet run --project PDMApp/PDMApp.csproj

# Publish Windows
dotnet publish PDMApp/PDMApp.csproj -c Release -f net10.0-windows10.0.19041.0
```

Open `PDMApp.sln` in **Visual Studio 2022** (v18.5+) for full MAUI tooling. No test project exists yet.

## Architecture

**Bootstrap flow:**
```
MauiProgram.cs → MauiAppBuilder → App.xaml → MainPage.xaml
```

- **MauiProgram.cs** — Single entry point. Registers fonts (OpenSans Regular/Semibold), sets up debug logging, builds `MauiApp`.
- **App.xaml** — Merges global resource dictionaries: `Colors.xaml` and `Styles.xaml`. No code logic.
- **MainPage.xaml/.cs** — Current landing page (demo welcome screen). The starting point for real feature development.

## Design System

Located in `PDMApp/Resources/Styles/`:

- **Colors.xaml** — 46 color tokens + 16 `SolidColorBrush` resources. Primary: `#512BD4` (purple). Supports `AppThemeBinding` for light/dark mode.
- **Styles.xaml** — 28 styles covering all standard MAUI controls. All interactive elements enforce `MinimumHeightRequest=44` for accessibility.

Always use named color/style resources instead of hardcoded values in XAML.

## Platform Notes

- **Windows-only target** in current `.csproj`. MAUI supports Android/iOS/macOS structurally but they are not configured.
- Windows-specific code lives in `PDMApp/Platforms/Windows/` (App.xaml, Package.appxmanifest).
- Dependencies managed via **NuGet** (`.csproj`), not npm/bun.
