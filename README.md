# Underwater Marine Debris Detection

An underwater object-detection study for identifying and classifying marine debris using multiple YOLO architectures.

The project investigates object detection under challenging underwater conditions including **turbidity, low contrast, occlusion, illumination variation, and complex backgrounds**.

The experiments progress from **YOLO baseline comparison** to **YOLOv11 fine-tuning and architectural experimentation**.

---

## Overview

Marine debris detection is challenging because underwater imagery often contains reduced visibility, background clutter, object deformation, and small or partially occluded objects.

This project uses an underwater marine debris dataset containing **8,610 annotated images captured using ROVs** and evaluates multiple YOLO architectures.

The study consists of:

1. Baseline comparison of YOLO architectures trained from scratch
2. YOLOv11 fine-tuning under different training conditions
3. YOLOv11 architectural modifications
4. Comparison using standard object-detection metrics

Dataset preparation and model-weight information are documented separately in [`dataset/`](dataset/) and [`models/`](models/).

---

## Experimental Workflow

```text
Marine Debris Dataset
        │
        ▼
Dataset Preparation
        │
        ▼
Train / Validation / Test
        │
        ▼
Data Augmentation
        │
        ▼
YOLO Baseline Models
        │
        ▼
Training from Scratch
        │
        ▼
Held-out Test Evaluation
        │
        ▼
Baseline Comparison
        │
        ▼
YOLOv11 Selection
        │
        ▼
Fine-tuning
        │
        ▼
Architectural Modifications
        │
        ▼
Final Comparison
```

---

# Baseline Experiments

The following YOLO architectures were trained from scratch without pretrained weights:

* YOLOv6s
* YOLOv8s
* YOLOv9s
* YOLOv10s
* YOLOv11n
* YOLOv11s
* YOLOv12n
* YOLOv12s

### Baseline Results

| Model    |  Precision |     Recall |         F1 |     mAP@50 |  mAP@50–95 |
| -------- | ---------: | ---------: | ---------: | ---------: | ---------: |
| YOLOv10s |     0.4527 |     0.5570 | **0.4994** |     0.4455 |     0.3396 |
| YOLOv11n | **0.4705** |     0.5195 |     0.4938 | **0.4664** |     0.3389 |
| YOLOv12n |     0.3225 |     0.4056 |     0.4420 |     0.2949 |     0.2111 |
| YOLOv6s  |     0.3684 |     0.4137 |     0.3895 |     0.3492 |     0.2410 |
| YOLOv8s  |     0.4262 | **0.5613** |     0.4845 |     0.4492 |     0.3291 |
| YOLOv9s  |     0.4369 |     0.4779 |     0.4565 |     0.4108 |     0.2947 |
| YOLOv11s |     0.4473 |     0.5081 |     0.4760 |     0.4374 |     0.3196 |
| YOLOv12s |     0.3408 |     0.4081 |     0.3716 |     0.4672 | **0.3443** |

### Baseline Observations

* **YOLOv8s** achieved the highest recall.
* **YOLOv11n** achieved the highest precision.
* **YOLOv10s** provided a strong overall balance across the evaluated metrics.
* **YOLOv12s** achieved the highest mAP@50–95 despite lower precision, recall, and F1.
* **YOLOv11n** was selected as the base architecture for subsequent experimentation.

---

# YOLOv11 Fine-Tuning

YOLOv11n was evaluated under different training conditions to investigate the effect of augmentation and fine-tuning.

| Training Condition     | Precision |     Recall |         F1 |     mAP@50 |  mAP@50–95 |
| ---------------------- | --------: | ---------: | ---------: | ---------: | ---------: |
| Scratch + Augmentation |    0.4705 |     0.5195 |     0.4938 |     0.4664 |     0.3389 |
| Without Augmentation   |    0.5472 |     0.2620 |     0.3544 |     0.2767 |     0.1767 |
| Fine-tuned             |    0.4459 | **0.5984** | **0.5110** | **0.4672** | **0.3443** |

The fine-tuned model achieved the highest recall and F1 score among the evaluated YOLOv11 configurations, while also improving mAP@50 and mAP@50–95 over the scratch-trained baseline.

---

# Architectural Experiments

The YOLOv11n architecture was further modified to investigate different feature-extraction and attention mechanisms.

The evaluated variants were:

* YOLOv11n + C3TR
* YOLOv11n + SPPELAN
* YOLOv11n + C2fPSA
* YOLOv11n + C2fCIB + C3TR

### Results

| Model                        |     mAP@50 | mAP@50–95 |  Precision |     Recall |         F1 |
| ---------------------------- | ---------: | --------: | ---------: | ---------: | ---------: |
| YOLOv11n + C3TR              |     0.4544 |    0.3390 |     0.4314 |     0.5230 |     0.4730 |
| YOLOv11n + SPPELAN           |     0.4432 |    0.3133 |     0.4238 |     0.5340 |     0.4726 |
| **YOLOv11n + C2fCIB + C3TR** | **0.4567** |    0.3240 |     0.4436 | **0.5422** | **0.4880** |
| YOLOv11n + C2fPSA            |     0.4416 |    0.3126 | **0.4584** |     0.5100 |     0.4828 |

The **C2fCIB + C3TR hybrid** achieved the highest mAP@50, recall, and F1 among the architectural variants evaluated.

---

# Evaluation

The models are compared using:

* Precision
* Recall
* F1 score
* mAP@50
* mAP@50–95

Training runs additionally monitor **box loss, classification loss, and DFL** to examine optimization and convergence.

The test split is kept separate from training and validation and is used for final quantitative evaluation.

---

# Repository Structure

```text
underwater-marine-debris-detection/
│
├── README.md
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── YOLOv6.ipynb
│   ├── YOLOv7.ipynb
│   ├── YOLOv8.ipynb
│   ├── YOLOv9.ipynb
│   ├── YOLOv10.ipynb
│   ├── YOLOv11.ipynb
│   ├── YOLOv11-finetune.ipynb
│   └── YOLOv12.ipynb
│
├── models/
│   └── README.md
│
└── dataset/
    └── README.md
```

The notebooks contain the training and evaluation workflows used in the experiments.

---

# Reproducibility

The repository does not include the complete dataset or trained model weights.

Dataset setup, annotation format, class information, and augmentation details are documented in [`dataset/README.md`](dataset/README.md).

Model-weight information is documented in [`models/README.md`](models/README.md).

Dataset paths used in the original notebook environment may need to be updated before reproducing the experiments.

---

# Project Status

**Version 1 — Experimental Research Repository**

Current scope:

* Underwater marine-debris detection
* Multi-model YOLO comparison
* Test-set evaluation
* YOLOv11 fine-tuning
* Architectural experimentation

### Future Work

* Underwater image enhancement
* Systematic error analysis
* Model compression
* ONNX/TensorRT export
* Edge deployment on embedded GPUs
* ROV/AUV integration
* Multi-modal optical and sonar perception

---

## Conclusion

This project investigates the effect of **architecture, augmentation, fine-tuning, attention mechanisms, and feature-fusion strategies** on underwater marine-debris detection.

The experiments progress from broad YOLO model comparison to focused YOLOv11 experimentation, with the **C2fCIB + C3TR hybrid** showing the strongest performance among the tested architectural variants.

The longer-term direction is a lightweight and robust detector suitable for future deployment in underwater robotic platforms.
