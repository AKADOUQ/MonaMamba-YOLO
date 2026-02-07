# MonaMamba-YOLO: Robust Dense Aluminum-Can Anomaly Detection under Industrial Scenario

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

This sample subset uses a single detection class: `fallen can` (class_id = 0), defined as a can that has fallen/tipped over on the production line (abnormal target). Each label file `download/labels/<stem>.txt` contains 0 or more lines in the standard YOLO txt format:

<pre>
class_id  cx  cy  w  h
</pre>

Here `class_id` is an integer (only `0` in this dataset), and `cx, cy, w, h` are **normalized** to `[0, 1]` by image width/height. 

An empty label file indicates **no fallen can** in the corresponding image. 

Bounding boxes should follow the **physical can body** rather than specular highlights alone; 
For partial occlusion, annotate the **visible extent**; 
For truncation/out-of-frame cases, annotate the visible part and keep the box within the image; 
For motion blur/glare, annotate only when the can boundary remains identifiable; 
If multiple fallen cans appear, annotate each instance separately (one line per instance).

---

## Evaluation Details
﻿
This section summarizes the evaluation protocol used in the manuscript so readers can interpret the reported results consistently. 

All images are evaluated at an input size of **640 × 640** using a fixed resize policy (`<letterbox (keep aspect ratio) / direct resize>`) that is kept identical across all compared methods, and **no test-time augmentation (TTA)** is applied unless explicitly stated. 

Post-processing uses standard NMS with a confidence threshold of `<value or "Ultralytics default">`, an NMS IoU threshold of `<value or "Ultralytics default">`, and a maximum of `<value or "Ultralytics default">` detections per image. 

For reference and reproducibility, please record the exact inference stack used in your experiments (e.g., `<PyTorch version>`, `<CUDA version>`, and `<Ultralytics/YOLO version>` such as `ultralytics==x.y.z`). 

We report **mAP@0.5** (IoU = 0.5) and **mAP@0.5:0.95** (IoU = 0.50:0.05:0.95, COCO-style), and Precision/Recall should be computed under the same IoU criterion used for mAP reporting to avoid inconsistencies.

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

