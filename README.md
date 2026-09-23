<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f0c29,50:302b63,100:24243e&height=200&section=header&text=Pure%20Status%20HD%20Updater%20Panel&fontSize=40&fontColor=ffffff&fontAlignY=38&desc=APK%20Update%20Manifest%20%E2%80%94%20Live%20OTA%20Control&descAlignY=58&descSize=16&animation=fadeIn" width="100%"/>

<br/>

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&pause=1000&color=A78BFA&center=true&vCenter=true&width=600&lines=Live+OTA+Update+Manifest;Force+Update+Support;Version+Control+%26+Changelog;Lightweight+JSON+Powered)](https://git.io/typing-svg)

<br/>

![Version](https://img.shields.io/badge/Version-0.3.9-blueviolet?style=for-the-badge&logo=android&logoColor=white)
![Version Code](https://img.shields.io/badge/Version_Code-39-7c3aed?style=for-the-badge&logo=github&logoColor=white)
![Force Update](https://img.shields.io/badge/Force_Update-Disabled-ef4444?style=for-the-badge&logo=shield&logoColor=white)
![Size](https://img.shields.io/badge/APK_Size-See_release_asset-10b981?style=for-the-badge&logo=files&logoColor=white)

</div>

---

<div align="center">

## ⚡ What is this?

</div>

This repository acts as the **live update manifest** for the **Pure Status HD** Android app.
When the app launches, it fetches `pure-status.json` from this repo to check for updates — no backend server required.

```
App Launch → fetch pure-status.json → compare version_code → prompt / force update
```

---

<div align="center">

## 📦 Current Release

</div>

<div align="center">

| Field | Value |
|-------|-------|
| 🏷️ Version Name | `0.3.9` |
| 🔢 Version Code | `39` |
| 📱 APK Size | `See release asset` |
| 🚨 Force Update | `false` |
| 🔗 Download | [pure-status-hd.apk](https://github.com/Matrix1999/Pure_status_updater/releases/latest/download/pure-status-hd.apk) |

</div>

---

<div align="center">

## 🗂️ Manifest Structure

</div>

```json
{
  "version_code": 39,
  "version_name": "0.3.9",
  "apk_url": "https://github.com/Matrix1999/Pure_status_updater/releases/latest/download/pure-status-hd.apk",
  "changelog": "Pure Status HD updater flow and the latest media-processing improvements.",
  "update_size": "See release asset",
  "force_update": false
}
```

| Key | Type | Description |
|-----|------|-------------|
| `version_code` | `int` | Integer incremented on every release — app compares this to installed build |
| `version_name` | `string` | Human-readable version shown in the update dialog |
| `apk_url` | `string` | Direct download link to the APK in GitHub Releases |
| `changelog` | `string` | Release notes shown before updating (`\n` for line breaks) |
| `update_size` | `string` | Displayed APK size — informational only |
| `force_update` | `bool` | `true` → user cannot dismiss the dialog and must update to continue |

---

<div align="center">

## 🔄 How to Push a New Release

</div>

**Step 1 — Upload the new APK to GitHub Releases**

Create a new release tag (e.g. `pure-status-next`) and attach the signed APK file.

**Step 2 — Update `pure-status.json`**

```json
{
  "version_code": 40,
  "version_name": "0.4.0",
  "apk_url": "https://github.com/Matrix1999/Pure_status_updater/releases/latest/download/pure-status-hd.apk",
  "changelog": "Pure Status HD stability and media-processing improvements",
  "update_size": "See release asset",
  "force_update": false
}
```

> ⚠️ Always increment `version_code` — the app uses this integer to decide whether to prompt.
> If `force_update` is `true`, the user **cannot** skip the update.

**Step 3 — Commit and push**

```bash
git add pure-status.json
git commit -m "chore: publish the next Pure Status HD release"
git push
```

The app picks up the change on next launch automatically.

---

<div align="center">

## 🛡️ Force Update Behaviour

</div>

```
force_update: false   →   Update dialog shown, user can dismiss and continue
force_update: true    →   Blocking dialog shown, app is unusable until updated
```

Use `force_update: true` whenever the update contains:
- Security patches
- Server API changes that break older clients
- Certificate or signing changes

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:24243e,50:302b63,100:0f0c29&height=120&section=footer&animation=fadeIn" width="100%"/>

*Pure Status HD — Update Panel*

</div>
