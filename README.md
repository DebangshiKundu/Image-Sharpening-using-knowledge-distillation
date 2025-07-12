#  Image Sharpness Enhancement using Knowledge Distillation

##  Overview

This project tackles the challenge of restoring image clarity in low-quality images—such as those seen during video conferencing or low-bandwidth streaming—by leveraging deep learning. A high-capacity **Teacher Model** (ResNet-based) is trained to learn fine-grained features, while a lightweight **Student Model** is distilled from it to enable faster inference with comparable quality.

The goal is to enhance the **perceived sharpness and visual fidelity** of blurry or low-resolution input images while maintaining real-time performance capabilities.

---

##  Objectives

- Improve the sharpness of low-resolution images.
- Leverage **knowledge distillation** to compress a high-performance model into a smaller one.
- Evaluate image quality using **SSIM** and **PSNR**.
- Enable a lightweight model to operate in constrained environments (e.g., edge devices).

---

## Solution Design
1. Data Preprocessing
We use the DIV2K Dataset for high-quality image samples. The pipeline:

Crops each image into multiple 128x128 patches.

Downsamples patches to simulate blur (using bicubic interpolation).

Upsamples them back to original resolution to simulate real-world LR inputs.

Generates paired Low-Resolution (LR) and High-Resolution (HR) data for supervised learning.

---

2. Model Architecture
Teacher Model (ResNet18-based)
A pretrained ResNet18 is modified to output enhanced RGB images from LR input by using a custom decoder after the backbone.

Student Model (Lightweight CNN)
A much simpler CNN that mimics the output of the teacher model while being efficient.

---

3. Knowledge Distillation
First, the Teacher is trained using LR-HR image pairs with MSE loss.

Then, the Student learns from the teacher's predictions (not the ground truth) using distillation loss.

---

 
4. Evaluation Metrics
SSIM (Structural Similarity Index): Measures structural similarity between images.

PSNR (Peak Signal-to-Noise Ratio): Quantifies reconstruction quality.


