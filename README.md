# ER-Hybrid-A-Dual-Stage-Model-for-Morphology-Aware-ER-Scoring-in-Histopathology

🎯 Project Objective
To build a system capable of:
1. Segmenting histological regions into ER expression categories.
2. Classifying whole regions based on the dominant intensity levels.

| Class ID | ER Expression | RGB Color     |
| -------- | ------------- | ------------- |
| 0        | Background    | (0, 0, 0)     |
| 1        | Normal        | (0, 159, 255) |
| 2        | Weak          | (0, 255, 0)   |
| 3        | Moderate      | (255, 216, 0) |
| 4        | Strong        | (255, 0, 0)   |


🧬 Pipeline Overview
🧩 Stage 1: Morphology Segmentation
-Model: UNet++ (Nested U-Net)
-Library: segmentation-models-pytorch
-Input: RGB histology images
-Output: Multi-class segmentation mask (ER expression regions)


![download](https://github.com/user-attachments/assets/178b9a30-b823-486d-9b0d-d76c54b789d1)


🔍 Stage 2: Patch-Based Classification
Architecture: Custom CNN (with residual blocks)
-Input: Segmented patches
-Output: Predicted dominant ER class (Normal, Weak, Moderate, Strong)

| Layer        | Description                  |
| ------------ | ---------------------------- |
| Conv2D       | Initial 3×3 conv block       |
| Residual x3  | Stacked feature extractors   |
| AdaptivePool | Global pooling               |
| FC Layer     | Final classifier (4 classes) |


🔢 Dataset Information
| Folder     | Contents              | Shape         |
| ---------- | --------------------- | ------------- |
| `/images/` | IHC RGB tissue slides | 256×256       |
| `/masks/`  | Annotated color masks | 256×256 (RGB) |

Both datasets are paired and transformed using albumentations with horizontal flips, color jittering, and normalization.


📊 Results Summary
🔹 Segmentation Accuracy
| Metric         | Value |
| -------------- | ----- |
| Pixel Accuracy | 91.6% |
| mIoU           | 0.88  |
| Dice Score     | 0.91  |


🔹 Classification Report
| Class    | Precision | Recall | F1-Score |
| -------- | --------- | ------ | -------- |
| Normal   | 0.93      | 0.90   | 0.91     |
| Weak     | 0.88      | 0.87   | 0.87     |
| Moderate | 0.91      | 0.89   | 0.90     |
| Strong   | 0.94      | 0.92   | 0.93     |


🧠 Why a Hybrid Approach?
| Feature                | Traditional Pipeline | ER-Hybrid |
| ---------------------- | -------------------- | --------- |
| End-to-End Scoring     | ❌                    | ✅         |
| Morphology Awareness   | ❌                    | ✅         |
| Patch Interpretability | ❌                    | ✅         |
| Segmentation + Class   | ❌                    | ✅         |


![image](https://github.com/user-attachments/assets/2765c15f-0809-4e0b-956f-f50172d91253)











