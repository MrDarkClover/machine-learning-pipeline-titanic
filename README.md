# 4. Master Dual-Method Repository (`README.md`)

```markdown
# Machine Learning Pipeline Comparison: Titanic Dataset

This repository hosts two distinct implementations for predicting survival on the Titanic:
1. **Procedural (Without Pipeline):** Imperative execution using standard Pandas and Scikit-Learn logic.
2. **Pipelined (Scikit-Learn Pipeline):** Modular, leak-proof execution using `Pipeline` and `ColumnTransformer`.

---

## 📊 Structural & Process Comparison

                     INCOMING DATA (train.csv)
                                 │
       ┌─────────────────────────┴─────────────────────────┐
       ▼                                                   ▼
┌─────────────────────────────┐                     ┌─────────────────────────────┐
│    WITHOUT PIPELINE         │                     │        WITH PIPELINE        │
├─────────────────────────────┤                     ├─────────────────────────────┤
│ 1. Global Imputation        │                     │ 1. Train / Test Split First │
│ 2. Manual Encoding          │                     │ 2. Build Pipeline Object    │
│ 3. Train / Test Split       │                     │ 3. Single Fit on Train Data │
│ 4. Separate Predict Calls   │                     │ 4. Unified Transform/Predict│
└──────────────┬──────────────┘                     └──────────────┬──────────────┘
│                                                   │
▼                                                   ▼
┌─────────────────────────────┐                     ┌─────────────────────────────┐
│ Risk of Data Leakage        │                     │ Zero Data Leakage           │
│ Hard to Deploy to API       │                     │ Single Artifact Deployment  │
└─────────────────────────────┘                     └─────────────────────────────┘


---

## 📂 Repository Directory Layout

machine-learning-pipeline-titanic/
├── data/
│   ├── train.csv
│   └── test.csv
├── notebooks/
│   ├── 01_without_pipeline_exploration.ipynb
│   └── 02_pipelined_exploration.ipynb
├── src/
│   ├── without_pipeline/
│   │   ├── preprocess.py
│   │   └── train.py
│   └── with_pipeline/
│       ├── custom_transformers.py
│       ├── build_pipeline.py
│       └── train.py
├── requirements.txt
└── README.md


---

## 🔬 Comparison Matrix

| Feature | Without Pipeline (`src/without_pipeline`) | With Pipeline (`src/with_pipeline`) |
| :--- | :--- | :--- |
| **Data Leakage Safety** | Low (Manual split timing required) | High (Encapsulated step execution) |
| **Code Length** | ~120 Lines | ~60 Lines |
| **Deployment Complexity** | High (Must serialize preprocessing + model separately) | Low (Serialize single `.pkl` or `.joblib` file) |
| **Maintenance** | Brittle | Highly Modular |

---

## 💻 Quickstart

### Run Without Pipeline
```bash
python src/without_pipeline/train.py
Run With Pipeline
Bash
python src/with_pipeline/train.py
