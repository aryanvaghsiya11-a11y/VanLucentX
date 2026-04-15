# VanLucentX | Tri-Modal Health Diagnostic AI

<p align="left">
  <a href="https://vanlucentx.vercel.app/"><img src="https://img.shields.io/badge/Live_Demo-VanLucentX-00C7B7?style=for-the-badge&labelColor=1e293b&logo=vercel&logoColor=white" alt="Live Demo" /></a>
  <img src="https://img.shields.io/badge/Frontend-Next.js_|_Tailwind-0ea5e9?style=for-the-badge&labelColor=1e293b&logo=react&logoColor=white" alt="Frontend Tech" />
  <img src="https://img.shields.io/badge/Backend-FastAPI-009688?style=for-the-badge&labelColor=1e293b&logo=fastapi&logoColor=white" alt="Backend Tech" />
  <img src="https://img.shields.io/badge/AI_Engine-DenseNet_|_XGBoost-f97316?style=for-the-badge&labelColor=1e293b&logo=tensorflow&logoColor=white" alt="ML Architecture" />
</p>

> **Note on Repository Status:** This repository serves as the public-facing showcase and frontend architecture overview for the VanLucentX platform. The core machine learning inference engine, neural network weights, and proprietary data pipelines are maintained in a separate, private repository to protect the intellectual property of the diagnostic algorithms.

## 🌐 Live Application
Experience the interactive dashboard and UI architecture here: **[vanlucentx.vercel.app](https://vanlucentx.vercel.app/)**

---

## 📖 About the Project: The Clinical Challenge
Detecting pulmonary infiltration from standard radiography is historically challenging due to overlapping tissue structures and subtle opacities. Traditional medical AI models attempt to solve this by operating in a vacuum—analyzing a single isolated X-ray image while ignoring the broader clinical picture of the patient. 

**VanLucentX** is an enterprise-grade, "Tri-Modal" AI health screening system designed to fix this isolated approach. It acts as a comprehensive digital diagnostic assistant by fusing three distinct streams of patient data into a single predictive pipeline. By synthesizing visual, historical, and physiological data, the system dramatically reduces false positives and mirrors the holistic diagnostic approach of a human physician.

### 🔍 Transparent AI: The Grad-CAM Integration
In clinical environments,VanLucentX implements **Visual Explainability via Grad-CAM (Gradient-weighted Class Activation Mapping)**. During inference, the system generates a color-coded attention heatmap overlaid directly onto the patient's radiograph, highlighting the exact anatomical regions and opacities that drove the neural network's prediction.

---

## 🧠 The Tri-Modal Architecture & Meta-Learner

The core innovation of the VanLucentX system is its **Stacking Ensemble Meta-Learner**. Rather than relying on a single algorithm, the architecture forces multiple specialized models to collaborate, outputting individual probability scores that are then weighted by a final fusion layer.

### 1. Radiological Vision Pipeline (Unstructured Data)
* **Input Data:** Chest X-Ray (DICOM/JPG)
* **Base Model:** `DenseNet121` (Transfer Learning)
* **Function:** DenseNet121 was selected for its high parameter efficiency and ability to alleviate the vanishing gradient problem. It extracts complex, high-level spatial hierarchies from the imaging data, identifying localized opacities and textural anomalies associated with infiltration.

### 2. Contextual Metadata Pipeline (Structured Data)
* **Input Data:** Patient Age, Biological Sex, Anatomical View Position
* **Base Model:** `XGBoost` (Extreme Gradient Boosting)
* **Function:** A patient's demographic profile significantly alters baseline risk. This tree-based framework processes structural patient records, mapping non-linear relationships in the metadata to provide crucial contextual weighting to the final diagnosis.

### 3. Physiological Time-Series Pipeline (Sequential Data)
* **Input Data:** 100-step time horizon of Heart Rate (BPM) and SpO2 levels
* **Function:** Evaluates dynamic sequence signals to capture physiological distress markers. Because lung infiltration immediately impacts oxygen saturation and cardiac load, tracking these temporal changes allows the model to identify respiratory failure markers that a static image cannot show.

### 🛡️ Engineering Reliability: Aggressive Regularization
Medical AI must perform reliably on unseen patient data. To ensure absolute robustness and prevent the ensemble from memorizing the training data, aggressive regularization techniques are enforced across the entire pipeline:
* **L1 & L2 Weight Decay:** Penalizing overly complex model weights.
* **Strategic Dropout Layers:** Randomly deactivating neurons during training to force the network to learn redundant, robust features.
* **Early Stopping:** Halting training at the exact epoch where validation accuracy peaks, strictly preventing data overfitting.

---

## 💻 Frontend Ecosystem
The deployed application represents a modern, high-performance medical UI designed for clinical trust, utilizing advanced state management to simulate the AI inference process.

* **Framework:** React / Next.js
* **Styling:** Tailwind CSS (Dark Slate / Medical Teal aesthetic tailored for low eye-strain in clinical settings)
* **Motion & Interactions:** Framer Motion (Implementing glassmorphism, staggered structural reveals, and simulated scanning states)
* **Hosting:** Vercel Global Edge Network for millisecond latency

## ⚙️ Backend Architecture & Inference API (Private Repo)
The Next.js frontend securely communicates with a standalone, high-performance backend. Built for speed and scalability, this API layer handles the heavy computational lifting of the ML models and image processing.

* **API Framework:** `FastAPI` (Asynchronous Python) for lightning-fast request handling and strict type validation via Pydantic.
* **Server Orchestration:** `Uvicorn` (ASGI web server) ensuring concurrent handling of medical data payloads.
* **Data Transformation:** Seamlessly converts incoming HTTP requests (images, JSON vitals) into structured `NumPy` tensors and `Pandas` DataFrames required by the inference engine.
* **Inference Endpoints:** Exposes secure REST endpoints (e.g., `POST /api/v1/predict`) that process the tri-modal data and return the Meta-Learner confidence scores alongside base64-encoded Grad-CAM heatmaps in milliseconds.

---
## 📊 Clinical Metrics & Model Performance
The ensemble model was rigorously tested to prioritize diagnostic safety (maximizing True Positives while minimizing False Negatives). Below are the evaluation metrics derived from the validation threshold testing (Meta-Learner at Optimal Youden's J Threshold = 0.374):

| Metric | Score | Clinical Significance |
| :--- | :--- | :--- |
| **Sensitivity (Recall)** | `99.8%` | Ability to correctly identify true positive infiltration cases. |
| **Specificity** | `84.9%` | Ability to correctly identify healthy (normal) scans. |
| **False Positive Rate (FPR)**| `15.1%` | Percentage of healthy patients incorrectly flagged. |
| **ROC-AUC** | `~0.95` | Overall diagnostic capability of the Meta-Learner. |

*(Validation matrix: TP: `530` | TN: `2097` | FP: `372` | FN: `1`)*

## 👨‍💻 Developer & Architect

**Aryan Vaghasiya**

Specializing in building robust, heavily regularized machine learning pipelines and intelligent diagnostic systems. Drawing from professional experience engineering advanced data solutions, including enterprise analytics and AI language services, the focus remains on the intersection of deep neural networks, interpretable AI, and scalable cloud deployment. 

This Tri-Modal system is part of a broader mission to leverage transparent, multi-modal AI in the medical field, moving beyond standard computer vision to build tools that truly assist clinicians in complex decision-making.

* **LinkedIn:** [Connect with me](www.linkedin.com/in/aryan-vaghasiya-68a3b01b6)
