---
layout: default
home: true
title: CellSeg — On-device cell segmentation for Android
description: >-
  Segment brightfield, phase-contrast, and fluorescence microscopy images
  directly on your Android device. Cellpose cyto3 ONNX runs entirely
  on-device — no data leaves your phone.
---

<section class="hero">
<div class="container">
<div class="hero-badge">⚠ Research use only &mdash; not a medical device</div>
<h1>Segment cells<br><em>on your device</em></h1>
<p class="hero-sub">After a one-time ~25&nbsp;MB model download, segmentation runs entirely on-device &mdash; no cloud, no account, no data upload required for inference.</p>
<div class="hero-actions">
<a class="btn btn-primary btn-lg" href="/download">&#8659; Download APK</a>
<a class="btn btn-outline btn-lg" href="https://github.com/lynchaos/CellSeg" target="_blank" rel="noopener noreferrer">GitHub ↗</a>
</div>
</div>
</section>

<section class="features">
<div class="container">
<div class="section-title">
<h2>Everything you need, in your pocket</h2>
<p>From image capture to quantitative metrics — entirely offline.</p>
</div>
<div class="features-grid">
<div class="feature-card">
<div class="feature-icon">🧫</div>
<h3>On-device inference</h3>
<p>The ~25 MB Cellpose cyto3 ONNX (FP32) model runs fully on-device via ONNX Runtime 1.19 with XNNPACK acceleration. No internet required.</p>
</div>
<div class="feature-card">
<div class="feature-icon">☁</div>
<h3>Cloud fallback</h3>
<p>Optionally route to your own Hugging Face Gradio Space for higher-resolution inference or when device resources are limited. Your images and API token stay private.</p>
</div>
<div class="feature-card">
<div class="feature-icon">📷</div>
<h3>Camera &amp; TIFF import</h3>
<p>Capture directly with the phone camera or import TIFF files from a microscopy export. Brightfield, phase-contrast, and fluorescence channels supported.</p>
</div>
<div class="feature-card">
<div class="feature-icon">📊</div>
<h3>Quantitative metrics</h3>
<p>Cell count, confluence %, mean/median cell area, density (cells/cm²), and area histograms — computed per run and exportable as CSV.</p>
</div>
<div class="feature-card">
<div class="feature-icon">📋</div>
<h3>Batch processing</h3>
<p>Queue multiple images for sequential segmentation. Export a combined metrics CSV for all runs with one tap.</p>
</div>
<div class="feature-card">
<div class="feature-icon">🔒</div>
<h3>Privacy-first</h3>
<p>Zero analytics, no ads, no crash reporters. Your HuggingFace token is stored in EncryptedSharedPreferences. All files live in app-private storage.</p>
</div>
</div>
</div>
</section>

<section class="built-on">
<div class="container">
<p class="built-on-label">Built on open source</p>
<div class="built-on-row">
<span class="built-on-item">Cellpose cyto3</span>
<span class="built-on-item">ONNX Runtime 1.19</span>
<span class="built-on-item">Jetpack Compose</span>
<span class="built-on-item">Hilt</span>
<span class="built-on-item">Room</span>
<span class="built-on-item">CameraX 1.4</span>
</div>
</div>
</section>
