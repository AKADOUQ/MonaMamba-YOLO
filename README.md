# MonaMamba-YOLO-Robust-Dense-Aluminum-Can-Anomaly-Detection-under-Industrial-Scenario

﻿
This repository releases an **annotated sample subset** on aluminum-can anomaly detection (YOLO-MAD), aiming to improve **transparency** and **reproducibility** under industrial privacy/IP constraints.
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
## Data

This release provides a sample subset packaged as `download.zip` (images and YOLO-format labels) together with `README.md`. The repository root contains only:

<pre>
.
├── download.zip
└── README.md
</pre>

After unzipping `download.zip`, the extracted folder contains the sample images and labels:

<pre>
download/
├── images/          # sample images (.jpg)
└── labels/          # YOLO-format annotations (.txt)
</pre>

Image–label pairs are matched by the identical filename stem (i.e., `download/images/<stem>.jpg` corresponds to `download/labels/<stem>.txt`). For example:

<pre>
download/images/D01_xxx_00_00_00-00_05_00_3087.jpg
download/labels/D01_xxx_00_00_00-00_05_00_3087.txt
</pre>

Some filenames may include spaces; when scripting, wrap paths in quotes.


---

## Annotation Specification (YOLO)

### Class Definition

| class_id | name       | definition |
|---------:|------------|------------|
| 0        | fallen can | A can that has fallen/tipped over on the production line (abnormal target). |

### Label Format

Each label file `download/labels/<stem>.txt` contains 0 or more lines in the standard **YOLO txt** format:

class_id cx cy w h

- `class_id`: integer (only `0` in this dataset)
- `cx, cy, w, h`: **normalized** to `[0, 1]` by image width/height

**Empty label file** means **no fallen can** in the image.

### Bounding-Box Rules

To ensure consistent annotations:
- **Boundary target:** boxes should follow the **physical can body**; specular highlights alone should not define the box.
- **Occlusion:** annotate the **visible extent** of the fallen can when partially occluded.
- **Truncation/out-of-frame:** annotate the visible part and keep the box within the image.
- **Motion blur / glare:** annotate if the can boundary remains identifiable; otherwise omit.
- **Multiple instances:** annotate each fallen can separately (one line per instance).

---

## Evaluation Details

This section describes the evaluation protocol used in the manuscript so readers can interpret reported numbers consistently.

### Input & Pre-processing
- Input size: **640 × 640**
- Resize policy: `<letterbox (keep aspect ratio) / direct resize>`  
  *(Use the same policy for all compared methods.)*
- Test-time augmentation (TTA): **No** (unless explicitly stated)

### Post-processing
- NMS: standard NMS
- Confidence threshold: `<value or "Ultralytics default">`
- NMS IoU threshold: `<value or "Ultralytics default">`
- Max detections per image: `<value or "Ultralytics default">`

> Recommendation: record the exact inference stack used in your experiments for reference:  
> - Framework: `<PyTorch version>`, `<CUDA version>`  
> - Implementation: `<Ultralytics/YOLO version>` (e.g., `ultralytics==x.y.z`)

### Metrics
We report:
- **mAP@0.5** (IoU = 0.5)
- **mAP@0.5:0.95** (IoU = 0.50:0.05:0.95, COCO-style)

Precision/Recall should be computed under the same IoU criterion used for mAP reporting to avoid inconsistency.

---

## Citation

If you use this sample subset, please cite:

<MonaMamba-YOLO: Robust Dense Aluminum-Can Anomaly Detection under Industrial  Scenario>, IEEE Transactions on Industrial Informatics (under review).

---

## Access to Full Materials (Restricted)

The **full dataset** and additional materials are retained and may be accessed for **research verification** under a data-use agreement upon reasonable request.

- Corresponding author: `<name>`
- Email: `<email>`
- Request subject: `YOLO-MAD dataset verification request`
- Intended use: research verification / benchmarking under agreement

---

## License

