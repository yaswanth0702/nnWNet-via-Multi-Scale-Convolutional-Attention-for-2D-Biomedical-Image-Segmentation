# Enhancing Local Feature Modeling in nnWNet via Multi-Scale Convolutional Attention for 2D Biomedical Image Segmentation

> **Missouri University of Science and Technology**  
> Yaswanth Podapati (ypfg3@mst.edu) 

---

## 📌 Abstract

Biomedical image segmentation is a fundamental task in medical image analysis, used in lesion detection, vessel extraction, and computer-aided diagnosis. This project enhances the **nnWNet** architecture (CVPR 2025) by integrating a **Multi-Scale Convolutional Attention (MSCA)** module into its Local Scope Blocks (LSBs), significantly improving accuracy for thin vessels and complex lesion boundaries on 2D biomedical datasets.

---

## 🏗️ Architecture

### nnWNet Overview
The nnWNet architecture combines:
- **LSB (Local Scope Block)** – Convolutional residual blocks for local feature extraction
- **GSB (Global Scope Bridge)** – Transformer-based modules for global context modeling
- **OPE (Overlapping Patch Embedding)** – For hierarchical feature extraction

### Proposed Enhancement – MSCA Module
The MSCA module uses **parallel depthwise convolutions** with kernel sizes **7×7, 11×11, and 15×15** to capture spatial features at multiple scales:
- Small kernels → fine structures (thin vessels)
- Medium kernels → intermediate patterns
- Large kernels → broader regions (lesion boundaries)

The outputs are concatenated and projected via a **1×1 convolution** to generate an attention map, applied as:

```
Fout = Fin + MSCA(Flocal)
```

---

## 📁 Repository Structure

```
├── Datasets/                        # Dataset download instructions
├── Results/                         # Quantitative & qualitative results
│   ├── DRIVE/                       # DRIVE dataset results
│   │   ├── training_curves/         # Loss, Dice, IoU, Accuracy plots
│   │   └── segmentation_outputs/    # Visual predictions
│   └── ISIC_2017/                   # ISIC-2017 dataset results
│       ├── training_curves/         # Loss, Dice, IoU plots
│       └── segmentation_outputs/    # Visual predictions
├── Drive_nnWNet.ipynb               # nnWNet on DRIVE dataset
├── Drive_nnWNet+MSCA.ipynb          # nnWNet + MSCA on DRIVE dataset
├── Drive_unet.ipynb                 # U-Net baseline on DRIVE dataset
├── ISIC_2017_nnwnet.ipynb           # nnWNet on ISIC-2017 dataset
├── ISIC_2017_nnwnet+msca.ipynb      # nnWNet + MSCA on ISIC-2017 dataset
├── ISIC_2017_unet.ipynb             # U-Net baseline on ISIC-2017 dataset
└── README.md
```

---

## 📊 Datasets

See the [`Datasets`](./Datasets) file for download instructions.

| Dataset | Task | Images | Notes |
|---------|------|--------|-------|
| **DRIVE** | Retinal Vessel Segmentation | 40 fundus images | Thin & branching vessel structures |
| **ISIC-2017** | Skin Lesion Segmentation | 2000+ dermoscopic images | Irregular shapes & unclear boundaries |

---

## ⚙️ Implementation Details

| Setting | Value |
|---------|-------|
| Framework | PyTorch |
| Image Size | 256 × 256 |
| Optimizer | Adam |
| Learning Rate | 1e-4 |
| Epochs | 50 |
| Batch Size | 8 |
| Loss Function | BCE Loss + Dice Loss |
| Preprocessing (DRIVE) | CLAHE enhancement + Normalization |
| Preprocessing (ISIC) | Normalization |

---

## 📈 Experimental Results

### DRIVE Dataset

| Model | Dice | IoU | Accuracy | Precision | Recall |
|-------|------|-----|----------|-----------|--------|
| U-Net | 0.79 | 0.66 | 0.91 | 0.75 | 0.84 |
| nnWNet | 0.76 | 0.61 | 0.94 | 0.75 | 0.77 |
| **nnWNet + MSCA** | **0.77** | **0.63** | **0.95** | **0.80** | 0.75 |

### ISIC-2017 Dataset

| Model | Dice | IoU | Accuracy | 95HD | ASD |
|-------|------|-----|----------|------|-----|
| U-Net | 0.65 | 0.54 | 0.91 | 33.23 | 16.46 |
| nnWNet | 0.62 | 0.49 | 0.91 | 43.23 | 19.71 |
| **nnWNet + MSCA** | **0.73** | **0.63** | **0.92** | **37.70** | **14.46** |

> nnWNet + MSCA achieves the best performance on both datasets, with especially notable improvements on ISIC-2017 boundary metrics (95HD and ASD).

---

## 🚀 How to Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/yaswanth0702/nnWNet-via-Multi-Scale-Convolutional-Attention-for-2D-Biomedical-Image-Segmentation.git
   cd nnWNet-via-Multi-Scale-Convolutional-Attention-for-2D-Biomedical-Image-Segmentation
   ```

2. **Download datasets** – follow instructions in the [`Datasets`](./Datasets) file.

3. **Open the relevant notebook in Google Colab:**

   | Notebook | Purpose |
   |----------|---------|
   | `Drive_nnWNet+MSCA.ipynb` | Main model on DRIVE |
   | `ISIC_2017_nnwnet+msca.ipynb` | Main model on ISIC-2017 |
   | `Drive_unet.ipynb` | U-Net baseline on DRIVE |
   | `ISIC_2017_unet.ipynb` | U-Net baseline on ISIC-2017 |

4. **Install dependencies:**
   ```bash
   pip install torch torchvision numpy matplotlib scikit-learn opencv-python
   ```

5. Set your dataset path inside the notebook and **Run All**.

---

## 🔍 Key Contributions

- Integration of **MSCA** into nnWNet's Local Scope Blocks for improved multi-scale spatial modeling
- Better **boundary localization** (lower 95HD and ASD on ISIC-2017)
- Improved **thin structure detection** (higher Precision on DRIVE)
- Maintained **computational efficiency** without major overhead
- Comprehensive evaluation on DRIVE and ISIC-2017 benchmarks

---

## 📄 Base Paper

> **nnWNet: Rethinking the Use of Transformers in Biomedical Image Segmentation and Calling for a Unified Evaluation Benchmark**  
> CVPR 2025 — Y. Zhou et al.

---

## 📚 References

Key references used in this project:
- nnU-Net (Isensee et al., Nature Methods 2021)
- nnWNet (Zhou et al., CVPR 2025)
- Vision Transformer / ViT (Dosovitskiy et al., ICLR 2021)
- Swin Transformer (Liu et al., ICCV 2021)
- Visual Attention Network (Guo et al., arXiv 2022)
- ISIC 2017 Challenge Dataset (Codella et al., arXiv 2017)

---

## 👥 Authors

| Name | Institution | Email |
|------|-------------|-------|
| Yaswanth Podapati | Missouri S&T | ypfg3@mst.edu |
| Chandramurugan | Missouri S&T | ckgky@mst.edu |

---

## 📄 License

This project is developed for academic research purposes at Missouri University of Science and Technology.
