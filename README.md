# Android preinstall cleanup

## Overview and purpose

This directory is a placeholder for tools that audit, disable, or uninstall Android preinstalled apps. When the repo was prepared there was no executable source, device inventory, or operation log, so it currently ships documentation and ignore rules only. It does not claim automation that does not exist yet.

A later implementation should be based on Android Debug Bridge (ADB), prefer rollback-friendly “disable/uninstall for the current user” flows, and avoid deleting files from the system partition.

## Current features

- Document project boundaries and safety constraints.
- Ignore device exports, package lists, logs, APKs, installers, build outputs, and local config.
- Reserve a rebuildable layout with no real device data for future ADB scripts.

There is no runnable removal script, allowlist/denylist, or auto-restore implementation. That matches the current tree.

## Tech stack and dependencies

No source dependencies yet. If an ADB implementation is added, expect:

- Android Platform Tools (`adb`).
- Windows PowerShell or a cross-platform shell.
- An Android device with USB debugging enabled.
- USB drivers matching the device.

Do not put device serials, accounts, installed-package dumps, vendor diagnostic packages, or real APKs in the repo.

## How to run / use

This version has no executable entry. To prepare a later environment, verify ADB first:

```powershell
adb version
adb devices
```

Before implementing any uninstall command:

1. Export the device package list into a local ignored directory.
2. Separate critical system components, vendor components, and ordinary preloads.
3. Validate on a test user or spare device.
4. Prefer recoverable operations and record the matching restore commands.
5. Keep real device output local; do not paste it into source or docs.

## File structure

```text
.
├── .gitignore  # Device data, APKs, build and run artifacts
└── README.md   # Current status, boundaries, safe-use notes
```

## Safety

Wrongly disabling system components can cause boot loops, launcher/settings crashes, and broken network or account features. If package rules are added later, use generic examples and explicit confirmation — never bind a full package list from a real device.
