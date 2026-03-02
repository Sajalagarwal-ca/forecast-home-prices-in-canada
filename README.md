# 🏠 Canada Home Price Prediction

A full-stack machine learning project that predicts residential property prices across Canadian cities and deploys the model as a live REST API using Flask.

![Python](https://img.shields.io/badge/Python-3.8+-blue?style=flat-square&logo=python)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.0+-orange?style=flat-square&logo=scikit-learn)
![XGBoost](https://img.shields.io/badge/XGBoost-Latest-red?style=flat-square)
![Flask](https://img.shields.io/badge/Flask-2.0+-black?style=flat-square&logo=flask)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=flat-square)

---

## Video Demo

[![YouTube Demo](https://www.youtube.com/watch?v=kycgobofe80)](https://www.youtube.com/watch?v=kycgobofe80)

## 📌 Project Overview

Predicting home prices is one of the most practical and high-value applications of machine learning in real estate. This project builds an end-to-end pipeline — from raw housing data through feature engineering, model comparison, and deployment — to produce a working price prediction tool for Canadian cities including **Toronto**, **Vancouver**, and **Barrie**.

The project demonstrates the full data science workflow: data cleaning, exploratory analysis, feature engineering, multi-model comparison, hyperparameter tuning, and production deployment via a Flask web application.

---

## 🎯 Objective

Build a regression model that accurately predicts Canadian residential home prices based on property features, with the final model deployed as a REST API that accepts city, size, and bedroom inputs and returns a price estimate.

---

## 📁 Project Structure

```
Canada-Home-Price-Prediction/
│
├── dataset/
│   └── canadian_housing_data.csv       # Raw housing dataset
│
├── notebooks/
│   └── Canada_Home_Price_Prediction.ipynb  # Full EDA, modelling, and analysis
│
├── flask_app/
│   ├── app.py                          # Flask REST API server
│   ├── model.pkl                       # Serialised trained model
│   ├── columns.json                    # Feature columns for inference
│   └── templates/
│       └── index.html                  # Frontend UI
│
├── requirements.txt                    # Python dependencies
└── README.md
```

---

## 🗂️ Dataset

The dataset contains residential property listings from across Canada with the following key features:

| Feature | Type | Description |
|---|---|---|
| `city` | Categorical | Canadian city (Toronto, Vancouver, Barrie, etc.) |
| `province` | Categorical | Province of the listing |
| `bedrooms` | Numeric | Number of bedrooms |
| `bathrooms` | Numeric | Number of bathrooms |
| `sqft` | Numeric | Total square footage of the property |
| `property_type` | Categorical | House, condo, townhouse, etc. |
| `price` | Numeric (Target) | Sale price in CAD |

---

## ⚙️ Methodology

### 1. Data Cleaning & Feature Engineering
- Removed null values and duplicate listings
- Identified and capped outliers in `price` and `sqft` using IQR-based filtering
- Applied **One-Hot Encoding** to categorical variables (`city`, `province`, `property_type`)
- Created interaction features between `sqft` and `bedrooms`
- Normalised continuous variables for scale-sensitive models

### 2. Exploratory Data Analysis
- Price distribution by city and property type
- Correlation heatmap of numeric features
- Outlier visualisation with box plots
- Geographic price variation analysis

### 3. Model Building & Comparison

Three regression models were built and evaluated head-to-head:

| Model | RMSE | R² Score | Notes |
|---|---|---|---|
| Linear Regression | High | ~0.68 | Baseline — misses non-linear patterns |
| Decision Tree | Medium | ~0.78 | Captures non-linearity, prone to overfitting |
| **XGBoost** | **Lowest** | **~0.89** | **Best model — handles interactions & outliers** |

### 4. Hyperparameter Tuning
- `GridSearchCV` used to tune XGBoost parameters: `max_depth`, `n_estimators`, `learning_rate`, `subsample`
- 5-fold cross-validation to prevent overfitting

### 5. Flask Deployment
- Trained model serialised with `pickle` as `model.pkl`
- REST API built with Flask exposing a `/predict` POST endpoint
- Frontend HTML form collects city, sqft, and bedrooms inputs
- Returns predicted price as a JSON response

---

## 🚀 Getting Started

### Prerequisites

```bash
Python 3.8+
pip
```

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/Canada-Home-Price-Prediction.git
cd Canada-Home-Price-Prediction

# Install dependencies
pip install -r requirements.txt
```

### Run the Jupyter Notebook

```bash
jupyter notebook notebooks/Canada_Home_Price_Prediction.ipynb
```

### Run the Flask App

```bash
cd flask_app
python app.py
```

Then open your browser at `http://localhost:5000`

### API Usage

```bash
curl -X POST http://localhost:5000/predict \
  -H "Content-Type: application/json" \
  -d '{"city": "Toronto", "sqft": 1200, "bedrooms": 3, "bathrooms": 2}'
```

**Response:**
```json
{
  "predicted_price": 874500.0,
  "city": "Toronto",
  "currency": "CAD"
}
```

---


## 🧰 Tech Stack

| Tool | Purpose |
|---|---|
| **Python 3.8+** | Core language |
| **pandas** | Data manipulation and cleaning |
| **NumPy** | Numerical operations |
| **scikit-learn** | Linear Regression, Decision Tree, preprocessing, GridSearchCV |
| **XGBoost** | Best-performing regression model |
| **Matplotlib / seaborn** | Data visualisation and EDA |
| **Flask** | REST API and web deployment |
| **pickle** | Model serialisation |
| **Jupyter Notebook** | Development and exploration |

---

## 📈 Key Findings

1. **XGBoost dominates** — Achieves the lowest RMSE and highest R² by capturing non-linear feature interactions that linear models cannot.
2. **City is the strongest predictor** — Toronto and Vancouver command significant price premiums over other Canadian cities.
3. **Sqft × bedrooms interaction matters** — A 3-bedroom 1,200 sqft property prices very differently than a 1-bedroom at the same sqft.
4. **Outlier removal was critical** — Luxury listings skewed the distribution; capping them significantly improved model generalisation.

---

## 🔮 Future Improvements

- [ ] Add more Canadian cities and postal code-level granularity
- [ ] Incorporate time-series features (listing date, market cycle)
- [ ] Experiment with ensemble stacking (XGBoost + Random Forest + Ridge)
- [ ] Deploy to cloud (AWS / GCP / Heroku) for public access
- [ ] Build a React frontend for a more polished UI
- [ ] Add SHAP values for model explainability

---

## 📺 YouTube Video

Watch the full project walkthrough on YouTube: **[https://www.youtube.com/watch?v=kycgobofe80]**

The video covers every step — from raw data to live Flask deployment — with detailed explanations of every design decision.

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## 👤 Author

**Sajal Agarwal**
- GitHub: [@Sajalagarwal-ca](https://github.com/Sajalagarwal-ca)
- LinkedIn: [agarwalsajal](https://www.linkedin.com/in/agarwalsajal/)
- YouTube: [ACS-Consultyics](https://www.youtube.com/@ACS-Consultyics)

---

⭐ **If this project helped you, please give it a star on GitHub!** ⭐
