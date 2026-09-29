# 2. Pipelined Machine Learning Project (`README_pipeline.md`)

```markdown
# Titanic Survival Prediction (Scikit-Learn Pipeline)

An end-to-end Machine Learning implementation using `sklearn.pipeline.Pipeline` and `ColumnTransformer` to enforce robust, modular data processing and prevent data leakage.

---

## 🛠️ How the Code Works

The pipeline bundles preprocessors and estimators into a single composite estimator. When `.fit()` or `.predict()` is called on the main pipeline, transformations apply automatically in sequence.

                  +-----------------------------+
                  |       Raw Data Input        |
                  +--------------+--------------+
                                 |
         +-----------------------+-----------------------+
         |                                               |
         v                                               v
Numerical Transformer                          Categorical Transformer
+-----------------------+                      +-----------------------+
| SimpleImputer(median) |                      | SimpleImputer(mode)   |
+-----------+-----------+                      +-----------+-----------+
|                                              |
v                                              v
+-----------------------+                      +-----------------------+
| StandardScaler()      |                      | OneHotEncoder()       |
+-----------+-----------+                      +-----------+-----------+
|                                               |
+-----------------------+-----------------------+
|
v
ColumnTransformer Union
|
v
RandomForestClassifier
|
v
Model Prediction


---

## 🏗️ Architecture & Data Flow

                              COLUMNTRANSFORMER
                   ┌──────────────────────────────────────┐
                   │  Numeric Pipeline                    │
                   │  [ Imputer ] ──> [ StandardScaler ]  │
[ Raw Data Input ] ──> │                                      │ ──> [ RandomForest ] ──> Output
│  Categorical Pipeline                │
│  [ Imputer ] ──> [ OneHotEncoder ]   │
└──────────────────────────────────────┘


---

## 🔑 Key Features & Pipeline Components

```python
from sklearn.compose import ColumnTransformer
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import StandardScaler, OneHotEncoder
from sklearn.ensemble import RandomForestClassifier

num_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

cat_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('encoder', OneHotEncoder(handle_unknown='ignore'))
])

preprocessor = ColumnTransformer(transformers=[
    ('num', num_transformer, ['Age', 'Fare', 'SibSp', 'Parch']),
    ('cat', cat_transformer, ['Sex', 'Embarked'])
])

full_pipeline = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', RandomForestClassifier(n_estimators=100, random_state=42))
])
💻 Quickstart
Bash
git clone [https://github.com/your-username/titanic-pipelined.git](https://github.com/your-username/titanic-pipelined.git)
cd titanic-pipelined
pip install -r requirements.txt
python src/train_pipeline.py

---
