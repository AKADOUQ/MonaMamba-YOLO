# MonaMamba-YOLO: Robust Dense Aluminum-Can Anomaly Detection under Industrial Scenario

This repository releases the **full dataset** for aluminum-can anomaly detection (YOLO-MAD), aiming to improve **transparency** and **reproducibility** under industrial scenario constraints.

- **Task:** single-class object detection  
- **Class:** `fallen can`

> **Availability statement.**  
> The **full dataset** is publicly available via the download link below.  
> The implementation is not publicly released due to factory privacy, contractual restrictions, and IP protection, and additional materials can be provided for research verification upon reasonable request.


---

## Data

The dataset is provided as a single archive (`download.zip`) containing images and YOLO-format labels. If you want to use the dataset released by this work, download the images and labels available [here](https://pan.baidu.com/s/1pIpsshS9onoC5QlZSiUEuw?pwd=5tey).

After downloading and unzipping `download.zip`, the extracted folder contains the images and labels:

<pre>
download/
├── images/          # images (.jpg)
└── labels/          # YOLO-format annotations (.txt)
</pre>

Image–label pairs are matched by the identical filename stem. For example:

<pre>
download/images/D01_xxx_00_00_00-00_05_00_3087.jpg
download/labels/D01_xxx_00_00_00-00_05_00_3087.txt
</pre>

Some filenames may include spaces; when scripting, wrap paths in quotes.

---

## Annotation Specification

This dataset uses a single detection class: `fallen can` (class_id = 0), defined as a can that has fallen over on the production line (abnormal target). Each label file `download/labels/<stem>.txt` contains 0 or more lines in the standard YOLO txt format:

<pre>
class_id  cx  cy  w  h
</pre>

Here `class_id` is an integer (only `0` in this dataset), and `cx, cy, w, h` are **normalized** to `[0, 1]` by image width/height. 

An empty label file indicates no fallen can; missing label files are not expected.

Bounding boxes should follow the **physical can body** rather than specular highlights alone; 
for partial occlusion, annotate the **visible extent**; 
for truncation and out-of-frame cases, annotate the visible part and keep the box within the image; 
for motion blur and glare, annotate only when the can boundary remains identifiable; 
if multiple fallen cans appear, annotate each instance separately.

---

## Evaluation Details

This section summarizes the evaluation protocol used in the manuscript so readers can interpret the reported results consistently. 

All images are evaluated at an input size of 640 × 640 using a fixed resize policy that preserves the original aspect ratio with padding, applied identically across all compared methods, and no test-time augmentation is used unless explicitly stated.

Post-processing uses standard NMS with the Ultralytics default validation settings (**conf=0.001**, **iou=0.7**, **max_det=300**). 

The experiments are conducted on Ubuntu 22.04 with **PyTorch 2.5.1** and **CUDA 12.4**. 

We report mAP@0.5 and mAP@0.5:0.95. Precision and Recall should be computed under the same IoU criterion used for mAP reporting to avoid inconsistencies.

---

## Citation

If you use this dataset, please cite:

MonaMamba-YOLO: Robust Dense Aluminum-Can Anomaly Detection under Industrial Scenario, IEEE Transactions on Industrial Informatics (under review).

---

## Contact

For questions or research verification requests, please contact the author at **qianwenjie@wust.edu.cn**.

