---
layout: default
title: Download
page_hero_title: Download CellSeg
page_hero_subtitle: Free, open source. Android 8.0 (API&nbsp;26) or later. No account required.
description: Download the latest CellSeg APK for Android 8.0 (API 26) and later. Free and open source.
---

<div class="download-card">
<div class="app-name">CellSeg</div>
<div class="app-meta">On-device cell segmentation &middot; Android</div>
<a class="btn btn-primary btn-lg"
   href="https://github.com/lynchaos/CellSeg/releases/latest"
   target="_blank" rel="noopener noreferrer">&#8659;&nbsp; Download latest APK</a>
<a class="release-link"
   href="https://github.com/lynchaos/CellSeg/releases"
   target="_blank" rel="noopener noreferrer">All releases on GitHub ↗</a>
</div>

<div class="warn">
<strong>Research use only.</strong>
CellSeg is not a medical device and is not CE-marked or FDA-cleared.
Do not use for clinical, diagnostic, or therapeutic decision-making.
</div>

## Requirements

| Requirement | Minimum |
|---|---|
| Android version | 8.0 (API 26) |
| App install size | ~15 MB |
| Model (downloaded on first launch) | ~26 MB |
| Recommended RAM | 2 GB |
| Supported ABIs | arm64-v8a, x86\_64 |

## How to install (sideload)

CellSeg is distributed as a direct APK — it is not on the Play Store.

1. On your Android device go to **Settings → Apps → Special app access → Install unknown apps**.
2. Grant your browser or file manager permission to install unknown apps.
3. Tap **Download latest APK** above.
4. Open the downloaded `.apk` file and tap **Install**.
5. Launch CellSeg. On first run tap **Download model** to fetch the ~26 MB ONNX file (Wi-Fi recommended).

<div class="note">
<strong>Tip:</strong> Keep the APK file after installation.
You can reinstall from it without losing your run history — provided you don't uninstall first
(history is stored in app-private storage and is deleted on uninstall).
</div>

## Permissions

| Permission | Why it's needed |
|---|---|
| `CAMERA` | Capture microscopy images directly with the phone camera |
| `READ_MEDIA_IMAGES` / `READ_EXTERNAL_STORAGE` | Import images from the gallery or a file manager |
| `INTERNET` | Download the ONNX model on first use; optional cloud segmentation |
| `WRITE_EXTERNAL_STORAGE` (≤ API 28) | Export CSV/images on older Android versions |

All images and segmentation outputs are stored in **app-private storage** (`/data/data/uk.yaylali.cellseg/`)
and are deleted automatically when the app is uninstalled.
See the [Privacy Policy](/privacy) for full details.

## Verify the APK (optional)

Each [GitHub release](https://github.com/lynchaos/CellSeg/releases) lists the SHA-256 hash of the APK.
Verify on your desktop after downloading:

```sh
# macOS / Linux
sha256sum CellSeg-v0.1.0.apk

# macOS only
shasum -a 256 CellSeg-v0.1.0.apk

# Windows PowerShell
Get-FileHash CellSeg-v0.1.0.apk -Algorithm SHA256
```

Compare the output against the hash on the release page.

## Open source

CellSeg is MIT-licensed. Source code is available at
[github.com/lynchaos/CellSeg](https://github.com/lynchaos/CellSeg).
Third-party licences are listed on the [About](/about) page and in the
[NOTICE](https://github.com/lynchaos/CellSeg/blob/main/NOTICE) file.

```bash
# macOS / Linux
shasum -a 256 cellseg-*.apk

# Windows (PowerShell)
Get-FileHash cellseg-*.apk -Algorithm SHA256
```

  </div>
</div>
