# TrustNewsAI ML Service

This folder contains the current machine-learning data preparation workflow:

- Raw dataset input
- Dataset exploration and quality checks
- Text cleaning and content construction
- Duplicate and short-record filtering
- Stratified train/test split
- Processed CSV outputs
- Reusable text preprocessing utilities

The current milestone prepares data for later model training. Model training and inference are not yet implemented in this service.

## Setup

Create and activate a virtual environment from inside `ml_services/`:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## Dataset

Download the Kaggle Fake and Real News Dataset and place the raw files here:

```text
data/raw/True.csv
data/raw/Fake.csv
```

The dataset is not included in this repository.

## Python Script Workflow

Run the scripts from the `ml_services/` directory.

### 1. Explore the dataset

```powershell
python scripts/explore_dataset.py
```

The exploration script reports:

- Data shape and columns
- REAL/FAKE label distribution
- Missing values and duplicate article count
- Article content-length statistics
- Potential content-length outliers
- Sample article titles

It also saves a label-distribution chart to `scripts/label_distribution.png`.

### 2. Prepare the dataset

```powershell
python scripts/prepare_dataset.py
```

The preparation script:

- Cleans title and article text
- Combines title and text into a content field
- Removes missing, invalid, short, and duplicate records
- Shuffles the cleaned data with a fixed random seed
- Creates a stratified 80/20 train/test split

Generated outputs:

```text
data/processed/
  news_clean.csv
  train.csv
  test.csv
```

The full cleaned file contains `title`, `text`, `content`, and `label`. The train and test files contain `content` and `label`.

## Project Structure

```text
ml_services/
  scripts/
    explore_dataset.py
    prepare_dataset.py
  src/
    trustnews_ml/
      __init__.py
      preprocessing.py
  data/
    raw/          Raw input CSV files (not committed)
    processed/    Generated CSV files (not committed)
  artifacts/      Reserved for future trained model files
  requirements.txt
```

## Current Data Contract

The cleaned dataset uses these columns:

- `title`
- `text`
- `content`
- `label`

Allowed labels:

- `REAL`
- `FAKE`

## Limitations and next step

This service currently explores and prepares data; it does not yet train a classifier or expose prediction functionality. The next milestone is to train and evaluate models using the prepared training data, then save and test the selected model before integrating inference with the backend.
