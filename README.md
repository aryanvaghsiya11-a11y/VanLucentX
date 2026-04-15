# VanLucentX | Tri-Modal Health Diagnostic AI

[![Live Demo](https://img.shields.io/badge/Live_Demo-VanLucentX-00C7B7?style=for-the-badge)](https://vanlucentx.vercel.app/)
[![Frontend Tech](https://img.shields.io/badge/Frontend-React_|_Tailwind_|_Framer-282C34?style=for-the-badge&logo=react)](#)
[![ML Architecture](https://img.shields.io/badge/AI_Engine-DenseNet121_|_XGBoost-FF6F00?style=for-the-badge&logo=tensorflow)](#)

> **Note on Repository Status:** This repository serves as the public-facing showcase and frontend architecture overview for the VanLucentX platform. The core machine learning inference engine, neural network weights, and proprietary data pipelines are maintained in a separate, private repository to protect the intellectual property of the diagnostic algorithms.

## 🌐 Live Application
Experience the interactive dashboard and UI architecture here: **[vanlucentx.vercel.app](https://vanlucentx.vercel.app/)**

---

## 📖 About the Project: The Clinical Challenge
Detecting pulmonary infiltration from standard radiography is historically challenging due to overlapping tissue structures and subtle opacities. Traditional medical AI models attempt to solve this by operating in a vacuum—analyzing a single isolated X-ray image while ignoring the broader clinical picture of the patient. 

**VanLucentX** is an enterprise-grade, "Tri-Modal" AI health screening system designed to fix this isolated approach. It acts as a comprehensive digital diagnostic assistant by fusing three distinct streams of patient data into a single predictive pipeline. By synthesizing visual, historical, and physiological data, the system dramatically reduces false positives and mirrors the holistic diagnostic approach of a human physician.

### 🔍 Transparent AI: The Grad-CAM Integration
In clinical environments, "black-box" AI is insufficient; physicians must understand *why* a model reached its conclusion. VanLucentX implements **Visual Explainability via Grad-CAM (Gradient-weighted Class Activation Mapping)**. During inference, the system generates a color-coded attention heatmap overlaid directly onto the patient's radiograph, highlighting the exact anatomical regions and opacities that drove the neural network's prediction.

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

---

## 👨‍💻 Developer & Architect

**Aryan Vaghasiya** | *Data & AI*

Specializing in building robust, heavily regularized machine learning pipelines and intelligent diagnostic systems. Drawing from professional experience engineering advanced data solutions, including enterprise analytics and AI language services, the focus remains on the intersection of deep neural networks, interpretable AI, and scalable cloud deployment. 

This Tri-Modal system is part of a broader mission to leverage transparent, multi-modal AI in the medical field, moving beyond standard computer vision to build tools that truly assist clinicians in complex decision-making.

* **GitHub:** [aryanvaghsiya11-a11y](https://github.com/aryanvaghsiya11-a11y)
* **LinkedIn:** [Connect with me](https://www.linkedin.com/in/aryan-vaghasiya/)
