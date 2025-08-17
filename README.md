# Travel Package Purchase Prediction (AIML)

## Overview
This project predicts whether a prospective customer will purchase a travel package based on demographic, engagement, and sales-pitch attributes. Using supervised learning, multiple models are trained and compared to identify the best-performing approach for conversion prediction.

---

## Goals
- Predict the probability that a prospect will purchase a travel package (`ProdTaken`)
- Compare baseline and tuned models on held-out test data
- Surface feature patterns that correlate with conversions

---

## Dataset
- File: `Tourism.xlsx` (sheet: `Tourism`)
- Shape: 4,888 rows × 20 columns
- Target: `ProdTaken` (1 = purchased, 0 = not purchased)
- Example features:
  - Demographics: `Age`, `Gender`, `MaritalStatus`, `NumberOfChildrenVisiting`
  - Engagement: `TypeofContact`, `DurationOfPitch`, `NumberOfFollowups`, `PitchSatisfactionScore`
  - Product/context: `ProductPitched`, `PreferredPropertyStar`, `CityTier`, `NumberOfTrips`
  - Other: `Passport`, `OwnCar`, `MonthlyIncome`, `Occupation`, `Designation`

---

## Methodology

### 1) Data Preparation
- Loaded data from `Tourism.xlsx` (`Tourism` sheet)
- Train/test split
- Encoded categorical variables; numerical features left in native scales or standardized as appropriate
- Removed purely identifier fields from modeling

### 2) Modeling
- Baselines and ensembles implemented in the notebook:
  - Logistic Regression
  - Decision Tree
  - Random Forest
  - Gradient Boosting
  - AdaBoost
  - XGBoost
- Hyperparameter tuning performed (grid/random search), with both **baseline** and **tuned** model variants evaluated

### 3) Evaluation
- Metrics reported on the **test set**:
  - Accuracy
  - Recall
  - Precision
  - F1-score
- Additional tabular “training performance” summaries are included in the notebook for reference

---

## Results (Test Set)
The notebook’s final comparison shows the following (**selected highlights**):

| Model                              | Accuracy | Recall  | Precision | F1     |
|------------------------------------|---------:|--------:|----------:|-------:|
| Decision Tree                      | 0.881    | 0.687   | 0.684     | 0.686  |
| Bagging Classifier                 | 0.914    | 0.671   | 0.842     | 0.747  |
| Weighted Bagging Classifier        | 0.891    | 0.581   | 0.786     | 0.668  |
| Random Forest Classifier           | 0.910    | 0.573   | 0.916     | 0.705  |
| Weighted Random Forest Classifier  | 0.905    | 0.520   | 0.955     | 0.674  |
| Tuned AdaBoost Classifier          | 0.881    | 0.654   | 0.697     | 0.675  |
| Tuned GradientBoost Classifier     | 0.874    | 0.496   | 0.753     | 0.598  |
| **Tuned XGBoost Classifier**       | **0.887**| **0.841**| 0.657    | 0.738  |

**Takeaways**
- **Bagging** achieved the highest **accuracy** (~0.914) with strong precision/recall balance.
- **Random Forest** also performed strongly on accuracy and precision.
- **Tuned XGBoost** delivered the **highest recall** (~0.841) with solid F1, making it attractive when catching as many true buyers as possible is the priority.

> Tip: Choose between Bagging/Random Forest vs. tuned XGBoost based on business need: overall accuracy and precision vs. higher recall of likely buyers.

---

## Repository Structure
```
AIML-Travel-Package-Purchase-Prediction/
├── TravelPackagePredicitionProject.ipynb # Main notebook
├── Tourism.xlsx # Dataset (sheet: Tourism)
└── README.md # Project documentation
```
