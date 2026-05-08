---
layout: default
title: Documentation
page_hero_title: Documentation
page_hero_subtitle: Everything you need to go from raw image to quantified results.
description: How to use CellSeg — getting started, segmentation modes, parameters, export, calibration, and model management.
---

<div class="toc">
<strong>Contents</strong>
<ol>
<li><a href="#getting-started">Getting started</a></li>
<li><a href="#segmentation-modes">Segmentation modes</a></li>
<li><a href="#parameter-reference">Parameter reference</a></li>
<li><a href="#calibration-and-physical-units">Calibration &amp; physical units</a></li>
<li><a href="#exporting-results">Exporting results</a></li>
<li><a href="#batch-processing">Batch processing</a></li>
<li><a href="#model-management">Model management</a></li>
<li><a href="#troubleshooting">Troubleshooting</a></li>
</ol>
</div>

---

## Getting started

### 1 — Install and download the model

After installing the APK ([Download](/download)), launch CellSeg.
On the first run the app offers to download the Cellpose cyto3 ONNX model (~26 MB).
Accept the prompt, or visit **Settings → Model management → Download model** later.
A Wi-Fi connection is recommended for the initial download.

<div class="tip">
<strong>Verify the model after download.</strong>
Go to <strong>Settings → Model management → Test inference</strong> to run a 256×256 dummy
input through the model and confirm it is working correctly before your first real run.
</div>

### 2 — Capture or import an image

From the **Home** screen:

- Tap **Camera** to capture a new image with your phone camera.
- Tap **Gallery** to import an existing image (JPEG, PNG, or TIFF) from storage.

You will be prompted to tag the sample with optional metadata:
**channel** (brightfield / phase-contrast / fluorescence), **magnification**, **cell line**,
**well ID**, and **timepoint**. These tags are stored with each run and appear in exported CSV files.

### 3 — Set parameters and run segmentation

On the **Analyse** screen:

1. Set **diameter** to match the expected cell size in your image (see [Choosing diameter](#choosing-diameter)).
2. Choose a **segmentation mode** (local or cloud — see [Segmentation modes](#segmentation-modes)).
3. Adjust advanced parameters if needed (see [Parameter reference](#parameter-reference)).
4. Tap **Run segmentation**. A progress indicator shows the current pipeline stage.

### 4 — View and export results

After the run completes you are taken to the **Run detail** screen:

- **Slider overlay** — swipe to compare the original image with the segmented outline overlay.
- **Flows visualisation** — toggle to show the Cellpose gradient flows (useful for diagnosing missed cells).
- **Metrics panel** — cell count, confluence %, mean and median cell area, estimated cell density.
- **Export** — outline PNG, mask TIFF, or metrics CSV for the current run.

---

## Segmentation modes

### Local (on-device)

The default mode. The Cellpose cyto3 FP16 ONNX model runs entirely on-device via
[ONNX Runtime Android](https://onnxruntime.ai) with the XNNPACK execution provider.

- No internet required after the initial model download.
- Processing time: typically 3–15 s on a mid-range device at 256 px max-resize.
- Images are rescaled to fit within `max_resize` before inference; original resolution is preserved on disk.

### Cloud (Hugging Face Gradio Space)

If you have a Hugging Face API token and a Gradio Space running Cellpose, you can route
inference to the cloud for larger images or faster turnaround on capable hardware.

Configure in **Settings → Hugging Face** by entering your Space slug and API token.
Your token is stored in `EncryptedSharedPreferences` on-device and is transmitted only to
`api.huggingface.co` and your configured Space.

<div class="warn">
<strong>Privacy:</strong> when using cloud mode, your image is uploaded to the configured Space.
Review the Hugging Face <a href="https://huggingface.co/privacy">Privacy Policy</a> and your Space's terms before enabling this mode.
</div>

---

## Parameter reference

| Parameter | Range | Default | Description |
|---|---|---|---|
| `diameter` | 5–500 px | 30 px | Expected cell diameter in pixels **at the rescaled resolution**. The single most impactful parameter — match it to your cell type. |
| `flow_threshold` | 0.0–3.0 | 0.4 | Maximum allowed flow error per cell mask. Higher values recover more (potentially spurious) cells near region boundaries. |
| `cellprob_threshold` | −6.0 to +6.0 | 0.0 | Cell probability cutoff. Lower values include more marginal detections; raise this to suppress background false positives. |
| `max_resize` | 256–2000 px | 256 px | The longest image edge is rescaled to this value before inference. Higher values improve accuracy for small cells at the cost of memory and time. |
| `max_iter` | 100–500 | 250 | Maximum dynamics integration iterations. Increase for dense or confluent samples. |

### Choosing diameter

`diameter` is the most impactful parameter. A mismatch (too large or too small) is the most
common reason for zero or very low cell counts.

**Quick estimation method:**

1. Open a representative image in any viewer with a ruler tool.
2. Measure the diameter of a typical cell in pixels.
3. If you are using `max_resize = 256` and your original image is 1024 px wide, divide the
   measured pixel diameter by 4 (the downscale factor). Set `diameter` to the resulting value.
4. For a 512 px max-resize, divide by 2, and so on.

**Rule of thumb values:**

| Cell type / objective | Typical diameter (px at 256 px resize) |
|---|---|
| Large cells (e.g. HEK293T, 10× obj.) | 25–45 |
| Medium cells (e.g. HeLa, 20× obj.) | 15–25 |
| Small cells (e.g. lymphocytes, 40× obj.) | 8–15 |

### Magnification presets

Presets adjust `max_iter` to match typical image density at each magnification.
The `diameter` field is **not** changed by a preset — always set it manually.

| Preset | max\_iter | Typical use |
|---|---|---|
| Default | 250 | General purpose |
| 4× objective | 200 | Low magnification, sparse samples |
| 10× objective | 250 | Standard tissue culture |
| 20× objective | 300 | High magnification, dense samples |

### Advanced tips

- **flow_threshold**: if you are getting fragmented masks on large cells, lower this value (e.g. 0.1–0.2).
- **cellprob_threshold**: if background regions are being detected as cells, raise this toward +2 or +3.
- **max_resize**: for small cells (< 10 px diameter at 256 px), try 512 or 1024 px for better boundary delineation. Expect 4–10× slower inference on device.
- **max_iter**: increase to 400–500 only if cells are very confluent or have complex shapes.

---

## Calibration and physical units

To convert pixel areas to physical units (µm², cells/cm²), set up a calibration entry in
**Settings → Calibration**.

For each objective you use, enter:

- **Magnification label** (e.g. `10×`)
- **px / µm** — pixels per micrometre at that magnification (from your microscope spec sheet or
  by imaging a stage micrometer)
- **FOV width / height** in mm (optional; required for density calculation in cells/cm²)

Once calibration is configured, per-run metrics will report:

- Mean and median cell area in **µm²**
- Estimated cell density in **cells/cm²**

<div class="note">
<strong>Finding px/µm:</strong> your microscope's spec sheet should list the pixel size at each
objective, typically as µm/px. Take the reciprocal to get px/µm.
For example, 0.65 µm/px → 1.54 px/µm.
</div>

---

## Exporting results

### Single run export

From the **Run detail** screen, tap the **Export** button and choose a format:

| Format | Contents |
|---|---|
| **Outline PNG** | Original image with segmentation outlines overlaid in colour |
| **Mask TIFF** | 16-bit label mask — each detected cell has a unique integer ID (0 = background) |
| **Metrics CSV** | One row: run ID, timestamp, channel, magnification, cell line, well ID, cell count, confluence %, mean area, median area, density |

### Batch export

From the **History** or **Batch** screen, tap **Export CSV** to download a single CSV file
containing metrics for all selected runs. Useful for building a per-experiment dataset.

### CSV column reference

| Column | Type | Description |
|---|---|---|
| `run_id` | UUID | Unique identifier for this run |
| `timestamp` | ISO 8601 | Date and time the run completed |
| `image_path` | path | Path to the source image in app storage |
| `channel` | string | Brightfield / Phase-contrast / Fluorescence |
| `magnification` | string | Magnification label (user-supplied) |
| `cell_line` | string | Cell line tag (user-supplied) |
| `well_id` | string | Well/position tag (user-supplied) |
| `cell_count` | integer | Number of detected cells |
| `confluence_pct` | float | Percentage of image area covered by cells |
| `mean_area_px` | float | Mean cell area in pixels² |
| `median_area_px` | float | Median cell area in pixels² |
| `mean_area_um2` | float | Mean cell area in µm² (requires calibration) |
| `median_area_um2` | float | Median cell area in µm² (requires calibration) |
| `density_cells_cm2` | float | Estimated cell density in cells/cm² (requires calibration + FOV) |

---

## Batch processing

The **Batch** screen lets you queue multiple images for sequential on-device segmentation
using a shared set of parameters.

1. Tap **+ Add images** to select images from storage.
2. Set the shared segmentation parameters (these apply to all images in the queue).
3. Tap **Run batch**. Progress is shown per image.
4. When complete, tap **Export CSV** for a combined results file.

<div class="note">
<strong>Tip:</strong> Batch mode uses the same parameters for every image in the queue.
If your images require different diameters (e.g. different magnifications), run them as
separate batches or individual runs.
</div>

---

## Model management

Access via **Settings → Model management**.

| Action | Description |
|---|---|
| **SHA-256** | Displays the hash of the currently installed model so you can verify it against the published checksum |
| **Test inference** | Runs a 256×256 zero-input through the model and reports latency. Useful for confirming the model is loaded correctly after download. |
| **Re-download** | Deletes the current model file and re-fetches from the canonical source |
| **Delete model** | Removes the model from storage. Segmentation is unavailable until the model is re-downloaded. |
| **Last verified** | Timestamp of the most recent successful test inference |

### Model file details

| Property | Value |
|---|---|
| Architecture | Cellpose cyto3 (U-Net variant) |
| Format | ONNX FP16 |
| Input | 1 × 2 × H × W (normalised brightfield + nucleus channel) |
| Output | Flows (dX, dY), cell probability |
| File size | ~26 MB |
| Execution provider | XNNPACK (CPU) |

---

## Troubleshooting

### Segmentation returns zero cells

- **Wrong diameter** — this is the most common cause. Try setting `diameter` to 15, 30, and 60
  and see which gives sensible detections on your image type.
- **cellprob_threshold too high** — lower it toward −2.0 or −4.0.
- **Very low contrast** — very dim or saturated images degrade accuracy. Adjust acquisition settings
  if possible, or apply pre-processing outside the app.
- **Model not loaded** — go to **Settings → Model management → Test inference** to confirm the model
  runs successfully.

### Segmentation produces many false positives

- **cellprob_threshold too low** — raise it toward +2.0 or +3.0.
- **diameter too small** — sub-cellular features may be detected as cells. Increase diameter.
- **Background texture** — strongly textured backgrounds (e.g. fibrin gels) can confuse the model.
  The Cellpose cyto3 model is designed for cells in standard culture; results on atypical samples may vary.

### App is slow during inference

- `max_resize = 256` gives the best performance for real-time use. Avoid values above 512 on
  devices with < 3 GB RAM.
- Close background apps to free RAM before running segmentation on large images.
- On devices without XNNPACK support, inference falls back to the default CPU provider and will
  be slower. Check the test inference latency in **Model management** for a baseline.

### Model download fails

- Ensure a stable internet connection (Wi-Fi recommended).
- Check that you have at least 60 MB of free storage.
- Retry from **Settings → Model management → Re-download**.
- If the download URL is unreachable, check the
  [GitHub releases page](https://github.com/lynchaos/CellSeg/releases) for an alternative download.

### Cloud inference returns an error

- Verify your HuggingFace API token is valid and has access to the Space.
- Check the Space slug format: `username/space-name` (no `https://`, no trailing slash).
- Confirm the Space is running (not sleeping) — cold-start a sleeping Space by visiting it in a browser first.
- Check the Space logs in the Hugging Face web UI for application-level errors.

### Out-of-memory crash during inference

- Reduce `max_resize` to 256 px.
- Ensure at least 512 MB of free RAM before running.
- Restart the device to clear background memory pressure.

---

*Found a bug or have a feature request? Open an issue on
[GitHub](https://github.com/lynchaos/CellSeg/issues).*

