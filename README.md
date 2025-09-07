# Intelligent Detection and Elimination of Energy Waste in Healthcare Facilities  
Edunet AIML Internship – Progress Submission  

---

## Problem Statement  
Healthcare facilities waste **30 – 40 %** of energy during non-critical operating hours (nights, weekends, low-occupancy periods) due to:  
- Medical equipment running unnecessarily  
- HVAC systems maintaining full capacity in empty wards  
- Lighting systems not adapting to real occupancy  
- Lack of intelligent scheduling for non-critical loads  

Goal: develop **machine-learning models** that distinguish **critical vs. non-critical** energy consumption and flag waste without compromising patient safety.

---

## Dataset  
**Hospital Energy Saving System Dataset** (Kaggle)  
- 10 000 rows × 25 columns  
- 5-minute resolution, patient vitals + granular power-usage data  
- Features for HVAC, lighting, medical equipment, environmental conditions, renewable usage, system health

Dataset link (download instructions in repo): *Hospital Energy Saving System Dataset – Kaggle*

---

## Week 1 Progress ✔️  
1. **Data loading & cleaning**  
   - Verified dtypes, no missing values or duplicates  
   - Converted `Timestamp` and extracted `Hour`, `Day_of_Week`, `Month`  
2. **Feature engineering**  
   - `Critical_Hours` = weekday 06:00 – 22:00  
   - `Energy_Waste` = high (> 70th pct) consumption during non-critical hours  
   - Ratios: `HVAC_to_Total_Ratio`, `Medical_to_Total_Ratio`, `Lighting_to_Total_Ratio`  
3. **Result**  
   - 1 532 potential waste records (≈ 15 %) identified  

---

## Week 2 Progress: ML Model Implementation 🚀  

### 1 . Exploratory Data Analysis  
- Bar chart: **energy-waste counts by hour** (peak waste after 22:00 and before 06:00)  
- Box plot: **consumption distribution** shows median non-critical use is significantly lower, with long right tail during waste events  

### 2 . Model Selection & Training  
| Model | Accuracy | Precision (waste) | Recall (waste) | F1-score (waste) |
|-------|----------|-------------------|----------------|------------------|
| Random Forest | **0.9995** | **1.00** | **1.00** | **1.00** |
| Logistic Regression | 0.9015 | 0.72 | 0.58 | 0.64 |
| SVM | 0.8525 | 0.82 | 0.05 | 0.09 |

**Best model:** **Random Forest** (Accuracy ≈ 99.95 %).  
Training set = 8 000 rows, Test set = 2 000 rows (class-stratified).

### 3 . Energy-Savings Analysis  
- **Total energy:** 150 217.83 kWh  
- **Detected waste:** 28 374.81 kWh (**18.89 %**)  
- **Potential cost savings:** \$2 837.48 (assuming \$0.10 / kWh)  

### 4 . Key Insights  
- Waste events are concentrated during late-night hours (22:00 – 05:00).  
- HVAC and lighting ratios are the strongest predictors in the Random Forest feature importance.  
- Extremely high model accuracy indicates clear separability between waste and normal patterns in this dataset.

### 5 . Challenges & Mitigations  
- **Class imbalance** (≈ 15 % waste): stratified split + tree-based model handled it well.  
- **Overfitting risk:** validated with unseen 20 % test set (still 99.95 % accuracy).  
- Logistic Regression and SVM under-performed due to non-linear relationships in features.

---

## Next Steps (Week 3 Preview)  
1. **Hyper-tune Random Forest** (n _estimators, max_depth) and test Gradient-Boosting / XGBoost.  
2. **Deploy** a rule-based alert system using the trained model for real-time monitoring.  
3. **Optimize energy-saving recommendations** (e.g., adjust HVAC set-points, schedule equipment) and estimate ROI over a full year.  
4. **Dashboard**: interactive visualization of live energy vs. predicted waste.

---

*Filed by **Dhanuja K S E** – Edunet AI/ML Internship*  
