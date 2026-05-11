# Multiple Disease Prediction Web App

Lightweight Streamlit web application that uses several pre-trained ML models (XGBoost / sklearn) to predict multiple diseases from user inputs.

## Quick start (Windows PowerShell)

1. Create and activate a virtual environment and install dependencies:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r Frontend/requirements.txt
```

2. Run the Streamlit app:

```powershell
cd Frontend
streamlit run app.py
```

Notes: you can also run the same commands on macOS / Linux using the appropriate `venv` activation and `pip` commands.

## Repository structure (key files)

- Frontend/
  - [Frontend/app.py](Frontend/app.py#L1) — main Streamlit application
  - [Frontend/requirements.txt](Frontend/requirements.txt#L1) — pinned Python deps for the app
  - [Frontend/code/DiseaseModel.py](Frontend/code/DiseaseModel.py#L1) — XGBoost wrapper and helpers
  - [Frontend/code/helper.py](Frontend/code/helper.py#L1) — symptom array preparation
  - [Frontend/code/train.py](Frontend/code/train.py#L1) — training script (rebuilds `clean_dataset.tsv` and `model/xgboost_model.json`)
  - Data files:
    - [Frontend/data/dataset.csv](Frontend/data/dataset.csv)
    - [Frontend/data/clean_dataset.tsv](Frontend/data/clean_dataset.tsv)
    - [Frontend/data/lung_cancer.csv](Frontend/data/lung_cancer.csv)
    - [Frontend/data/symptom_Description.csv](Frontend/data/symptom_Description.csv)
    - [Frontend/data/symptom_precaution.csv](Frontend/data/symptom_precaution.csv)
  - Models and artifacts:
    - [Frontend/model/xgboost_model.json](Frontend/model/xgboost_model.json#L1)
    - [Frontend/models/diabetes_model.sav](Frontend/models/diabetes_model.sav)
    - [Frontend/models/heart_disease_model.sav](Frontend/models/heart_disease_model.sav)
    - [Frontend/models/parkinsons_model.sav](Frontend/models/parkinsons_model.sav)
    - [Frontend/models/lung_cancer_model.sav](Frontend/models/lung_cancer_model.sav)
    - [Frontend/models/breast_cancer.sav](Frontend/models/breast_cancer.sav)
    - [Frontend/models/chronic_model.sav](Frontend/models/chronic_model.sav)
    - [Frontend/models/hepititisc_model.sav](Frontend/models/hepititisc_model.sav)
    - [Frontend/models/liver_model.sav](Frontend/models/liver_model.sav)
  - Images used by the UI: `d3.jpg`, `positive.jpg`, `negative.jpg`, `h.png`, etc.

## How it works

- The Streamlit UI (`Frontend/app.py`) loads pre-trained models from `Frontend/models/` and `Frontend/model/` and exposes several forms for user input.
- The multi-disease predictor uses an XGBoost model (wrapper in `Frontend/code/DiseaseModel.py`) together with `Frontend/code/helper.py` to convert symptoms into the model feature vector.

## Re-train the XGBoost model (optional)

To rebuild the dataset and re-train the XGBoost model:

```powershell
cd Frontend
python code/train.py
```

This script will recreate `data/clean_dataset.tsv`, train an XGBoost classifier, and save `model/xgboost_model.json`.

## Running notes and troubleshooting

- Most code assumes the working directory is `Frontend` (paths like `data/...` are relative). Use `cd Frontend` before running the training script or `streamlit run app.py` for predictable behavior.
- If you replace or add models, ensure the file names and paths in `Frontend/app.py` match the new files.
- The `requirements.txt` in `Frontend/` contains pinned packages required for the app. If installation fails, try upgrading `pip` and reinstalling.

## Contributing

- Make changes on a branch, run the app locally, and open a PR describing the edits.

## License

- No license specified. Add a `LICENSE` file if you want to declare one.
