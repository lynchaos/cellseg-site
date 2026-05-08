---
layout: default
title: Download
description: Download the latest CellSeg APK for Android 8.0 (API 26) and later. Free and open source.
---

<div class="page-hero">
  <div class="container">
    <h1>Download CellSeg</h1>
    <p>Free, open source. Android 8.0 (API&nbsp;26) or later.</p>
  </div>
</div>

<div class="content">
  <div class="container">

    <div class="download-card">
      <div class="app-name">CellSeg</div>
      <div class="app-meta">On-device cell segmentation &middot; Android</div>
      <a class="btn btn-primary btn-lg"
         href="https://github.com/lynchaos/cellseg/releases/latest"
         target="_blank" rel="noopener noreferrer">
        &#8659;&nbsp; Download latest APK
      </a>
      <a class="release-link"
         href="https://github.com/lynchaos/cellseg/releases"
         target="_blank" rel="noopener noreferrer">
        All releases on GitHub ↗
      </a>
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
| Model (downloaded on first use) | ~26 MB |
| Recommended RAM | 2 GB |
| Supported ABIs | arm64-v8a, x86\_64 |

## How to install (sideload)

CellSeg is not distributed via the Play Store. Install via APK sideloading:

1. On your Android device open **Settings → Apps → Special app access → Install unknown apps**.
2. Allow your browser or file manager to install unknown apps.
3. Download the APK from the button above.
4. Open the downloaded `.apk` file and tap **Install**.
5. Launch CellSeg. On the first run, tap **Download model** to fetch the ~26 MB ONNX file over Wi-Fi.

<div class="note">
  <strong>Tip:</strong> Keep the APK after installation — you can reinstall from the same file
  if you uninstall and re-install without losing your run history (history is lost on uninstall
  since files are in app-private storage).
</div>

## Permissions

| Permission | Reason |
|---|---|
| `CAMERA` | Capture microscopy images directly |
| `READ_MEDIA_IMAGES` / `READ_EXTERNAL_STORAGE` | Import images from the gallery or a file manager |
| `INTERNET` | Download the ONNX model; optional cloud segmentation |
| `WRITE_EXTERNAL_STORAGE` (≤ API 28) | Export CSV/images on older Android versions |

All images and segmentation results are stored in **app-private storage** (`/data/data/…`)
and are deleted automatically when the app is uninstalled.
See the [Privacy Policy](/privacy) for full details.

## Verify the APK (optional)

You can verify the downloaded APK with the SHA-256 hash listed on each
[GitHub release page](https://github.com/lynchaos/cellseg/releases).

```bash
# macOS / Linux
shasum -a 256 cellseg-*.apk

# Windows (PowerShell)
Get-FileHash cellseg-*.apk -Algorithm SHA256
```

  </div>
</div>
