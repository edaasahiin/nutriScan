# nutriScan
🥗 NutriScan – Predicting Nutrition Grades of Food Products
COE305 – Machine Learning Final Project
Team Members:
Eda Şahin
Tuana Harmankaya
Zehra Özcan

📌 Project Overview
NutriScan is a multi-class machine learning system designed to predict the nutrition_grade_fr (A–E) of food products using structured nutritional values per 100g.
Food databases often contain missing or inconsistent nutrition grades. This project builds a robust predictive pipeline to estimate grades automatically using numeric nutrient features.
Final best-performing model: Random Forest

🎯 Problem Statement
Given nutritional values per 100g:
energy_100g
fat_100g
saturated-fat_100g
sugars_100g
salt_100g
proteins_100g
fiber_100g
carbohydrates_100g
Predict:
nutrition_grade_fr ∈ {a, b, c, d, e}
This is treated as a multi-class classification problem.

📊 Dataset
Original Source: OpenFoodFacts (Kaggle)
Customized subset: 5,000 US products
Final labeled samples: 4,026
Data type: Structured (tabular)
Important:
The column nutrition-score-fr_100g was excluded to prevent data leakage.

⚙️ Data Preprocessing
Removed rows with missing target labels
Median imputation for numeric missing values
StandardScaler applied for linear/distance-based models
Stratified 80/20 train-test split
Stratified K-Fold (3-fold) used in hyperparameter tuning
Evaluation metrics:
Accuracy
Macro Precision
Macro Recall
Macro F1 (primary metric due to class imbalance)

🤖 Models Implemented
Non-Ensemble Models
Logistic Regression
Decision Tree
K-Nearest Neighbors (KNN)
Ensemble Models
Random Forest
Gradient Boosting
Tuned Random Forest (GridSearchCV)

📈 Model Performance (Test Set)
Model	Accuracy	Macro F1
Logistic Regression	0.629	0.606
Decision Tree	0.819	0.821
KNN	0.667	0.659
Random Forest	0.857	0.854
Gradient Boosting	0.851	0.847
Tuned Random Forest	0.857	0.854

Best Model: Random Forest
Tree-based ensemble models significantly outperformed linear baselines due to their ability to capture non-linear relationships and feature interactions.

🔍 Feature Importance Insights
Model-based feature importance analysis showed:
salt_100g
saturated-fat_100g
energy_100g
sugars_100g
These were the most influential predictors.
This aligns with nutrition scoring logic: higher salt and saturated fat levels generally correspond to worse grades.

📊 SHAP Interpretability
SHAP (TreeExplainer) was used to analyze feature contributions.
Findings:
Strong interactions between salt, saturated fat, and energy
Tree-based models effectively captured non-linear feature interactions

📉 Confusion Matrix Insights
Most classification errors occurred between neighboring grades (e.g., b↔c, c↔d).
Extreme grades (a vs e) were rarely confused, indicating strong separation of very healthy vs very unhealthy products.

💻 User Interface (Streamlit)
A Streamlit web application was implemented to:
Browse 4,026 products
Filter by grade
Search by product name
Display nutritional values
Show health risk score (mapped from grade)
Provide rule-based nutritional insights
Run UI Locally
pip install -r requirements.txt
streamlit run app.py
Then open:
http://localhost:8501

🛠 Technologies Used
Python
pandas
numpy
scikit-learn
matplotlib
seaborn
shap
streamlit
Google Colab

🚀 Future Improvements
Incorporate ingredient text using NLP
Apply class imbalance techniques
Probability calibration
Explore advanced boosting libraries (XGBoost, LightGBM)

📂 Repository Structure (Suggested)
├── notebook.ipynb
├── app.py
├── requirements.txt
├── README.md
└── data/

📚 References
OpenFoodFacts Dataset
Breiman (2001) – Random Forest
Friedman (2001) – Gradient Boosting
Scikit-learn Documentation
