# Intelligent Detection and Elimination of Energy Waste in Healthcare Facilities

## Edunet AIML Internship - Progress Submission

---

## Problem Statement

Healthcare facilities waste **30-40%** of energy during non-critical operating hours such as nights, weekends, and low-occupancy periods due to:

- Medical equipment running unnecessarily
- HVAC systems maintaining full capacity even in empty wards
- Lighting systems not adapting to actual occupancy
- Lack of intelligent scheduling for non-critical energy loads

This project aims to develop **machine learning models** to distinguish between **critical and non-critical energy consumption**, optimizing only the non-critical usage without compromising patient safety.

---

## Dataset

Used the **Hospital Energy Saving System Dataset** from Kaggle:

- 10,000 rows, 25 columns  
- Detailed healthcare-specific patient monitoring and energy consumption data  
- Includes HVAC, lighting, medical equipment power usage, environmental conditions, and operational modes  
- Timestamped every 5 minutes  
- Includes patient vitals and AI predicted health statuses  

Dataset link: [Hospital Energy Saving System Dataset - Kaggle](https://www.kaggle.com/datasets/ziya07/hospital-energy-saving-system-dataset)

---

## Data Loading and Cleaning

- Loaded dataset using `pandas`
- Verified column names and data types
- Converted `Timestamp` column to datetime format
- Extracted time features: Hour, Day of Week, Month
- Checked for missing/duplicate values — none found

---

## Feature Engineering

- Labeled **critical hours** as weekdays between 6 AM and 10 PM  
- Created **energy waste indicator** for high energy consumption during non-critical hours (above 70th percentile)  
- Calculated HVAC, medical equipment, and lighting power usage ratios relative to total power usage  

---

## Sample Code

import pandas as pd
import numpy as np

Load dataset
df = pd.read_csv('hospital_communication_energy_system.csv')

Convert Timestamp to datetime
df['Timestamp'] = pd.to_datetime(df['Timestamp'])

Extract time features
df['Hour'] = df['Timestamp'].dt.hour
df['Day_of_Week'] = df['Timestamp'].dt.dayofweek

Label critical hours (weekday daytime)
df['Critical_Hours'] = np.where(
(df['Hour'].between(6, 22)) & (df['Day_of_Week'] < 5), 1, 0)

Define energy waste (high energy during non-critical hours)
threshold = df['Energy Consumption (kWh)'].quantile(0.7)
df['Energy_Waste'] = np.where(
(df['Critical_Hours'] == 0) & (df['Energy Consumption (kWh)'] > threshold), 1, 0)

Feature ratios
df['HVAC_to_Total_Ratio'] = df['HVAC Power Usage (kWh)'] / df['Total Power Usage (kWh)']
df['Medical_to_Total_Ratio'] = df['Medical Equipment Power Usage (kWh)'] / df['Total Power Usage (kWh)']
df['Lighting_to_Total_Ratio'] = df['Lighting Power Usage (kWh)'] / df['Total Power Usage (kWh)']


---

## Results So Far

- Created healthcare-specific time and energy waste features  
- Identified approx. 1,532 energy waste records during non-critical hours  
- Dataset fully cleaned with no missing values  
- Ready for EDA, model training, and optimization  

---

## Next Steps

- Exploratory Data Analysis to visualize patterns  
- Train ML models to detect energy waste periods  
- Develop optimization methods to reduce non-critical energy consumption  
- Estimate energy and cost savings for healthcare facilities  

---

## Personal Statement

This internship project has enhanced my skills in applying machine learning and data engineering to real-world energy optimization problems in healthcare. It combines domain knowledge with data science to deliver impactful solutions that drive sustainability without compromising patient safety.

---

Thank you for reviewing my progress!

---

*Filed by [Your Name]*  
*Edunet AI/ML Internship Program*  
