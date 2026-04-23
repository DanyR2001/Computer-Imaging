# Computational Imaging Project — Motion Deblur & Denoising

## Overview
This project addresses an inverse problem in computational imaging: reconstructing high-quality images from degraded observations affected by motion blur and noise.

We compare **classical**, **deep learning**, and **generative approaches** under the same experimental conditions, with the goal of analyzing their strengths and limitations.

---

## Task Definition
Given a clean image \( x \), we generate a degraded observation \( y \):

\[
y = Kx + n
\]

where:
- \( K \): motion blur operator
- \( n \): additive Gaussian noise

### Degradation parameters:
- Kernel size: **9**
- Motion angle: *(chosen experimentally)*
- Noise levels: **0.005, 0.01, 0.05, 0.1**

All methods are evaluated on the **same degraded inputs**.

---

## Dataset

Dataset used: **FFHQ 256x256**

🔗 https://huggingface.co/datasets/bitmind/ffhq-256

### Preprocessing:
- Resize to **256×256**
- Normalize pixel values to **[0,1]**
- Train / Validation / Test split
- Synthetic degradation generation

All preprocessing choices are documented and reproducible.

---

## Methods

We implement and compare four methodological families:

### 1. Variational Method
- **Total p-Variation (TpV)**
- \( p \in (0.1, 0.5) \)
- Optimization-based reconstruction

---

### 2. End-to-End Deep Learning
- Architecture: *(e.g. UNet / NAFNet / ViT)*
- Supervised training on degraded → clean pairs
- Loss functions: L1 / L2 / perceptual (optional)

---

### 3. Generative Method
- **Diffusion Posterior Sampling (DPS)**
- Adapted for inverse problems
- Combines diffusion priors with data consistency

---

### 4. Hybrid Method
- **Plug-and-Play (PnP) with HQS**
- Iterative reconstruction:
  - Data fidelity step
  - Denoising step using pretrained model

---

## Evaluation

We compare all methods using:

### Quantitative metrics:
- **PSNR**
- **SSIM**

### Qualitative analysis:
- Visual comparison of reconstructed images
- Artifact inspection
- Robustness to noise levels

---

## Results

- Comparative plots across all methods
- Performance vs noise level
- Trade-offs:
  - accuracy
  - speed
  - stability

---

## Project Structure
```
├── data/ # dataset and preprocessing
├── degradation/ # blur + noise simulation
├── variational/ # TpV implementation
├── models/ # deep learning architectures
├── diffusion/ # DPS implementation
├── pnp/ # Plug-and-Play HQS
├── evaluation/ # PSNR, SSIM, plots
├── notebooks/ # experiments and visualization
├── utils/ # helper functions
└── main.py
```

## 🚀 How to Run

### 1. Clone repository
```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install dependencies

pip install -r requirements.txt

### 3. Download dataset

Follow instructions from:
https://huggingface.co/datasets/bitmind/ffhq-256

### 4. Run experiments

python main.py --method unet
python main.py --method tpv
python main.py --method dps
python main.py --method pnp

# Parameter Selection

Parameters are chosen heuristically, including:

Regularization weight (TpV)
Network architecture and training setup
Number of diffusion steps (DPS)
HQS iteration parameters

A detailed discussion is provided in the report and presentation.
