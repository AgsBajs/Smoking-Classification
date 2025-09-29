# Smoking Prediction with Logistic Regression  
**Using the Global Coffee Health Dataset (Kaggle)**  

## 📌 Project Overview  
This project explores the relationship between lifestyle factors and smoking behavior using the [Global Coffee Health Dataset](https://www.kaggle.com/datasets/uom190346a/global-coffee-health-dataset/data). The primary goal was to build a predictive model to identify smokers based on demographic, lifestyle, and health-related features.  

We compared baseline models (Logistic Regression and Random Forest), tuned Logistic Regression, and explored the role of decision thresholds in balancing **precision** and **recall**.  

---

## 📊 Dataset Description  
The dataset contains **10,000 synthetic records** reflecting realistic correlations between coffee consumption, sleep, and health outcomes across 20 countries.  

### **Features**  
- **ID** *(int)* → Unique record ID  
- **Age** *(int)* → Participant age (18–80)  
- **Gender** *(cat)* → Male, Female, Other  
- **Country** *(cat)* → Country of residence (20 total)  
- **Coffee_Intake** *(float)* → Cups of coffee per day (0–10)  
- **Caffeine_mg** *(float)* → Estimated daily caffeine intake in mg  
- **Sleep_Hours** *(float)* → Hours of sleep per night (3–10)  
- **Sleep_Quality** *(cat)* → Poor, Fair, Good, Excellent  
- **BMI** *(float)* → Body Mass Index (15–40)  
- **Heart_Rate** *(int)* → Resting heart rate (50–110 bpm)  
- **Stress_Level** *(cat)* → Low, Medium, High  
- **Physical_Activity_Hours** *(float)* → Weekly physical activity (0–15 hours)  
- **Health_Issues** *(cat)* → None, Mild, Moderate, Severe  
- **Occupation** *(cat)* → Office, Healthcare, Student, Service, Other  
- **Smoking** *(bool)* → Target variable (0 = No, 1 = Yes)  
- **Alcohol_Consumption** *(bool)* → 0 = No, 1 = Yes  

---

## 🔎 Methodology  
1. **Preprocessing**  
   - Imputed missing values (median for numerics, most frequent for categoricals).  
   - Standardized numeric features.  
   - One-hot encoded categorical features.  

2. **Baseline Models**  
   - Logistic Regression  
   - Random Forest  
   - Observed poor performance from Random Forest due to high sparsity after one-hot encoding and class imbalance.  

3. **Model Tuning**  
   - GridSearchCV on Logistic Regression (`C`, penalty, solver).  
   - Chose **Logistic Regression with L2 penalty, C ≈ 1.445, solver = liblinear**.  

4. **Threshold Tuning**  
   - Explored thresholds 0.3–0.7.  
   - Found **0.45** yielded the best trade-off:  
     - Precision ≈ **0.201**  
     - Recall ≈ **0.828**  
     - F1 Score ≈ **0.323**  
   - ROC-AUC ≈ 0.507 and PR-AUC ≈ 0.208 show the dataset has weak signal for smoking prediction, but recall-focused thresholds enable screening.  

---

## 📈 Results  
- **Default (0.50 threshold)** → Recall = 0.429, F1 = 0.274  
- **Chosen (0.45 threshold)** → Recall = 0.828, F1 = 0.323  
- Confusion Matrix @ 0.45:  
