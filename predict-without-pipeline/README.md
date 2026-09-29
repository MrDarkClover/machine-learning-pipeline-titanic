# Titanic Survival Prediction (Without Pipeline)

This repository demonstrates a traditional, step-by-step Machine Learning workflow without using sklearn Pipelines. Each stage—data loading, preprocessing, model training, and evaluation—is handled imperatively across explicit code blocks.

---

## 🛠️ How the Code Works

The execution flows sequentially through distinct scripts or functional blocks, manually passing data structures between steps.

+------------------+
| Raw Data (CSV)   |
+--------+---------+
|
v
+------------------+     • Impute Missing Values (Age, Embarked)
| Preprocessing    | --> • Drop Unused Columns (Cabin, Ticket, Name)
+--------+---------+     • One-Hot Encode Categorical Features (Sex, Embarked)
|
v
+------------------+     • Train/Test Split (80/20)
| Model Training   | --> • Train Random Forest Classifier
+--------+---------+
|
v
+------------------+     • Calculate Accuracy, F1-Score
| Evaluation       | --> • Generate Confusion Matrix
+------------------+


---

## 🏗️ Architecture & Data Flow

[ train.csv ] ──> pd.read_csv() ──> df.fillna() ──> pd.get_dummies() ──> train_test_split()
│
┌────────────────────────────┴────────────────────────────┐
▼                                                         ▼
[ X_train, y_train ]                                      [ X_test, y_test ]
│                                                         │
▼                                                         │
rf_model.fit()                                                     │
│                                                         │
└────────────────────────────┬────────────────────────────┘
▼
rf_model.predict()
│
▼
[ Evaluation Metrics ]


---

## 🚨 Limitations of the Non-Pipelined Approach

1. **Data Leakage Risk:** Imputation parameters (e.g., mean Age) are calculated using the full dataset before splitting into train/test sets.
2. **Code Duplication:** Preprocessing logic must be manually re-written for test and production data.
3. **Low Maintainability:** High coupling between data transformations and model logic makes scaling difficult.

---

## 💻 Quickstart

```bash
git clone [https://github.com/your-username/titanic-non-pipelined.git](https://github.com/your-username/titanic-non-pipelined.git)
cd titanic-non-pipelined
pip install -r requirements.txt
python src/train.py

---
