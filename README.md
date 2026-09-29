# Powenetics — update channel

Public distribution point for the **Powenetics V2** and **Powenetics V3** desktop apps.

This repository deliberately contains **no source code**. It holds only:

- `components.json` — the update manifest the apps poll over HTTPS
- release assets (app installers, vetted RTSS runtime packages) attached to Releases

The application source lives in private repositories; only the distributables are public so the
in-app updater can reach them anonymously.

## How the apps use this

| Component | Source | Verification |
|---|---|---|
| **PresentMon** | Intel's official [`GameTechDev/PresentMon`](https://github.com/GameTechDev/PresentMon) releases | Authenticode — must be signed by *Intel Corporation* |
| **RTSS** | `rtss` entry below (Guru3D publishes no update feed) | SHA-256 from the manifest **and** Authenticode — must be signed by *MICRO-STAR INTERNATIONAL* |
| **Powenetics app** | `apps` entry below | SHA-256 from the manifest |

Updates are **never** installed silently: the app only checks, then reports. Downloading and
installing happens after an explicit click, and each component must pass the verification
listed in the table above.

The [Powenetics V3 31.50.1 release](https://github.com/crmaris/powenetics-updates/releases/tag/v3-31.50.1)
includes an installer and portable ZIP. Both contain the self-contained Windows x64 app
and command-line updater.

## Manifest

`components.json` is served raw over HTTPS:

```
https://raw.githubusercontent.com/crmaris/powenetics-updates/main/components.json
```

Bumping a version = upload the asset to a Release here, then update the matching entry
(`version`, `url`, `sha256`). Helper scripts live in the app repositories under `updates/`.
