# TrustNewsAI Setup Guidelines

These instructions set up and run the current machine-learning data workflow on Windows using PowerShell. Run commands from the repository root unless a step says otherwise.

## 1. Get the project

If you have not cloned the repository yet:

```powershell
git clone https://github.com/kura458/Trust-News-AI.git
cd Trust-News-AI
```

If you already have the repository, open its folder in VS Code or PowerShell.

## 2. Create a Python virtual environment

From the repository root:

```powershell
cd ml_services
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can run the scripts using the environment's Python directly:

```powershell
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

## 3. Install dependencies

With the virtual environment activated:

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

## 4. Add the dataset files

Download the Kaggle Fake and Real News Dataset and place these two files in:

```text
ml_services\data\raw\True.csv
ml_services\data\raw\Fake.csv
```

The scripts expect these exact filenames. The dataset files are not included in this repository.

## 5. Explore the dataset

From the `ml_services` directory, run:

```powershell
python scripts/explore_dataset.py
```

The script reports dataset structure, label distribution, missing values, duplicate articles, content lengths, and outliers. It also saves a label-distribution chart to `scripts/label_distribution.png`.

## 6. Prepare the dataset

After exploration, run:

```powershell
python scripts/prepare_dataset.py
```

The script cleans and combines article titles and text, removes unsuitable and duplicate records, shuffles the data, and creates a stratified 80/20 train/test split.

Generated files are saved under:

```text
ml_services\data\processed\news_clean.csv
ml_services\data\processed\train.csv
ml_services\data\processed\test.csv
```

These generated data files are ignored by Git.

## 7. Run from the repository root (optional)

You can also run either script from the repository root by using its path:

```powershell
python ml_services/scripts/explore_dataset.py
python ml_services/scripts/prepare_dataset.py
```

Make sure the Python environment has the dependencies installed before running them.

## 8. Troubleshooting

**Python is not recognized:** Install Python and ensure it is available on your PATH. Reopen PowerShell after installation.

**A package is missing:** Activate the `.venv` environment in `ml_services` and run `python -m pip install -r requirements.txt`.

**Dataset files are not found:** Confirm that both `True.csv` and `Fake.csv` are in `ml_services/data/raw/` and that the filenames match exactly.

**The chart is not generated:** Check that Matplotlib and Seaborn installed successfully and review the terminal error message.

## Current project status

This setup guide covers the existing dataset exploration and preparation scripts. It does not describe a notebook workflow: the current repository contains Python scripts, and model training/inference integration is still future work.
