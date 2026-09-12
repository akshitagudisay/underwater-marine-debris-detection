 

## Current Status

Trained model checkpoint files (`.pt`) are **not included** in this repository.

The repository focuses on documenting the experimental workflow, including:

* Model training
* Test-set evaluation
* Model comparison
* Fine-tuning
* Architectural modifications

The trained weights remain external due to their file size and repository management considerations.

## Models Evaluated

The experiments compare the following YOLO architectures:

* YOLOv6s
* YOLOv7
* YOLOv8s
* YOLOv9s
* YOLOv10s
* YOLOv11n
* YOLOv11s
* YOLOv12n
* YOLOv12s

Additional experiments were performed using:

* YOLOv11n with fine-tuning
* YOLOv11n with architectural modifications

## YOLOv11 Architectural Experiments

The YOLOv11 experiments investigate modifications involving:

* C3TR
* SPPELAN
* C2fPSA
* C2fCIB + C3TR

These experiments were used to study the effect of different feature-extraction and attention mechanisms on underwater marine debris detection.

 

Model checkpoints are relatively large and are not required to understand or reproduce the documented experimental workflow.

 