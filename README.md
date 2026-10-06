# Odin Tools — official release feed

This repository holds no source code. It exists so that the Odin Tools desktop
application can find, download, and verify its own updates, and so that a new
customer has an installer to download.

## What each asset is

| Asset | Purpose |
| --- | --- |
| `latest.json` | The update manifest the running application reads at startup. |
| `Odin-Update-<version>.odinupd` | The update payload: the files under `resources/`, packed and hashed. |
| `Odin Tools-Setup-<version>.exe` | The installer, for a first-time installation only. |

## How an update is delivered

1. On every start the application reads
   `https://github.com/oden1999/Odin-Tools/releases/latest/download/latest.json`.
   This check is silent and does not delay startup.
2. If the published version is newer than the installed one, a window offers the
   update. The window does not block the application; it can be dismissed.
3. Accepting downloads the payload, verifies its SHA-256 against the manifest,
   writes the files over the installation's `resources/`, and restarts the
   application.

The original installer is never run again. An update only replaces the files it
was shipped with, and every path inside the payload is relative to the
installation root.