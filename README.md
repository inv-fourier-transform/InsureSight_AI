<p align="center">
  <img src="https://img.icons8.com/ios-filled/200/4f46e5/heart-health.png" width="120" alt="Health Insurance Cost Predictor" />
</p>

<h2 align="center">InsureSight AI</h2>
<p align="center"><b>InsureSight AI is an ML powered app for predicting health insurance premiums based on personal & medical profiles.</b></p>

<p align="center">
  <a href="https://streamlit.io/"><img alt="Streamlit" src="https://img.shields.io/badge/streamlit-1.43.2-ff4b4b?logo=streamlit&logoColor=white"></a>
  <a href="https://pandas.pydata.org/"><img alt="Pandas" src="https://img.shields.io/badge/pandas-2.2.3-150458?logo=pandas&logoColor=white"></a>
  <a href="https://numpy.org/"><img alt="NumPy" src="https://img.shields.io/badge/numpy-2.2.3-013243?logo=numpy&logoColor=white"></a>
  <a href="https://scikit-learn.org/"><img alt="scikit-learn" src="https://img.shields.io/badge/scikit--learn-1.6.1-f7931e?logo=scikit-learn&logoColor=white"></a>
  <a href="https://xgboost.readthedocs.io/"><img alt="XGBoost" src="https://img.shields.io/badge/xgboost-3.0.1-1f4e79?logo=xgboost&logoColor=white"></a>
  <a href="https://joblib.readthedocs.io/"><img alt="Joblib" src="https://img.shields.io/badge/joblib-1.5.0-4f46e5?logo=python&logoColor=white"></a>
</p>

<p align="center">
  <b>Frontend:</b> Streamlit &nbsp; | &nbsp; <b>ML Framework:</b> XGBoost & scikit-learn &nbsp; | &nbsp; <b>Language:</b> Python
</p>

<p align="center">
  This project uses XGBoost regression models to predict health insurance premiums based on age, medical history, lifestyle factors, & demographics.
</p>

---

A machine learning web application that predicts health insurance premium costs based on user-provided personal and medical information. The application features an intuitive Streamlit interface, age-specific model selection, risk score normalization, and real-time predictions.

---

## Features

- **Age-Based Model Selection**: Uses separate trained models for users aged ≤25 and >25 for improved accuracy.
- **Comprehensive Risk Assessment**: Calculates normalized risk scores based on medical history conditions (Diabetes, Heart Disease, Blood Pressure, Thyroid).
- **Feature Engineering**: Automatically encodes categorical variables (Gender, Region, BMI Category, Smoking Status, etc.).
- **Real-Time Predictions**: Instant premium estimates displayed in INR format.
- **Clean UI**: Organized 4-row grid layout with intuitive icons for all input fields.
- **Input Validation**: Enforces valid ranges for all numeric inputs (Age, Dependants, Income, Genetic Risk).
- **Pre-Trained Models**: Pre-trained XGBoost models and scalers loaded via joblib for fast inference.

---

## Folder Structure

```text
insurance_premium_prediction/
│
├── artifacts/
│   ├── model_u25.joblib          # XGBoost model for age ≤ 25
│   ├── model_others.joblib       # XGBoost model for age > 25
│   ├── scaler_u25.joblib         # Feature scaler for age ≤ 25
│   └── scaler_others.joblib      # Feature scaler for age > 25
│
├── main.py                       # Streamlit frontend application
├── prediction_helper.py          # Prediction logic & preprocessing
├── requirements.txt              # Project dependencies
├── .gitignore                    # Git ignore file
├── LICENSE                       # License file
└── README.md                     # Project documentation
```


---

## Setup Instructions

### Prerequisites

- Python 3.10 or higher
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/inv-fourier-transform/insurance-premium-prediction.git
cd insurance-premium-prediction
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```
### Running the Application
```bash
streamlit run main.py
```
## Input Features

The application collects the following information to generate premium predictions:

### Demographics & Personal Info
- **Age (18–100):** Primary insured's age  
- **Gender:** Male or Female  
- **Marital Status:** Married or Unmarried  
- **Number of Dependants (0–10):** Family members covered  

### Financial & Employment
- **Income in Lakhs (0–200):** Annual income in Indian Rupees (Lakhs)  
- **Employment Status:** Salaried, Self-Employed, or Freelancer  

### Health & Lifestyle
- **BMI Category:** Normal, Overweight, Obesity, or Underweight  
- **Smoking Status:** No Smoking, Occasional, or Regular  
- **Genetical Risk (0–5):** Genetic predisposition risk score  
- **Medical History:**  
  - No Disease  
  - Diabetes  
  - High Blood Pressure  
  - Heart Disease  
  - Thyroid  
  - Or combinations of the above  

### Coverage Details
- **Insurance Plan:** Bronze, Silver, or Gold coverage tier  
- **Region:** Northwest, Southeast, Northeast, or Southwest  

---

## How It Works

### 1. Risk Score Calculation
The `calculate_normalized_risk()` function in `prediction_helper.py` assigns risk scores to medical conditions:

- **Heart Disease:** 8  
- **Diabetes / High Blood Pressure:** 6  
- **Thyroid:** 5  
- **No Disease:** 0  

Combined conditions (e.g., *Diabetes & Heart Disease*) are summed and normalized to a **0–1 scale**.

---

### 2. Feature Preprocessing
- **Categorical Encoding:**  
  One-hot encoding for Gender, Region, Marital Status, BMI Category, Smoking Status, and Employment Status  

- **Ordinal Encoding:**  
  Insurance Plan → Bronze = 1, Silver = 2, Gold = 3  

- **Income Level Mapping:**  
  Income converted to categorical levels:  
  `<10L`, `10L–25L`, `25L–40L`, `>40L`

---

### 3. Age-Based Scaling & Prediction
- Users aged **≤ 25** use `scaler_u25` and `model_u25`  
- Users aged **> 25** use `scaler_others` and `model_others`  

Features are scaled using the appropriate scaler before prediction.  
The **XGBoost regression model** returns the premium estimate.

---

## Model Training (Optional)

To retrain the models with your own data:

1. Prepare your dataset with the features listed above and target variable `premium_amount`
2. Split data by age (≤25 and >25)
3. Train separate XGBoost regressors for each age group
4. Save models and scalers to the `artifacts/` directory using `joblib.dump()`

---

## Contributing

Contributions are welcome!  
Please open an issue or submit a pull request for improvements, bug fixes, or feature enhancements.

---

## License

This project is licensed under the **MIT License**.

---

🎯 *Predict your health insurance premiums with confidence using machine learning!*





