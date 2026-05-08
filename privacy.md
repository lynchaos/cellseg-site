---
layout: default
title: Privacy Policy
page_hero_title: Privacy Policy
page_hero_subtitle: Last updated May 2026 &mdash; see <a href="https://github.com/lynchaos/CellSeg/commits/main/PRIVACY.md" target="_blank" rel="noopener noreferrer">git history</a> for all changes.
description: CellSeg privacy policy — what data is collected, how network requests are made, and how files are stored.
---

## Summary

CellSeg collects **no personal data**. There are no analytics, no crash reporters, and no
advertising SDKs in the app. The only outbound network traffic is the one-time model download
and any cloud segmentation requests you explicitly initiate yourself.

## Data collected

- **No personal identifiers** are collected or transmitted.
- **No analytics SDK** is included (no Firebase, no Mixpanel, no Amplitude, etc.).
- **No crash reporting SDK** is included (no Crashlytics, no Sentry, etc.).
- **No advertising identifiers** are accessed.
- Images you capture or analyse remain on your device unless you explicitly send them to a
  cloud segmentation endpoint that you configure.

## Network requests

### Local segmentation mode

When using **local segmentation** (the default), no image data or metadata ever leaves your
device. The only network request CellSeg makes is a **one-time download** of the ONNX model
file (~14 MB) from the configured model host (currently a public Hugging Face repository).

After the model has been downloaded, local segmentation works entirely offline.

### Cloud segmentation mode

When using **cloud segmentation** (Hugging Face Gradio Space), the image you are processing
is sent over HTTPS to the Gradio Space you have configured.

- Please review the [Hugging Face Privacy Policy](https://huggingface.co/privacy) and the
  privacy terms of the specific Space you connect to.
- Your Hugging Face API token (if provided) is stored in Android
  `EncryptedSharedPreferences` and is **never** logged or written to any storage other than
  that encrypted store. It is transmitted only to `api.huggingface.co` and your configured Space.
- Cloud mode is opt-in and disabled by default.

## File storage

All files produced by CellSeg — captured images, segmentation outputs (masks, outline PNGs,
flow visualisations), metrics, and the ONNX model — are stored in
**app-private storage** (`Context.filesDir`, typically `/data/data/uk.yaylali.cellseg/files/`).

This storage is:

- Not accessible to other apps without root access.
- **Deleted automatically** when CellSeg is uninstalled.
- Excluded from Android Auto Backup (the app opts out to protect potentially sensitive
  microscopy images).

## Permissions

| Permission | Purpose |
|---|---|
| `CAMERA` | Capture microscopy images with the phone camera |
| `READ_MEDIA_IMAGES` / `READ_EXTERNAL_STORAGE` | Import images from gallery or file manager |
| `INTERNET` | Model download; optional cloud segmentation |
| `WRITE_EXTERNAL_STORAGE` (API ≤ 28) | Export results on older Android versions |

## No third-party SDKs

CellSeg does not include any of the following categories of SDK:

- Advertising (AdMob, Meta Audience Network, etc.)
- Analytics (Firebase Analytics, Mixpanel, Amplitude, etc.)
- Crash reporting (Crashlytics, Sentry, Bugsnag, etc.)
- Social login or sharing

A complete list of all third-party libraries and their licences is published in the
[NOTICE](https://github.com/lynchaos/CellSeg/blob/main/NOTICE) file in the source repository.

## Children's privacy

CellSeg is a research tool intended for adult researchers and scientists.
It is not directed at children and does not knowingly collect data from anyone under 13.

## Changes to this policy

Material changes will be announced via a commit to
[PRIVACY.md](https://github.com/lynchaos/CellSeg/blob/main/PRIVACY.md) in the repository.
The git history provides a full audit trail of all changes.

## Contact

Questions or concerns about privacy: `support@yaylali.uk`
