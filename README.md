# DAU-Net: Dual Attention-aided U-Net for Tumor Segmentation in Breast Ultrasound Images

This project is a faithful reproduction of the paper:  
**“Dual attention-aided U-Net for segmenting tumor in breast ultrasound images”**  
Published in *PLOS ONE, 2024* by Prof. Ram Sarkar and team.

## 📌 Objective

To implement and evaluate the DAU-Net architecture for tumor segmentation using the BUSI dataset. The model integrates:
- Residual U-Net backbone
- Dual Attention Mechanism (CBAM + PAM = PCBAM)
- Shifted Window Attention (SWA) at the bottleneck

---

## 📚 Paper Reference

> Sarkar R., et al. (2024). *Dual attention-aided U-Net for segmenting tumor in breast ultrasound images*. PLOS ONE.  
[Link to paper (PDF)](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0303670)

---

## 🧠 Architecture Overview

### 🔹 Base: Residual U-Net  
Skip-connected convolution blocks with residual links.

### 🔹 Attention Modules:
- **CBAM (Convolutional Block Attention Module)** — channel + spatial attention
- **PAM (Positional Attention Module)** — dot-product-based attention across spatial dimensions
- **PCBAM** = CBAM + PAM

### 🔹 SWA:
Shifted Window Attention applied at the bottleneck to capture long-range dependencies.

---

## 🗂 Dataset

**Breast Ultrasound Images Dataset (BUSI)**  
- Source: [Kaggle - BUSI Dataset](https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset)
- Classes: Benign, Malignant, Normal
- Each image includes a corresponding segmentation mask (`_mask.png`)

### Preprocessing:
- Grayscale normalization (0–1)
- Resized to **128x128**
- Ground truth masks binarized (0 or 1)
- Split: 70% train, 10% val, 20% test

---

## 🛠️ Model Configuration

| Setting            | Value                |
|--------------------|----------------------|
| Input size         | 128x128x1            |
| Optimizer          | Adam                 |
| Learning rate      | 1e-4                 |
| Loss               | BCE + Dice           |
| Batch size         | 2 (due to Colab GPU) |
| Epochs             | 10                   |

---

## 📈 Results

### ✅ Training & Evaluation

| Metric           | Original Paper | Our Reproduction |
|------------------|----------------|------------------|
| Accuracy         | 94.27%         | **93.67%**       |
| Dice Coefficient | 93.11%         | ~**81%**         |
| Validation Acc.  | ~95%           | **95.13%**       |
| Test Loss        | ~0.65          | **0.8090**       |

> ⚠️ Note: The original paper trained for 200 epochs with batch size 16.  
> I used 10 epochs with batch size 2 due to Colab memory constraints.

---
