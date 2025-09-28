---
title: "MOT-TR: DETR Fine-Tuning for Moved-Object Detection"
excerpt: "Robust, reproducible pipeline designed to fine-tune the DETR (DEtection TRansformer) model for the task of detecting moved objects in pairs of images taking from parking lots and intersections (VIRAT dataset)."
collection: portfolio
---
## Overview

MOT-TR is a robust, reproducible pipeline designed to fine-tune the DETR (DEtection TRansformer) model for the task of detecting moved objects in pairs of images. Instead of treating object detection as a static problem, the project focuses on *scene-change analysis* — identifying objects that have been displaced between a “before” and “after” view.  

The pipeline spans dataset construction, preprocessing, model adaptation, staged training, evaluation, and analysis. It combines PyTorch, Hugging Face Transformers, and Torchvision to deliver an end-to-end workflow that is both modular and easy to reproduce. You can build custom datasets, configure training via a simple config file, and produce detailed quantitative and qualitative results.

---

## Dataset & Preprocessing

- **Data organisation:** Raw images are stored in `data/base/cv_data_hw2/data/`, while bounding-box annotations live in `data/matched_annotations/`. Each annotation file encodes one object per line as:  `<class_id><x_center><y_center><width><height>`

All coordinates are normalised relative to image dimensions.

- **Image diff strategy:** To highlight movement, the pipeline computes the pixel-wise difference between the “before” and “after” images and feeds this diff through a pre-trained image processor. This emphasises scene changes and proved more effective than feature-level diffs.
- **Custom dataset class:** The `MovedObjectDataset` class handles image-annotation pairing, applies diff preprocessing, and integrates with Hugging Face’s image processor. The dataset is split into training and validation sets with fixed seeds for reproducibility.

---

## Model Architecture & Training

- **Model:** Fine-tunes `facebook/detr-resnet-50`, adapting its classification head to the number of custom classes. Transfer learning leverages pre-trained visual and spatial features.
- **Training strategies:**  
  - Train only the classification head (20 epochs).  
  - Unfreeze all layers and reduce the learning rate.  
  - Continue staged training with progressively smaller learning rates.  
- **Techniques:**  
  - Gradient accumulation to simulate larger batch sizes on limited GPUs.  
  - Cosine learning-rate schedule with restarts for better convergence.  
- **Hyperparameters:** Configurable via `code/config.py`. A typical run uses:  
  - Raw batch size: 2 (for a Tesla T4 GPU)  
  - Accumulation steps: 16 (effective batch size 32)  
  - Cosine-with-restarts scheduler  
  - ~80 epochs of training  
- **Logging & monitoring:** Metrics (loss, precision, recall, F1) logged via TensorBoard. The best model is automatically checkpointed.

---

## Evaluation & Results

**Quantitative metrics:**  

- Stage 1: Eval loss ≈ 2.38  
- Stage 2: Eval loss ≈ 1.62  
- Stage 3: Eval loss ≈ 0.60  
This shows a three-fold improvement with staged unfreezing and careful LR tuning.  
- **Qualitative analysis:** Visualisations overlay predicted bounding boxes on diff images. Successes show accurate moved-object detection, while common failures include excessive differences from camera movement and missed detections from limited training data.

---

## Key Contributions

- **End-to-end pipeline:** Includes ground-truth annotation tools, custom dataloaders, preprocessing with image diffs, model adaptation, staged training, and evaluation.  
- **Performance gains:** Reduced eval loss from 2.38 to 0.60, stabilising convergence on a small dataset.  
- **Reproducibility:** Fixed random seeds, modular configs, clear directory structure, and automated logging/checkpointing.

---

## Lessons Learned & Future Work

This project underscored the importance of:  

- Thoughtful preprocessing (image diffs matter).  
- Careful learning-rate tuning.  
- Staged training strategies for small datasets.  

**Future directions:**  

- Data augmentation (geometric + photometric).  
- Hyperparameter optimisation (Optuna, Ray Tune).  
- Advanced evaluation metrics (mAP).  
- Camera-motion compensation to reduce false positives.  

---

📄 [Full Technical Report and Code available at](https://github.com/prasadboi/MOT-TR/blob/main)
