---
layout: default
title: About
page_hero_title: About CellSeg
page_hero_subtitle: On-device cell segmentation for Android &mdash; built on Cellpose cyto3.
description: About CellSeg, the Cellpose model, licensing, author, and open-source attribution.
---

## What is CellSeg?

CellSeg is a free, open-source Android application for quantitative cell segmentation of
microscopy images. It is designed for researchers and field scientists who need rapid,
reproducible cell counting without cloud dependencies or specialised desktop hardware.

Key design goals:

- **Offline-first** — the full segmentation pipeline runs on-device after a one-time model download.
- **Quantitative** — cell count, confluence %, mean/median cell area, and density are computed per run.
- **Privacy-preserving** — no analytics, no crash reporters, no data upload in local mode.
- **Open** — MIT-licensed source code; Cellpose codebase under BSD 3-Clause.

## The model: Cellpose cyto3

CellSeg uses the **Cellpose cyto3** generalised cell segmentation model, exported to ONNX FP32
format for on-device inference via ONNX Runtime 1.19 with XNNPACK acceleration.

The cyto3 model is part of the Cellpose project led by **Carsen Stringer** and **Marius Pachitariu** at HHMI Janelia Research Campus.

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

> Stringer, C. & Pachitariu, M.
> **Cellpose3: one-click image restoration for improved cellular segmentation.**
> *Nature Methods* 22, 592–599 (2025).
> [https://doi.org/10.1038/s41592-025-02595-5](https://doi.org/10.1038/s41592-025-02595-5)
> *(This is the cyto3 model used in CellSeg.)*

> Pachitariu, M., Rariden, M. & Stringer, C.
> **Cellpose-SAM: superhuman generalisation for cellular segmentation.**
> *bioRxiv* (2025).
> [https://doi.org/10.1101/2025.04.28.651001](https://doi.org/10.1101/2025.04.28.651001)
> *(Used in cloud/HuggingFace inference mode.)*

## Licences

### CellSeg — MIT Licence

```
MIT License

Copyright (c) 2025–2026 Kemal Yaylali

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Cellpose codebase — BSD 3-Clause Licence

The Cellpose source code is released under the BSD 3-Clause Licence
(Copyright © 2020 Howard Hughes Medical Institute). The full licence text is
in the upstream repository at
[github.com/MouseLand/cellpose/blob/main/LICENSE](https://github.com/MouseLand/cellpose/blob/main/LICENSE).

### Cellpose cyto3 weights — redistributed with permission

The cyto3 model weights themselves do not have an explicit upstream licence
statement. They are redistributed in this app's ONNX form at
[huggingface.co/kmlyyll/cellpose-cyto3-onnx](https://huggingface.co/kmlyyll/cellpose-cyto3-onnx)
with the explicit permission of the upstream authors at HHMI Janelia, granted by
Marius Pachitariu (May 2026), under the conditions of:

1. **Attribution** of the Cellpose papers and project.
2. **Licence propagation** — this notice must travel with any further redistribution.

For completeness on the upstream chain: Cellpose-SAM (used by the app's optional
cloud mode) sits on top of Segment Anything (SAM) weights. Per Michael Perham
(Director, Janelia Innovations & Open Science at HHMI Janelia, May 2026), these
upstream SAM weights carry a fully permissive licence that allows commercial
applications.

### ONNX Runtime — MIT Licence

ONNX Runtime is used for on-device model inference.

```
MIT License

Copyright (c) Microsoft Corporation

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### Third-party software

The following open-source libraries are used in CellSeg. All are included unmodified.
Full licence texts are in the
[NOTICE](https://github.com/lynchaos/CellSeg/blob/main/NOTICE) file.

| Library | Version | Licence | Copyright |
|---|---|---|---|
| Jetpack Compose (UI, Foundation, Material3) | 1.7.x | Apache 2.0 | Google LLC |
| Compose Navigation | 2.8.x | Apache 2.0 | Google LLC |
| AndroidX Room | 2.6.x | Apache 2.0 | Google LLC |
| AndroidX DataStore (Proto) | 1.1.x | Apache 2.0 | Google LLC |
| AndroidX Security Crypto | 1.1.x | Apache 2.0 | Google LLC |
| CameraX (core, camera2, lifecycle, view) | 1.4.x | Apache 2.0 | Google LLC |
| Hilt (Dagger Android) | 2.51.x | Apache 2.0 | Google LLC |
| Protocol Buffers (protobuf-javalite) | 4.x | BSD 3-Clause | Google LLC |
| Moshi (core + Kotlin codegen) | 1.15.x | Apache 2.0 | Square, Inc. |
| Retrofit | 2.11.x | Apache 2.0 | Square, Inc. |
| OkHttp | 4.12.x | Apache 2.0 | Square, Inc. |
| Coil (compose) | 2.7.x | Apache 2.0 | Coil Contributors |
| Timber | 5.0.x | Apache 2.0 | Jake Wharton |
| Google Tink (via Security Crypto) | 1.x | Apache 2.0 | Google LLC |

The Apache 2.0 Licence can be read at
[apache.org/licenses/LICENSE-2.0](https://www.apache.org/licenses/LICENSE-2.0).

## Author

**Kemal Yaylali**
[yaylali.uk](https://yaylali.uk) &middot; GitHub: [@lynchaos](https://github.com/lynchaos) &middot; `support@yaylali.uk`

## Contributing

Contributions are welcome — bug reports, feature requests, and pull requests.
Please read [CONTRIBUTING.md](https://github.com/lynchaos/CellSeg/blob/main/CONTRIBUTING.md)
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
