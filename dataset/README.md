# Dataset

## SeaClear Marine Debris Detection & Segmentation Dataset

This project uses the **SeaClear Marine Debris Detection & Segmentation Dataset**, which contains **8,610 underwater images** annotated for object detection and instance segmentation.

The dataset was collected using **Remotely Operated Vehicles (ROVs)** during SeaClear field experiments across multiple locations:

* Bistrina, Croatia
* Jakljan, Croatia
* Lokrum, Croatia
* Slano, Croatia
* Marseille, France

All images are provided at **1920 × 1080** resolution.

**Dataset DOI:** [10.4121/4f1dff25-e157-4399-a5d4-478055461689.v1](https://doi.org/10.4121/4f1dff25-e157-4399-a5d4-478055461689.v1)

**License:** CC BY 4.0

---

## Original Dataset

The original SeaClear dataset contains **40 object categories**, covering marine litter as well as observed animals, plants, and robot parts.

The original annotations are provided in **COCO JSON format** and the images are organized into folders corresponding to individual site-camera pairs.

For this project, the dataset was prepared specifically for **YOLO-based object detection experiments**.

---

## Project Classes

For the experiments in this repository, the original categories were grouped into **12 classes** to create meaningful detection categories and reduce class imbalance.

| Class ID | Category      |
| -------: | ------------- |
|        0 | animal        |
|        1 | cement_clay   |
|        2 | ceramic       |
|        3 | fiber         |
|        4 | glass         |
|        5 | metal         |
|        6 | paper         |
|        7 | plastic       |
|        8 | rov_equipment |
|        9 | rubber        |
|       10 | unknown_misc  |
|       11 | wood          |

---

## Dataset Split

For the experiments, the prepared dataset was divided using a **60/20/20 split**:

| Split      |    Images | Purpose                          |
| ---------- | --------: | -------------------------------- |
| Train      |     5,166 | Model training                   |
| Validation |     1,722 | Model development and validation |
| Test       |     1,722 | Final held-out evaluation        |
| **Total**  | **8,610** |                                  |

The training data was additionally augmented wrt classes ,resulting to reduce class imbalance

---

## Annotation Conversion

The original dataset provides annotations in **COCO format**.

For the YOLO experiments, the annotations were converted to YOLO bounding-box format.

Each image is associated with a `.txt` label file containing:

```text
class_id x_center y_center width height
```

The bounding-box coordinates are normalized with respect to the image dimensions.

---

## Data Augmentation

Augmentation was applied to the training data to improve robustness to variations commonly encountered in underwater imagery.

The transformations included:

* Horizontal flipping
* Vertical flipping
* Small-angle rotation (e.g. ±15°)
* Brightness variation
* Contrast variation
* Shearing

The validation and test sets were not augmented.

---

## Dataset Structure

After preparation for the YOLO experiments, the expected directory structure is:

```text
dataset/
├── train/
│   ├── images/
│   └── labels/
│
├── val/
│   ├── images/
│   └── labels/
│
├── test/
│   ├── images/
│   └── labels/
│
└── data.yaml
```

The `data.yaml` file specifies the dataset paths, number of classes, and the 12 project class names.

---

## Dataset Availability

The original SeaClear dataset is **not included** in this GitHub repository.

The dataset can be obtained from its official repository using the DOI provided above.

The repository contains the project notebooks and documentation required to understand the dataset preparation and YOLO experiments.

---

 

## Citation

If using the original dataset, please cite the SeaClear Marine Debris Detection & Segmentation Dataset:

> Đuraš, A., Ilioudi, A., Wolf, B., Palunko, I., & De Schutter, B. *SeaClear Marine Debris Detection & Segmentation Dataset*. 4TU.ResearchData. DOI: 10.4121/4f1dff25-e157-4399-a5d4-478055461689.v1
