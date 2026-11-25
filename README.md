# TrustNewsAI — News Credibility Analysis (Project Scaffold)

TrustNewsAI is an AI-assisted news credibility project intended to classify article text as **REAL** or **FAKE**. This repository contains an early full-stack project structure and a separate data-preparation workflow.

> **Project status:** The repository is an in-progress scaffold. The frontend is still the default Next.js starter page, and the FastAPI backend currently exposes only a basic root endpoint. The frontend, backend, and ML workflow are not yet integrated into a complete working product.

## Repository architecture

```text
Trust-News-AI/
├── frontend/       Next.js 16 / React 19 / TypeScript starter
├── backend/        FastAPI application scaffold
├── ml_services/
│   ├── scripts/    Dataset exploration and preparation
│   ├── src/        Reusable text preprocessing
│   ├── data/       Raw and processed dataset locations
│   └── artifacts/  Reserved for trained model files
├── docs/           Product guide and roadmap
├── setup_guidelines.md
└── done.md
```

## Current ML workflow

The ML service currently focuses on preparing the Kaggle Fake and Real News dataset.

1. Download the dataset and place `True.csv` and `Fake.csv` in `ml_services/data/raw/`.
2. Explore the dataset and inspect its quality.
3. Clean article text, combine title and body, normalize labels, remove duplicates and short records, and create a stratified train/test split.

The processed dataset is written under `ml_services/data/processed/`. See [ML service documentation](ml_services/README.md) for details.

## Requirements

- Python 3.10 or later (use a version compatible with the pinned dependencies)
- Node.js and npm for the frontend
- Windows PowerShell or another terminal

## Set up the ML environment (Windows PowerShell)

Run from the repository root:

```powershell
cd ml_services
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Place the dataset files in `ml_services/data/raw/`, then run:

```powershell
python scripts/explore_dataset.py
python scripts/prepare_dataset.py
```

## Frontend scaffold

```powershell
cd frontend
npm install
npm run dev
``

Open the local URL printed by Next.js (normally `http://localhost:3000`). The current page is the uncustomized starter screen.

## Backend scaffold

Create and activate a Python virtual environment, install FastAPI and an ASGI server, then start the app from the repository root:

```powershell
python -m pip install fastapi uvicorn
uvicorn backend.main:app --reload
```

The current API only provides a basic `GET /` endpoint; no article-analysis endpoint or ML integration is implemented yet.

## Planned next steps

- Implement model training and evaluation in the ML service.
- Add a prediction interface or service endpoint.
- Define request/response schemas and connect FastAPI to inference.
- Replace the Next.js starter page with the article analysis UI.
- Add tests, documented evaluation metrics, and deployment configuration.

## Important limitation

A model prediction is not proof that a news story is true or false. Any future result should be presented as a model estimate, with limitations and source verification guidance.
