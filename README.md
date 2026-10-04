# Traffic Object Detection in Bangladeshi Roads Evaluating of Supervised, Semi-Supervised and Self-Supervised Learning

A Machine Learning project followed by **supervised, semi-supervised and self-supervised learning using YOLO-based detectors**.
This project explores how object-detection models perform on complex Bangladeshi traffic scenes and whether unlabeled images can help reduce dependence on manual bounding-box annotations.

## Project Overview

Traffic scenes in Bangladesh contain visually diverse road users including rickshaws, buses, trucks, motorcycles, CNGs, cycles, cars, and pedestrians. Detecting these objects reliably is useful for computer-vision research but fully labeling large traffic datasets is expensive. In this project, we investigate the effectiveness of semi-supervised and selfsupervised learning strategies for improving object detection performance under limited annotation settings on the Bangladeshi Traffic Flow Dataset.

This project was developed in two stages:

1. **Supervised object detection:** YOLOv10, YOLOv11 and YOLOv12 were trained and compared.
2. **Label-efficient learning:** the best detector from the first stage (here, it's YOLOv12) was used as the basis for:
   - **Pseudo-labeling** as the semi-supervised approach.
   - **SimCLR** and a **DINO-style teacher–student method** as self-supervised representation-learning experiments.

The goal was not simply to find a single "best" model. The project explored how different learning strategies behave on a Bangladeshi traffic dataset.

---

## Dataset

The project uses the **TFP-BD / Bangladeshi Traffic Flow Dataset** covering traffic scenes from four locations in Dhaka:
- Arambag
- Shapla Chattar
- Bashabo
- Abul Hotel

The Dataset consists of **23,678 images** images extracted from videos of these locations and nine traffic-related classes:
`Rickshaw`, `Bus`, `Truck`, `Bike`, `Mini-truck`, `People`, `Car`, `CNG`, and `Cycle`.
The original annotations were provided in **Pascal VOC XML** format and were converted to the YOLO annotation format for model training.

**Dataset Link:**
https://data.mendeley.com/datasets/h8bfgtdp2r/4

---

## Methodology
# Part 1 — Supervised Object Detection

The first stage required training three separate object detectors:
- YOLOv10
- YOLOv11
- YOLOv12

Then the experiments compare the models using standard object-detection metrics.

---

# Part 2 — Label-efficient learning

# Semi-Supervised Learning:

### Method: Pseudo-Labeling

The project uses **pseudo-labeling with YOLOv12**.
The general idea is:
1. Start from a trained detector/teacher model.
2. Use it to generate predictions on data treated as unlabeled.
3. Retain predictions according to the notebook's pseudo-labeling procedure.
4. Use those pseudo-labels together with labeled training data to train/evaluate the student detector.

The project therefore investigates whether automatically generated labels can provide useful additional supervision without manually labeling every image.

---

# Self-Supervised Representation Learning: 

This project explored:
1. **SimCLR**
2. **DINO-style teacher–student learning**

These experiments were intended to investigate whether representation learning without relying entirely on manual labels could provide useful features for downstream object detection.

## SimCLR

SimCLR learns representations by bringing augmented views of the same image closer in representation space while separating representations of different images.

## DINO-style learning

The project also implements a **DINO-style teacher–student self-supervised workflow** around the YOLOv12-family setup.
It is important to describe this accurately:
> This is a custom DINO-style teacher–student implementation used in the project. It should not be presented as the official DINOv2 implementation.

---

# Experimental Results

The original experiments produced multiple sets of metrics across the supervised, pseudo-labeling, SimCLR, and DINO-style workflows. Some notebook outputs that were directly inspected include:

| Experiment / Evaluation | mAP@0.5  | mAP@0.5:0.95 |
|-------------------------|---------:|-------------:|
| YOLOv10 test evaluation | 0.6398   |    0.4103    |
| YOLOv12 test evaluation | 0.6671   |    0.4278    |
| Pseudo-labeling teacher | 0.74985  |    0.51691   |
| Pseudo-labeling student | 0.74731  |    0.51672   |
| DINO-style evaluation*  | 0.7530   |    0.5125    |
| YOLOv11 test evaluation | 0.642    |   0.409      |

\*The DINO-style notebook evaluation was performed on a **4,735-image validation split**, so it should not be presented as directly equivalent to the 2,369-image test evaluations above.

---

# The Notebook's Links

The notebooks were developed around a **Kaggle GPU environment**.
Several notebooks use Kaggle-specific paths. Therefore, they are not guaranteed to run unchanged on a local machine.

YOLOv10: https://www.kaggle.com/code/rejaulkarimsohag/final-yolov10-cse475 

YOLOv11: https://www.kaggle.com/code/mdesrafilrahman/cse475-assignment01-group-no-i-yolo11 

YOLOv12: https://www.kaggle.com/code/limaprodhan/final-traffic-yolov12-cse475 

Pseudo-labeling: https://www.kaggle.com/code/esrafilrahman/cse475-pseudo-labeling-in-yolov12 

SimCLR + YOLOv12s: https://www.kaggle.com/code/mdesrafilrahman/cse475-simclr-with-yolo12 

DINO-style + YOLOv12s: https://www.kaggle.com/code/limaprodhan/ssl-dino-with-yolov12s 

---

# Limitations

- The DINO implementation is a project-specific DINO-style workflow.
- The project does not claim production-level reliability or safety for real-world traffic systems.

---

# What We learned

Through this project, we gained practical experience with:
- Object detection using modern YOLO architectures.
- Dataset preparation and annotation conversion.
- Training and evaluating detection models.
- mAP, precision, recall, and related evaluation metrics.
- Semi-supervised learning through pseudo-label generation.
- Self-supervised representation learning.
- SimCLR-style contrastive learning.
- DINO-style teacher–student learning.
- Kaggle GPU experimentation.
- Comparing experimental results and identifying reproducibility issues.
- Presenting machine-learning experiments honestly when different evaluation runs produce different results.

---

# Team

1. Lima Prodhan 
2. Md. Esrafil Rahman
3. Rejaul Karim Sohag

**East West University | CSE475 Machine Learning**

---
