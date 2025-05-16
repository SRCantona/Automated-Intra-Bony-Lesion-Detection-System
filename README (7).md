# 🌟 LesionLens: Automated Detection of Intra-Bony Jaw Lesions

Welcome to **LesionLens**, an end-to-end AI pipeline that transforms panoramic dental X‑rays into actionable clinical insights—lightning-fast lesion detection powered by YOLOv11, seamless dataset management via Roboflow, and an intelligent AI agent for instant report generation.

---

## 🎯 Research Objectives
1. **Automate** localization and classification of intra-bony jaw lesions in panoramic radiographs.  
2. **Benchmark** YOLOv11 performance against expert radiologist annotations.  
3. **Streamline** clinical reporting via a generative AI agent.  
4. **Deploy** a lightweight inference service for real‑world dental workflows.

---

## 📂 Dataset
- **Source:** 3,315 panoramic radiographs curated from institutional archives.  
- **Annotations:** Expert-delineated bounding boxes for periapical and other intra‑bony lesions.  
- **Splits:** 70% train, 15% validation, 15% test.

---

## 🛠️ Roboflow Integration
We leverage Roboflow to:  
- Import raw images and metadata.  
- Standardize annotations (COCO/TXT).  
- Perform on‑the‑fly augmentations: random rotation, scaling, brightness shifts.  
- Export ready‑to‑train datasets at 640×640 px.

---

## 🔍 Model Selection
- **Base:** YOLOv11 (C3K2, SPPF, C2PSA modules)  
- **Backbone:** CSPDarknet with optimized depth and width scaling.  
- **Head:** Anchor‑based detection with multi‑scale feature fusion.

---

## 📊 Performance Metrics
- **mAP@0.5:** Mean Average Precision at IoU 0.5.  
- **mAP@0.5:0.95:** COCO-style averaged across IoU thresholds.  
- **Precision & Recall:** Lesion-specific classification performance.  
- **Sensitivity & Specificity:** Clinical reliability indicators.  
- **Inference Time:** Average detection latency per image.

---

## 🚀 Methodology
1. **Preprocessing**  
   - Grayscale conversion, histogram equalization.  
   - Resize to 640×640 px, normalize.
2. **Augmentation**  
   - Geometric: rotation (±15°), flips.  
   - Photometric: brightness/contrast jitter, Gaussian blur.
3. **Training**  
   - Optimizer: SGD (LR=0.01, momentum=0.9).  
   - Epochs: 150 with early stopping.  
   - Batch size: 16, mixed precision.
4. **Validation**  
   - Monitor mAP metrics, checkpoint best weights.
5. **Testing & Inference**  
   - Generate JSON detection outputs + annotated PNGs.

---

## 📈 Results
| Metric           | Validation | Test    |
|------------------|------------|---------|
| mAP@0.5          | 0.87       | 0.85    |
| mAP@0.5:0.95     | 0.65       | 0.63    |
| Precision        | 0.89       | 0.87    |
| Recall           | 0.84       | 0.82    |
| Sensitivity      | 0.91       | 0.89    |
| Specificity      | 0.88       | 0.86    |
| Avg. Inference   | 0.032 s    | 0.033 s |

*Our YOLOv11-based pipeline achieves radiologist-level accuracy with sub‑50 ms inference time per image.*

---

## 🤖 AI Agent for Automated Reporting
A custom generative AI agent consumes detection outputs to draft clinical reports:
- **Lesion Summary:** Locations, sizes, confidence scores.  
- **Diagnostic Insights:** Contextual interpretation based on lesion type.  
- **Recommendations:** Follow-up imaging, biopsy suggestions.  
- **Editable Draft:** Clinician can refine before sign‑off.

---

## 🗣️ Discussion & Limitations
- **Strengths:** High precision, rapid inference, seamless report automation.  
- **Limitations:**  
  - Challenged by extremely small/low-contrast lesions.  
  - Dataset bias toward certain demographics.  
  - Lack of multi-modal imaging (e.g., CBCT).  
- **Future Work:**  
  - Integrate 3D volumetric data.  
  - Expand to other dental pathologies (cysts, tumors).

---

## 🏗️ Project Structure
```
├── data/                      # Raw & processed images
│   ├── raw/
│   └── processed/
├── src/                       # Code
│   ├── model/                 # YOLOv11 scripts
│   ├── agent/                 # Reporting modules
│   └── utils/                 # Preprocess & eval
├── reports/                   # Documentation
├── presentations/             # Slide decks
└── README.md                  # 👉 You are here
```

---

## 🎬 Input & Output
- **Inputs:** PNG/JPEG radiographs.  
- **Outputs:**  
  - JSON detections + annotated images.  
  - CSV performance summary.  
  - Draft clinical report (DOCX).

---

## ⚙️ Usage
```bash
git clone …/LesionLens.git
conda env create -f environment.yml
conda activate lesionlens
# Train:
python src/model/train.py --data data/processed …
# Inference:
python src/model/infer.py …
# Generate Report:
python src/agent/report.py …
```

---

## 📦 Deliverables
- **Source Code** (YOLOv11 & agent).  
- **Draft & Final Reports** (`GP_final_draft.docx`, `Final_Report.pdf`).  
- **Research Paper** (`Research_Paper.pdf`).  
- **Presentations** (`Group4_YOLOv11.pptx`, `Defense_Slides.pptx`).

---

## 🙏 Acknowledgments
Supervised by **Dr. Mustafa Youldash**, supported by **IAU COD‑BDS**. Special thanks to all annotators and clinical experts.

*LesionLens — where AI meets dental diagnostics.*
