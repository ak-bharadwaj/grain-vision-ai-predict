# GrainVision AI — Intelligent Agritech Grain Classification & Quality Scoring

[![React](https://img.shields.io/badge/React-18-61DAFB?logo=react)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue?logo=typescript)](https://www.typescriptlang.org/)
[![Flask](https://img.shields.io/badge/Flask-2.x-black?logo=flask)](https://flask.palletsprojects.com/)
[![Radix UI](https://img.shields.io/badge/Radix_UI-Primitives-161618?logo=radix-ui)](https://www.radix-ui.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?logo=tailwind-css)](https://tailwindcss.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end Agritech Computer Vision platform pairing a **Python/Flask deep learning inference microservice** with a **React 18 / Radix UI analytics dashboard**. GrainVision automates rice varietal identification, aspect ratio morphology analysis, grain breakage grading, and batch purity certification.

---

## 🏛️ System Architecture

```mermaid
flowchart LR
    subgraph ClientApp ["Frontend Architecture (React + Vite + Radix)"]
        Upload["High-Res Ingestion / Drag-and-Drop Image Uploader"]
        QueryState["TanStack React Query Cache Layer"]
        Dashboard["Batch Analytics & Recharts Quality Distribution"]
        Card["Grain Morphology & Defect Inspector"]
    end

    subgraph APILayer ["Inference Server (Python / Flask)"]
        CORS["Flask-CORS Ingress Controller"]
        Preproc["Pillow & OpenCV Preprocessing & Aspect Scaling"]
        Model["Trained Grain Feature Extraction & Classifier"]
        Scorer["Purity, Breakage & Morphological Metrics Engine"]
    end

    Upload --> QueryState
    QueryState -->|POST /predict (multipart/form-data)| CORS
    CORS --> Preproc
    Preproc --> Model
    Model --> Scorer
    Scorer -->|JSON Diagnostic Payload| QueryState
    QueryState --> Dashboard
    QueryState --> Card
```

---

## 🌾 Morphological & Quality Metrics

The computer vision engine evaluates each grain sample across essential agronomic metrics:
1. **Varietal Classification**: Differentiates varieties (Basmati, Jasmine, Arborio, Sona Masoori, etc.) based on length-to-width ratio and surface texture.
2. **Grain Breakage & Head Rice Yield (HRY)**: Measures individual grain lengths to calculate whole grain vs broken grain ratios ($< 75\%$ intact length classified as broken).
3. **Chalkiness & Adulteration Rate**: Analyzes light reflectance to detect chalky kernels and mixture percentages in commercial grain batches.
4. **Foreign Matter & Discoloration**: Flags foreign seed impurities, black tips, and fungal discolorations with bounding-box overlays.

---

## 📂 Repository Structure

```text
grain-vision-ai-predict/
├── app.py                      # Flask backend inference service & REST API
├── backend-setup.md            # Backend environment setup instructions
├── components.json             # Shadcn / Radix component configuration
├── package.json                # React frontend dependencies
├── tailwind.config.js          # Agritech visual design tokens
├── vite.config.ts              # Vite bundle optimization
├── src/
│   ├── components/             # Reusable Radix UI & grain inspector cards
│   ├── pages/                  # Upload, Batch Analysis, and Report Views
│   ├── hooks/                  # React Query data fetching hooks
│   └── lib/                    # API client and formatters
└── Rice Type Classification.docx # Original agritech domain specification
```

---

## 🚀 Getting Started

### 1. Launch Flask Backend
```bash
# In backend directory
python -m venv venv
source venv/bin/activate  # On Windows: .\venv\Scripts\activate
pip install flask flask-cors pillow numpy werkzeug

python app.py
```
Backend runs at `http://localhost:5000`.

### 2. Launch React Frontend
```bash
# In frontend root directory
npm install
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.
