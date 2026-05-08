---
layout: default
title: About
description: About CellSeg, the Cellpose model, the author, and the open-source licence.
---

<div class="page-hero">
  <div class="container">
    <h1>About CellSeg</h1>
    <p>On-device cell segmentation for Android &mdash; built on Cellpose cyto3.</p>
  </div>
</div>

<div class="content">
  <div class="container">

## What is CellSeg?

CellSeg is a free, open-source Android application for quantitative cell segmentation
of microscopy images. It is designed for researchers and field scientists who need rapid,
reproducible cell counting without cloud dependencies or specialised desktop hardware.

Key design goals:

- **Offline-first** — the full segmentation pipeline runs on-device.
- **Quantitative** — cell count, confluence, area statistics, and density are computed per run.
- **Privacy-preserving** — no analytics, no data upload in local mode.
- **Open** — MIT-licensed source, MIT-licensed model weights (Cellpose BSD-3-Clause).

## The model: Cellpose cyto3

CellSeg uses the **Cellpose cyto3** generalised segmentation model, exported to ONNX FP16
format. The model was trained by Carsen Stringer, Tim Wang, Michaël Pachitariu,
and collaborators at HHMI Janelia Research Campus.

The model is distributed under the **BSD 3-Clause Licence**.

### Citation

If you use CellSeg in published research, please cite the original Cellpose papers:

> Stringer, C., Wang, T., Michaelos, M. & Pachitariu, M.
> **Cellpose: a generalist algorithm for cellular segmentation.**
> *Nature Methods* 18, 100–106 (2021).
> [https://doi.org/10.1038/s41592-020-01018-x](https://doi.org/10.1038/s41592-020-01018-x)

> Pachitariu, M. & Stringer, C.
> **Cellpose 2.0: how to train your own model.**
> *Nature Methods* 19, 1634–1641 (2022).
> [https://doi.org/10.1038/s41592-022-01663-4](https://doi.org/10.1038/s41592-022-01663-4)

The full attribution and all third-party licences are published in the
[NOTICE](https://github.com/lynchaos/cellseg/blob/main/NOTICE) file.

## Author

**Kemal Yaylali**
[yaylali.uk](https://yaylali.uk) &middot; `support@yaylali.uk`

## Licence

CellSeg is released under the **MIT Licence**. You are free to use, copy, modify,
merge, publish, distribute, sublicense, and/or sell copies of the software under
the terms of that licence.

See [LICENSE](https://github.com/lynchaos/cellseg/blob/main/LICENSE) for the full text.
Third-party attributions are listed in [NOTICE](https://github.com/lynchaos/cellseg/blob/main/NOTICE).

## Contributing

Contributions are welcome — bug reports, feature requests, and pull requests.
Please read [CONTRIBUTING.md](https://github.com/lynchaos/cellseg/blob/main/CONTRIBUTING.md)
before opening a pull request.

## Disclaimer

<div class="warn">
  <strong>Research use only.</strong>
  CellSeg is an experimental research tool. It is <strong>not a medical device</strong>,
  is not CE-marked, and is not FDA-cleared or FDA-approved.
  Results must not be used for clinical, diagnostic, or therapeutic decision-making.
  Always validate outputs against established laboratory methods before relying on them
  for any consequential decision.
</div>

  </div>
</div>
