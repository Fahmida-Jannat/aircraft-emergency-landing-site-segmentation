
# Aircraft Emergency Landing-Site Identification Using Semantic Segmentation

### Supervised and Self-Supervised Deep Learning Approaches

This research project explores **semantic segmentation of aerial imagery** to identify potential aircraft emergency landing regions. It compares fully supervised deep learning models with self-supervised learning (SSL) approaches to evaluate segmentation accuracy, label efficiency, and the potential for reducing manual annotation requirements.

## Project Objectives

- Identify potential landing-site regions through pixel-level segmentation.
- Compare supervised and self-supervised segmentation architectures.
- Evaluate performance using mIoU, Dice Score, and Pixel Accuracy.
- Investigate the effectiveness of SSL with limited labeled images.

## Dataset

**Dataset:** Moroccan Aircraft Emergency Landing Sites  
**Source:** [Mendeley Data](https://data.mendeley.com/datasets/jrh8jxwv2t/2)

| Property | Details |
|---|---|
| Total Images | 2,090 image–mask pairs |
| Resolution | 256 × 256 pixels |
| Classes | Background (0), Landing Site (1) |
| Training | 1,416 images |
| Validation | 314 images |
| Testing | 360 images |

Dataset preprocessing included image–mask validation, binary mask conversion, normalization, and training-only augmentation.

The dataset is available from its original source and is not redistributed in this repository.

## Methodology

The research is divided into two parts.

### Part A — Supervised Semantic Segmentation

Three models were trained using labeled aerial imagery:

- **DeepLabV3–ResNet50:** CNN-based segmentation with multi-scale feature extraction.
- **SegFormer-B0:** Transformer-based semantic segmentation.
- **YOLO26n-Sem:** Lightweight semantic segmentation architecture.

### Part B — Self-Supervised Semantic Segmentation

Four SSL approaches were investigated:

- **SimCLR:** Contrastive representation learning.
- **BYOL:** Self-supervised learning without negative pairs.
- **MAE:** Masked image reconstruction.
- **DINOv2:** Student–teacher self-distillation.

SSL models used **1,416 unlabeled images for pretraining** and **314 labeled images for downstream fine-tuning**.

## Experimental Results

| Model | Approach | mIoU | Mean Dice |
|---|---|---:|---:|
| **DeepLabV3–ResNet50** | Supervised | **0.8220** | 0.9011 |
| SegFormer-B0 | Supervised | 0.8154 | 0.8969 |
| YOLO26n-Sem | Supervised | 0.8041 | 0.8897 |
| **MAE** | Self-Supervised | **0.8055** | 0.8908 |
| SimCLR | Self-Supervised | 0.8018 | 0.8885 |
| DINOv2 | Self-Supervised | 0.7999 | 0.8874 |
| BYOL | Self-Supervised | 0.7843 | 0.8773 |

### Key Findings

- **Best supervised model:** DeepLabV3–ResNet50 (82.20% mIoU).
- **Best self-supervised model:** MAE (80.55% mIoU).
- **Label efficiency:** MAE retained **98.00% of the supervised baseline mIoU** while using **77.82% fewer labeled images**.

These results demonstrate the potential of SSL to reduce annotation requirements while maintaining competitive segmentation performance.

## Repository Structure

```text
aircraft-emergency-landing-site-segmentation/
│
├── README.md
│
├── code/
│   ├── PartA/
│   │   ├── EDA_and_Preprocessing.ipynb
│   │   ├── DeepLabV3.ipynb
│   │   ├── SegFormer_B0.ipynb
│   │   └── YOLO26_Semantic_Segmentation.ipynb
│   │
│   └── PartB/
│       ├── Data_Preparation.ipynb
│       ├── SimCLR.ipynb
│       ├── BYOL.ipynb
│       ├── MAE.ipynb
│       └── Final_Comparison.ipynb
│
└── reports/
    └── Research_Paper.pdf
```

*Note: The repository structure uses simplified notebook filenames. Rename your uploaded files accordingly. The paper also reports DINOv2 results, although its implementation notebook is not included in the available code.*

## Tools and Technologies

**Language:** Python  
**Frameworks:** PyTorch, Torchvision, Transformers  
**Libraries:** OpenCV, NumPy, Pandas, Scikit-learn, Matplotlib  
**Environment:** Kaggle Notebooks (GPU)

## Limitations

The models identify visual candidate regions rather than certifying landing safety. Operational factors such as terrain slope, obstacles, weather, and aircraft requirements are not evaluated. Additionally, the SSL experiments used the test set during checkpoint selection, so reported scores may be optimistic.


## Project Report

The complete project report presents the methodology, dataset preparation, model implementations, experimental results, performance comparisons, and error analysis conducted during this project.

📄 **[View Project Report](Report/Supervised_and_Self_Supervised_Semantic_Segmentation_for_Aircraft_Emergency_Landing_Site_Identification%20%286%29.pdf)**


## Project Contributors

**Fahmida Jannat**  
**Sumaiya Akter**  
**Nusrat Ahmed Sruti**

Department of Computer Science and Engineering  
East West University, Bangladesh

**Course:** CSE 438 — Digital Image Processing

## Conclusion

This project demonstrates that self-supervised learning can achieve competitive aerial semantic segmentation performance with substantially fewer labeled images. MAE emerged as the strongest SSL approach, highlighting its potential for annotation-efficient remote-sensing applications.
