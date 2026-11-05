# ISOM3360 Group 13 Project

Developed collaboratively in Google Colab. This repository is a versioned archive; commit dates do not reflect when the work was completed.

## Modelling procedures
0. Setup
1. ⁠⁠Data loading & missing value checking
2. ⁠⁠Preprocessing pipeline
3. ⁠⁠Baseline models with 5-fold CV (majority, logistic, shallow decision tree) + Evaluation
4. ⁠⁠Logistic & decision tree with hyperparameter tuning + Evaluation -> choose one model for further class imbalance handling (should be decision tree but need to check with the evaluation)
5. ⁠⁠Class imbalance handling (Undersampling, Oversampling, SMOTE, class weighting) -> choose the method based on evaluation
6. ⁠⁠Advanced Learners
7. ⁠Threshold / cost analysis
8. ⁠⁠Final model evaluation
9. ⁠⁠Final comparison
10. Export models

## Run predictions locally

Open a terminal in the project folder and create a Python environment.

Create virtual environment and install dependencies from requirements.txt

### Prepare and predict

1. Run model development and "Export Models" code block in the training notebook. Copy the resulting `exported_models/` folder locally, including `model_index.csv`. For Colab, download and extract the folder.
2. Add `unseen_companies.csv` with the same financial features, definitions, units, and normalization as training. No `Bankrupt?` target is needed. Missing values require a saved fitted imputer.
3. Open prediction notebook and run settings, configure settings, and see available exported models.
4. Fill the empty filename in `MODEL_PATH`, check `INPUT_PATH`, and optionally set `ID_COLUMNS`. Example:

   ```python
   MODEL_PATH = EXPORT_DIR / "11_cost_sensitive_decision_tree.joblib"
   ```

5. Rerun settings and all following cells. Results are saved to `predictions/<model_filename>_predictions.csv`, without retraining.

The export includes all 13 named configurations, regardless of performance. Each grid search contributes its selected estimator, not every candidate or fold model.

### Settings and compatibility

- Paths use the working directory printed by settings. Change `EXPORT_DIR` if bundles are elsewhere.
- After switching models, rerun settings and all following cells.
- Leave `THRESHOLD_OVERRIDE = None` to use the saved rule. Overrides should come from training/validation data.
- To replace an existing result, set `OVERWRITE_OUTPUT = True`; otherwise choose a new `OUTPUT_PATH`.
- Match the package versions recorded in the bundle; requirements are not fully pinned. Load only trusted bundles.

Risk scores require calibration before interpretation as probabilities. Use review flags to support analyst judgment.
