---
layout: default
title: Documentation
description: How to use CellSeg — getting started, segmentation modes, parameters, export, and model management.
---

<div class="page-hero">
  <div class="container">
    <h1>Documentation</h1>
    <p>Everything you need to get from raw image to quantified results.</p>
  </div>
</div>

<div class="content">
  <div class="container">

## Getting started

### 1 — Install and download the model

After installing the APK ([Download](/download)), launch CellSeg.
On the first run the app offers to download the Cellpose cyto3 ONNX model (~26 MB).
Accept the prompt, or visit **Settings → Model management → Download model** later.
A Wi-Fi connection is recommended.

### 2 — Capture or import an image

From the **Home** screen:

- Tap **Camera** to capture a new image with your phone camera.
- Tap **Gallery** to pick an existing image (JPEG, PNG, or TIFF) from storage.

You will be prompted to tag the sample with optional metadata:
**channel** (brightfield / phase-contrast / fluorescence), **magnification**, **cell line**,
**well ID**, and **timepoint**.

### 3 — Run segmentation

On the **Analyse** screen, choose your parameters (see [Parameter reference](#parameter-reference)),
then tap **Run segmentation**. Progress is shown in real time.

### 4 — View results

After a run completes you are taken to the **Run detail** screen, which shows:

- Side-by-side slider comparing the original image and the segmented outline overlay.
- Flows visualisation (optional).
- Metrics: cell count, confluence %, mean and median cell area, estimated cell density.
- Export options: outline PNG, mask TIFF, CSV.

---

## Segmentation modes

### Local (on-device)

The default mode. The Cellpose cyto3 FP16 ONNX model runs entirely on-device via
[ONNX Runtime Android](https://onnxruntime.ai) with the XNNPACK execution provider.

- **No internet required** after the initial model download.
- Processing time: typically 3–15 s on a mid-range device at 256 px max-resize.
- Image is rescaled to fit within `max_resize` before inference.

### Cloud (Hugging Face Gradio Space)

If you have a Hugging Face API token and a Gradio Space running Cellpose, you can route
inference to the cloud for larger images or faster turnaround on capable hardware.

Configure in **Settings → Hugging Face** by entering your Space slug and API token.
Your token is stored encrypted on-device and is only sent to `api.huggingface.co` and your Space.

> **Privacy note:** when using cloud mode, your image is uploaded to the configured Space.
> Review the Hugging Face [Privacy Policy](https://huggingface.co/privacy) and your Space's terms.

---

## Parameter reference

| Parameter | Range | Default | Description |
|---|---|---|---|
| `diameter` | 5–500 px | 30 px | Expected cell diameter in pixels at the rescaled resolution. The most important parameter — match it to your cell size. |
| `flow_threshold` | 0.0–3.0 | 0.4 | Maximum allowed flow error. Higher values detect more (potentially spurious) cells. |
| `cellprob_threshold` | −6.0 to +6.0 | 0.0 | Cell probability cutoff. Lower values include more marginal detections. |
| `max_resize` | 256–2000 px | 256 px | The longest image edge is rescaled to this value before inference. Higher values improve accuracy for small cells but increase memory and time. |
| `max_iter` | 100–500 | 250 | Maximum dynamics integration iterations. Increase for dense or complex samples. |

### Choosing diameter

Diameter is the most impactful parameter. A quick way to estimate it:

1. Open a representative image.
2. Manually measure the diameter of a typical cell in pixels (use any image viewer with a ruler).
3. Set `diameter` to that value.

If you are using a **magnification preset** (see below), the diameter is not changed automatically —
you should still set it to the apparent cell diameter **in pixels at the rescaled resolution**.

### Magnification presets

Presets adjust `max_iter` to match typical image density at each magnification.
The `diameter` field is not changed by a preset — adjust it manually.

| Preset | max\_iter | Typical use |
|---|---|---|
| Default | 250 | General purpose |
| 4× objective | 200 | Low magnification, sparse samples |
| 10× objective | 250 | Standard |
| 20× objective | 300 | High magnification, dense samples |

---

## Calibration and physical units

To convert pixel areas to physical units (µm², cells/cm²), set up a calibration entry in
**Settings → Calibration**.

For each objective you use, enter:

- **Magnification label** (e.g. `10×`)
- **px / µm** — pixels per micrometre at that magnification (from your microscope spec sheet)
- **FOV width / height** in mm (optional; required for density calculation)

Once calibration is set, per-run metrics will include mean cell area in µm² and
estimated density in cells/cm².

---

## Exporting results

### Single run export

From the **Run detail** screen, tap the **Export** menu to choose:

| Format | Contents |
|---|---|
| Outline PNG | Original image with segmentation outlines overlaid |
| Mask TIFF | 16-bit label mask (each cell has a unique integer label) |
| Metrics CSV | Single row: run ID, timestamp, cell count, confluence %, area stats |

### Batch export

From the **History** or **Batch** screen, tap the **Export CSV** button to download
a single CSV containing metrics for all selected or all queued runs.

---

## Model management

Access via **Settings → Model management**.

- **SHA-256**: displayed so you can verify the downloaded model matches the published hash.
- **Test inference**: runs a 256×256 dummy input through the model and reports latency.
- **Re-download**: deletes and re-fetches the model from the canonical source.
- **Delete model**: removes the model from storage (segmentation will be unavailable until re-downloaded).
- **Last verified**: timestamp of the most recent successful test inference.

---

## Troubleshooting

**Segmentation returns zero cells**
- Check that `diameter` is appropriate for your image. Too large or too small a value often causes missed detections.
- Lower `cellprob_threshold` (e.g. to −2.0).
- Ensure the image has reasonable contrast. Very dim or saturated images degrade accuracy.

**App is very slow during inference**
- `max_resize = 256` is recommended for real-time use. Avoid values above 512 on low-RAM devices.
- Close background apps to free RAM.

**Model download fails**
- Ensure a stable internet connection.
- Check that you have at least 50 MB of free storage.
- Try again from **Settings → Model management → Re-download**.

**Cloud inference returns an error**
- Verify your HuggingFace API token is valid and has access to the Space.
- Check the Space slug format: `username/space-name`.

  </div>
</div>
