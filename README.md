# Crypto Scam Transaction Detection

Summative project for the Introduction to Machine Learning module. Compares traditional Scikit-learn models against TensorFlow deep learning models (Sequential and Functional APIs, `tf.data` pipeline) on a crypto scam transaction classification problem.

## Repository contents

```
── Crypto-Scam-Detection-Report/
    ├── Model-Training-and-Evaluation_HonourGod-Levison.ipynb   # main notebook (run this)
    └── crypto_scam_transaction_dataset.csv                      # dataset (20,000 transactions)
    └── figures/                                                  # plots saved by the notebook
```
## Problem statement

Given metadata available at the moment a blockchain transaction executes (wallet history, transaction/gas amounts, chain/platform/token, behavioural scores), predict whether the transaction is associated with scam activity (`is_scam`). The dataset is imbalanced (7.25% positive) and the notebook explicitly addresses this through stratified splitting, class weighting, and PR-AUC-first evaluation rather than relying on raw accuracy.

## How to run

The notebook's first cell (`!pip install ...`) installs all dependencies, so it runs unmodified on Colab or a fresh Jupyter environment — just open it and Run All. To execute it headlessly instead:

```bash
pip install tensorflow scikit-learn xgboost pandas numpy matplotlib seaborn nbformat nbclient
jupyter nbconvert --to notebook --execute --inplace "Model-Training-and-Evaluation_HonourGod-Levison.ipynb"
```

Random seed is fixed (42) for reproducibility. The Scikit-learn/XGBoost results are fully deterministic under this seed; the two TensorFlow models show minor run-to-run variation (±0.02 PR-AUC) from CPU floating-point non-determinism — see the report's Appendix A for details.

> **Windows note:** if you hit a `WinError 206`/long-path `OSError` installing TensorFlow, it's the 260-character `MAX_PATH` limit colliding with TensorFlow's deeply nested headers — install into a virtual environment at a short path (e.g. `C:\ml-venv`) rather than enabling Windows long-path support system-wide.

## Models and experiments

| Family | Models |
|---|---|
| Traditional ML (Scikit-learn) | Logistic Regression, Random Forest (tuned), XGBoost (tuned) |
| Deep Learning (TensorFlow) | Sequential MLP, Functional-API Wide & Deep network |

13 experiments in total (3 traditional models, 2 feature-selection variants, 2 main deep models, 6 deep-learning ablation configs) are recorded in a single consolidated experiment log inside the notebook (Section 6.2), alongside dedicated outlier/noise analysis (Section 3.1), an empirical feature-selection validation (Section 5.4), and a bias–variance analysis (Section 7.1).

## Links

- **Report:** [Crypto-Scam-Detection_Summative-Assessment/Crypto-Scam-Detection_Summative-Assessment-HonourGod-Levison.pdf]
- **GitHub repo:** `https://github.com/H-levison/Crypto-Scam-Detection_Summative-Assessment.git`
- **Presentation video:** `<add once recorded>`
