# Sketch-to-Image Translation: Pix2Pix vs. Stable Diffusion

![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

## 🚀 Overview

This project investigates translating freehand sketches into realistic images using state-of-the-art generative models. We compare the performance of **Pix2Pix** (a GAN-based model) and **Stable Diffusion + ControlNet** (a diffusion-based model) on sketch-to-photo translation tasks.

**Key highlights:**
- Two parallel pipelines: Pix2Pix (Conditional GAN) and Stable Diffusion v1.5 with ControlNet.
- Dataset: Sketchy Dataset (~25k photos, ~450k sketches).
- Evaluation using PSNR, SSIM, and FID for both quality and faithfulness metrics.

---

## 🖼️ Problem Statement

Translating sparse and noisy sketches into photorealistic images is a challenging task due to:
- Incomplete input (missing textures, details)
- Diverse photo domains and categories
- Ambiguities in freehand drawings

---

## 🔬 Methods

### 1️⃣ Pix2Pix Pipeline
- **Architecture:** U-Net generator + PatchGAN discriminator
- **Loss:** Conditional GAN loss + L1 reconstruction
- **Input:** Paired sketch-photo samples
- **Preprocessing:** Bounding box cropping, category normalization, sketch cleaning

### 2️⃣ Stable Diffusion + ControlNet Pipeline
- **Base Model:** Stable Diffusion v1.5
- **Guidance:** ControlNet using Canny/sketch conditioning
- **Input:** Freehand sketches with enhanced edge detection
- **Strengths:** High photorealism, flexible domain adaptation

---

## 🗂️ Dataset

- **Dataset:** [Sketchy Database](http://sketchy.database) (used ~25,000 photos and ~450,000 sketches)
- **Preprocessing:**
    - Cropped using per-image bounding boxes (from `stats.csv`)
    - Filtered out ambiguous or incorrect sketches
    - Normalized pairs (sketch/photo) per category to enhance training stability

---

## 📊 Evaluation Metrics

We use **standard metrics** to evaluate generated images:
- **PSNR (Peak Signal-to-Noise Ratio)**
- **SSIM (Structural Similarity Index)**
- **FID (Fréchet Inception Distance)**

Example results:
| Metric   | Pix2Pix | Stable Diffusion |
|----------|---------|------------------|
| FID      | ~245    | ~190             |
| Notes    | More faithful to sketches | More photorealistic |

---

## 📈 Results

- **Pix2Pix:** 
    - Pros: Strong alignment with sketch structure
    - Cons: Images often appear synthetic
- **Stable Diffusion:**
    - Pros: Excellent photorealism
    - Cons: Sometimes ignores precise sketch structure

See the `notebooks/` directory for visual comparisons and full metric reports.

---

## ✅ Requirements

- Python 3.8+
- Key libraries:
    - PyTorch
    - Diffusers (Hugging Face)
    - ControlNet
    - OpenCV, Matplotlib, Scikit-learn

---

## 🛠️ Usage

1️⃣ **Clone the repository:**

```bash
git clone https://github.com/AnakinHuang/translate_sketches_to_realistic_images_via_pix2pix_and_stable_diffusion.git
cd translate_sketches_to_realistic_images_via_pix2pix_and_stable_diffusion
```

2️⃣ **Install dependencies:**

```bash
pip install -r requirements.txt
```

3️⃣ **Run the pipeline:**

- Pix2Pix training:
    ```bash
    python train_pix2pix.py
    ```

- Stable Diffusion inference:
    ```bash
    python infer_stable_diffusion.py --input sketches/
    ```

---

## 📂 Repository Structure

```
├── data/                  # Dataset folder (not included)
├── notebooks/             # Jupyter notebooks for experiments & evaluation
├── models/                # Saved models/checkpoints
├── src/
│   ├── pix2pix/           # Pix2Pix implementation
│   ├── stable_diffusion/  # Stable Diffusion + ControlNet implementation
├── requirements.txt
└── README.md
```

---

## 👥 Contributors

- **Yuesong Huang**
- **Zijian Gu**

---

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file for details.

---
