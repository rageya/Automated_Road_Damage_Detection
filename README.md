# 🛣️ Automated Road Damage Detection

> **YOLOv8s** fine-tuned on the **RDD2022** dataset — detecting 4 road damage classes across 6 countries in real time.

[![Hugging Face Spaces](https://img.shields.io/badge/🤗%20Hugging%20Face-Spaces-blue)](https://huggingface.co/spaces/ProjectRoadDamageDetection/Automated-Road-Damage-Detection)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Model: YOLOv8s](https://img.shields.io/badge/Model-YOLOv8s-orange)](https://github.com/ultralytics/ultralytics)
[![Dataset: RDD2022](https://img.shields.io/badge/Dataset-RDD2022-green)](https://arxiv.org/abs/2209.08538)

---

## 📌 Overview

This project provides an automated road damage detection system powered by **YOLOv8s**, fine-tuned on the **RDD2022 (Road Damage Dataset 2022)**. It detects four types of surface damage from road images and provides per-class counts, pothole severity assessments, and country-specific pothole density context.

Upload any road image and get instant visual annotations along with a structured damage report.

---

## 🎯 Damage Classes

| Code | Class Name | Color |
|------|---------------------|------------|
| D00 | Longitudinal Crack | 🔵 Blue |
| D10 | Transverse Crack | 🟢 Green |
| D20 | Alligator Crack | 🟠 Orange |
| D40 | Pothole | 🔴 Red |

---

## 🌍 Supported Countries (Pothole Context)

| Country | Pothole Density |
|-------------------|------------------------|
| 🇮🇳 India | ⬛⬛⬛ Very High |
| 🇳🇴 Norway | ⬛⬛⬛ High |
| 🇺🇸 United States | ⬛⬛⬛ Moderate |
| 🇨🇿 Czech Republic | ⬛⬛⬛ Moderate |
| 🇨🇳 China | ⬛⬛ Low-Moderate |
| 🇯🇵 Japan | ⬛ Low |

---

## 🚀 How to Use

1. **Upload a road image** using the image input panel (drag & drop, camera capture, or paste from clipboard).
2. **Adjust thresholds** (optional):
   - **Confidence Threshold** (default: `0.25`) — minimum detection confidence score.
   - **IoU Threshold** (default: `0.45`) — suppresses overlapping boxes.
3. **Select the country** where the photo was taken for pothole density context.
4. Click **🔍 Detect Damage** (or the image auto-triggers detection on upload).
5. View the **annotated output image** + **Detection Summary**, **Pothole Report**, and **Country Context** tables.

---

## 📊 Output Explained

### Detection Summary

A per-class breakdown table showing:

- Count of each damage type detected
- Percentage of total detections

### Pothole (D40) Report

| Field | Description |
|------------------|------------------------------------------------|
| Pothole Count | Number of D40 boxes detected |
| % of Detections | Proportion of potholes vs all damage |
| Severity | Critical / Moderate / Low / None |
| Avg Confidence | Mean confidence score for pothole boxes |

**Severity thresholds:**

- 🔴 **CRITICAL** — Potholes > 30% of all detections → Immediate repair needed
- 🟠 **MODERATE** — Potholes > 10% → Schedule maintenance
- 🟡 **LOW** — Any potholes detected → Monitor road surface
- 🟢 **NONE DETECTED** — Road surface OK

### Country Context

Provides pothole density, dominant damage types, and data collection method for the selected country as documented in the RDD2022 dataset.

---

## 🧠 Model Details

| Property | Value |
|---------------|---------------------------|
| Architecture | YOLOv8s (small) |
| Weights file | `yolov8s_best.pt` |
| Input size | 640 × 640 px |
| Classes | 4 (D00, D10, D20, D40) |
| Framework | Ultralytics YOLOv8 |
| Device | CUDA (GPU) / CPU fallback |

---

## 📁 Dataset — RDD2022

- **Total images:** 47,420
- **Countries:** India, Japan, United States, Czech Republic, China, Norway
- **Annotation format:** Bounding boxes (YOLO format)
- **Reference:** [Arya et al., 2022 — arxiv:2209.08538](https://arxiv.org/abs/2209.08538)

---

## 🗂️ Repository Structure

```text
Automated-Road-Damage-Detection/
├── app.py                  # Gradio UI + inference pipeline
├── predict.py              # Standalone prediction script
├── yolov8s_best.pt         # Fine-tuned YOLOv8s weights (22.5 MB)
├── rdd2022.yaml            # Dataset config (class names, paths)
├── requirements.txt        # Python dependencies
├── examples/               # Sample road images (6 countries)
│   ├── india_test_image.jpg
│   ├── China_Drone_000253.jpg
│   ├── United_States_004798.jpg
│   ├── Czech_test_image.jpg
│   ├── China_Drone_000295.jpg
│   └── norway_road_test.jpg
└── README.md
```

---

## 🔧 Local Setup

```bash
# Clone the Space
git clone https://huggingface.co/spaces/ProjectRoadDamageDetection/Automated-Road-Damage-Detection
cd Automated-Road-Damage-Detection

# Install dependencies
pip install -r requirements.txt

# Run the app
python app.py
```

The app will be available at `http://localhost:7860`.

---

## 📦 Requirements

```text
gradio>=4.0
ultralytics
torch
torchvision
numpy
Pillow
opencv-python
```

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](https://opensource.org/licenses/MIT) for details.

---

## 📚 Citation

If you use this work or the RDD2022 dataset, please cite:

```bibtex
@article{arya2022rdd2022,
  title   = {RDD2022: A multi-national image dataset for automatic Road Damage Detection},
  author  = {Arya, Deeksha and Maeda, Hiroya and Ghosh, Sanjay Kumar and Toshniwal, Durga and Mraz, Alexander and Kashiyama, Takehiro and Sekimoto, Yoshihide},
  journal = {arXiv preprint arXiv:2209.08538},
  year    = {2022}
}
```

---

## 🙌 Acknowledgements

- [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics) for the object detection framework
- [RDD2022 Dataset](https://arxiv.org/abs/2209.08538) for the training data
- [Gradio](https://gradio.app/) for the web interface
