# MonaMamba-YOLO-Robust-Dense-Aluminum-Can-Anomaly-Detection-under-Industrial-Scenario

# YOLO-MAD Fallen Can Sample Subset
﻿
This repository releases an **annotated sample subset** for the TII manuscript on aluminum-can anomaly detection (YOLO-MAD), aiming to improve **transparency** and **reproducibility** under industrial privacy/IP constraints.
﻿
- **Task:** single-class object detection
- **Class:** `fallen can` (ID = 0)
﻿
> **Availability statement.**  
> Due to factory privacy, contractual restrictions, and IP protection, the **full dataset** and the **implementation** are not publicly released.  
> We release this **annotated sample subset** with annotation specifications and evaluation details, and retain all materials for research verification under a data-use agreement (with partner permission) upon reasonable request.
﻿
---
﻿
## 1. What’s Included
﻿
This release contains:
- `images/` — sample images (`.jpg`)
- `labels/` — YOLO-format annotations (`.txt`)
- `README.md` — this document
﻿
### 1.1 Directory Structure
.
├── images/
├── labels/
└── README.md﻿
﻿
### 1.2 Pairing Rule (IMPORTANT)

Image–label pairs are matched by **identical filename stem**:

- Image: `images/<stem>.jpg`
- Label: `labels/<stem>.txt`

For example:
- `images/D01_xxx_00_00_00-00_05_00_3087.jpg`
- `labels/D01_xxx_00_00_00-00_05_00_3087.txt`

**Do not rename files.** Some filenames may include spaces; when scripting, wrap paths in quotes.

---

## 2. Annotation Specification (YOLO)

### 2.1 Class Definition

| class_id | name       | definition |
|---------:|------------|------------|
| 0        | fallen can | A can that has fallen/tipped over on the production line (abnormal target). |

### 2.2 Label Format

Each label file `labels/<stem>.txt` contains 0 or more lines in the standard **YOLO txt** format:

class_id cx cy w h

- `class_id`: integer (only `0` in this dataset)
- `cx, cy, w, h`: **normalized** to `[0, 1]` by image width/height

**Empty label file** means **no fallen can** in the image.

### 2.3 Bounding-Box Rules (Consistency Guidelines)

To ensure consistent annotations:
- **Boundary target:** boxes should follow the **physical can body**; specular highlights alone should not define the box.
- **Occlusion:** annotate the **visible extent** of the fallen can when partially occluded.
- **Truncation/out-of-frame:** annotate the visible part and keep the box within the image.
- **Motion blur / glare:** annotate if the can boundary remains identifiable; otherwise omit.
- **Multiple instances:** annotate each fallen can separately (one line per instance).

---

## 3. Evaluation Details (Paper Protocol)

This section describes the evaluation protocol used in the manuscript so readers can interpret reported numbers consistently.

### 3.1 Input & Pre-processing
- Input size: **640 × 640**
- Resize policy: `<letterbox (keep aspect ratio) / direct resize>`  
  *(Use the same policy for all compared methods.)*
- Test-time augmentation (TTA): **No** (unless explicitly stated)

### 3.2 Post-processing
- NMS: standard NMS
- Confidence threshold: `<value or "Ultralytics default">`
- NMS IoU threshold: `<value or "Ultralytics default">`
- Max detections per image: `<value or "Ultralytics default">`

> Recommendation: record the exact inference stack used in your experiments for reference:  
> - Framework: `<PyTorch version>`, `<CUDA version>`  
> - Implementation: `<Ultralytics/YOLO version>` (e.g., `ultralytics==x.y.z`)

### 3.3 Metrics
We report:
- **mAP@0.5** (IoU = 0.5)
- **mAP@0.5:0.95** (IoU = 0.50:0.05:0.95, COCO-style)

Precision/Recall should be computed under the same IoU criterion used for mAP reporting to avoid inconsistency.

(Optional) If evaluating *tiny* cases:
- Tiny definition: `<relative bbox area threshold or pixel-size threshold>`
- Report: Tiny Recall (as used in the manuscript)

---

## 4. Integrity Check (Optional)

To validate that the release is complete:
- Each entry in `images.csv` should exist in `images/`
- Each entry in `labels.csv` should exist in `labels/`
- Each image should have a matching label file with the same stem, and vice versa

---

## 5. License & Usage

This sample subset is released **for academic research and benchmarking only**.  
Commercial use is not permitted without explicit written permission from the data owner/partner.

- License: `<choose a license or state custom terms>`  
  *(If you cannot adopt an OSI license, state custom “research-only” terms clearly.)*

---

## 6. Citation

If you use this sample subset, please cite:

<Your paper title>, IEEE Transactions on Industrial Informatics (under review).

---

## 7. Access to Full Materials (Restricted)

The **full dataset** and additional materials are retained and may be accessed for **research verification** under a data-use agreement (with partner permission) upon reasonable request.

- Corresponding author: `<name>`
- Email: `<email>`
- Request subject: `YOLO-MAD dataset verification request`
- Intended use: research verification / benchmarking under agreement
