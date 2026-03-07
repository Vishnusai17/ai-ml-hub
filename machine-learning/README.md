# 🧠 Machine Learning Curriculum

A structured, progressive curriculum from fundamentals to production-grade ML.

---

## 📍 Phase 1 — Foundations (Weeks 1–4)

### Mathematics
| Topic | Resource |
|---|---|
| Linear Algebra | [3Blue1Brown — Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) |
| Calculus (Derivatives, Chain Rule) | [3Blue1Brown — Essence of Calculus](https://www.youtube.com/playlist?list=PLZHQObOWTQDMsr9K-rj53DwVRMYO3t5Yr) |
| Probability & Statistics | [StatQuest with Josh Starmer](https://www.youtube.com/@statquest) |
| Numpy, Pandas, Matplotlib | [Python Data Science Handbook](https://jakevdp.github.io/PythonDataScienceHandbook/) |

### Core ML Concepts
- Supervised vs Unsupervised vs Reinforcement Learning
- Train / Validation / Test split
- Bias-Variance Tradeoff
- Cross-validation
- Evaluation Metrics (accuracy, precision, recall, F1, AUC-ROC)

---

## 📍 Phase 2 — Classical Algorithms (Weeks 5–10)

| Algorithm | Key Idea | When to Use |
|---|---|---|
| Linear Regression | Fit a line to minimize MSE | Continuous output, linear relationship |
| Logistic Regression | Sigmoid for binary classification | Binary labels, interpretability needed |
| Decision Trees | Recursive binary splits | Tabular data, interpretable |
| Random Forests | Ensemble of decision trees | Most tabular tasks, handles noise |
| Gradient Boosting (XGBoost/LightGBM) | Sequential error correction | Competitions, structured data |
| SVM | Maximum margin hyperplane | High-dimensional, small datasets |
| K-Means | Minimize within-cluster variance | Clustering, customer segmentation |
| PCA | Project to top eigenvectors | Dimensionality reduction, visualization |

**Practice:** [Kaggle Learn](https://www.kaggle.com/learn) + [Scikit-learn Docs](https://scikit-learn.org/)

---

## 📍 Phase 3 — Applied ML (Weeks 11–16)

### Feature Engineering
- Handling missing data (imputation, indicators)
- Encoding categoricals (one-hot, target, embeddings)
- Scaling (StandardScaler, MinMaxScaler, RobustScaler)
- Feature selection (mutual information, SHAP, RFE)

### Model Selection & Tuning
- Grid Search vs Random Search vs Bayesian Optimization (Optuna)
- Early stopping, regularization (L1/L2)
- Calibration (Platt scaling, isotonic regression)

### ML in Production
- Model serialization (joblib, pickle, ONNX)
- Experiment tracking ([Weights & Biases](https://wandb.ai/), MLflow)
- Model monitoring (data drift, concept drift)
- REST APIs for model serving (FastAPI)

---

## 📍 Phase 4 — Projects

| Project | Skills Demonstrated |
|---|---|
| House Price Prediction | Regression, feature engineering, EDA |
| Titanic Survival | Classification, cross-validation, pipelines |
| Customer Churn | Imbalanced data, SHAP explainability |
| Credit Card Fraud Detection | Anomaly detection, precision-recall tradeoff |
| Recommendation System | Collaborative filtering, matrix factorization |

---

## 📚 Full Courses

| Course | Provider | Cost |
|---|---|---|
| Machine Learning Specialization | Coursera / Andrew Ng | Free to audit |
| CS229 Machine Learning | Stanford (YouTube) | Free |
| Applied ML in Python | Michigan / Coursera | Free to audit |
| fast.ai Practical ML | fast.ai | Free |

---

## 📖 Books

| Book | Authors | Level |
|---|---|---|
| Hands-On ML with Scikit-Learn, Keras & TF | Géron | Beginner→Intermediate |
| Pattern Recognition and ML | Bishop | Advanced |
| Probabilistic ML | Murphy | Advanced |
| The Elements of Statistical Learning | Hastie, Tibshirani, Friedman | Advanced (free PDF) |
