---
layout: default
title: Privacy Policy
description: CellSeg privacy policy — what data is collected, how network requests are made, and how files are stored.
---

<div class="page-hero">
  <div class="container">
    <h1>Privacy Policy</h1>
    <p>Last updated: May 2026 &mdash; see <a href="https://github.com/lynchaos/cellseg/commits/main/PRIVACY.md" target="_blank" rel="noopener noreferrer">git history</a> for changes.</p>
  </div>
</div>

<div class="content">
  <div class="container">

## Data collected

CellSeg collects **no personal data**. Specifically:

- No analytics SDK is included.
- No crash reporting is sent to any third party.
- No advertising identifiers are accessed.
- Images captured or analysed remain on your device unless you explicitly share them via the Android Share sheet or configure cloud segmentation (see below).

## Network requests

### Local segmentation mode

When using **local segmentation**, no image data or metadata leaves your device.
The only network request is the one-time download of the ONNX model file (~26 MB) from the
configured model host (currently a public Hugging Face repository).

### Cloud segmentation mode

When using **cloud segmentation** (Hugging Face Gradio Space), images are sent to the
Gradio Space you have configured for processing.

- Please review the [Hugging Face Privacy Policy](https://huggingface.co/privacy) and the
  terms of the specific Space you connect to.
- Your Hugging Face API token (if provided) is stored in Android's
  `EncryptedSharedPreferences` and is **never** logged or transmitted to any server other than
  `api.huggingface.co` and your configured Space.

## Storage

All files produced by CellSeg — captured images, segmentation outputs (masks, outlines, flows),
and metrics — are stored in **app-private storage** (`Context.filesDir`).

This storage is:

- Not accessible to other apps without root access.
- **Deleted automatically** when CellSeg is uninstalled.
- Not backed up to Google Drive by default (the app opts out of Android Auto Backup for
  sensitive image data).

## No third-party SDKs

CellSeg does not include any of the following:

- Advertising SDKs (AdMob, Meta Audience Network, etc.)
- Analytics SDKs (Firebase Analytics, Mixpanel, Amplitude, etc.)
- Crash reporting SDKs (Crashlytics, Sentry, etc.)
- Social login or sharing SDKs

The complete list of third-party libraries is published in the
[NOTICE](https://github.com/lynchaos/cellseg/blob/main/NOTICE) file in the source repository.

## Contact

Questions or concerns about privacy: `support@yaylali.uk`

  </div>
</div>
