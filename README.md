# Hospital-readmission-analysis-python
HOSPITAL READMISSION DASHBOARD

An end-to-end Python data analysis and visualization dashboard designed to analyze patient readmission rates, demographics, health metrics, and key risk factors within a healthcare setting.

---

## 📌 Project Overview
Hospital readmission within 30 days is a critical quality metric in healthcare management. High readmission rates reflect operational inefficiencies and increased healthcare costs. 

This project provides a comprehensive exploratory data analysis (EDA) and interactive/visual dashboard using **Python, Pandas, Seaborn, and Matplotlib**. The analysis processes **30,000 patient records** to evaluate key healthcare parameters such as age distribution, pre-existing conditions (Diabetes, Hypertension), Body Mass Index (BMI), Length of Stay (LOS), and cholesterol levels to identify patterns driving readmissions.

---

## 📊 Key Performance Indicators (KPIs)
Based on the dashboard summary metrics:

| Metric | Value | Description |
| :--- | :--- | :--- |
| **Total Patients** | `30,000` | Total cohort size analyzed |
| **Readmission Rate** | `12.25%` | Patients readmitted within 30 days (`3,674` patients) |
| **Average Age** | `53.9 Years` | Average age across the patient sample |
| **Average BMI** | `28.9` | Borderline overweight demographic average |
| **Average Stay** | `5.5 Days` | Mean duration of initial hospital admission |
| **Avg Cholesterol** | `225.3 mg/dL` | Mean cholesterol level across patients |

---

## 📈 Visualizations & Insights

The dashboard is structured into 9 analytical modules:

1. **Gender Distribution**: Balanced distribution across Male (`10,097`), Female (`9,879`), and Other (`10,024`) demographics.
2. **Readmission Status**: High proportion of non-readmitted patients (`26,326`) vs. 30-day readmissions (`3,674`).
3. **Age Group Breakdown**: The highest patient density belongs to the `65+` elderly group (`10,244`), followed by `19–35` (`7,034`).
4. **Diabetes vs. Readmission**: Higher proportion of readmissions among diabetic patients (`1,976`) compared to non-diabetic patients (`1,698`).
5. **Hypertension vs. Readmission**: Hypertensive patients exhibit a higher readmission count (`1,945`) than non-hypertensive patients (`1,729`).
6. **BMI Distribution**: Uniformly distributed BMI across range 18 to 40, centered near the sample mean of 28.9.
7. **Length of Stay (LOS)**: Standard distribution of hospital stay duration ranging between 1 and 10 days.
8. **Cholesterol Levels**: Uniform spread ranging between 150 mg/dL and 300 mg/dL.
9. **Correlation Heatmap**: Evaluates linear correlations among numeric attributes (`age`, `cholesterol`, `bmi`, `medication_count`, `length_of_stay`).

---

## 🛠️ Tech Stack & Libraries

- **Language:** Python 3.x
- **Data Manipulation:** `pandas`, `numpy`
- **Data Visualization:** `matplotlib`, `seaborn`

---

## 📁 Repository Structure

```text
├── data/
│   └── hospital_readmission_data.csv[hospital.csv](https://github.com/user-attachments/files/30390864/hospital.csv)
   # Dataset containing patient records
├── assets/
│   └── hospital_final_dashboard.png  <img width="1920" height="1200" alt="hospital final dashboard" src="https://github.com/user-attachments/assets/84ec75b1-0e2f-43ce-a549-de96d726b6ca" />
  # Dashboard visualization export
```

---

## 🚀 How to Run the Project

### 1. Clone the Repository
```bash
git clone https://github.com/your-username/hospital-readmission-dashboard.git
cd hospital-readmission-dashboard
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the Dashboard Code
Execute the code in Jupyter Notebook / Google Colab or run as a Python script:
```bash
python dashboard.py
```

---

## 💻 Dashboard Python Code

```python
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns

# Load Dataset (Ensure your dataset path is correctly set)
# df = pd.read_csv("hospital_readmission_data.csv")

# KPI Calculations
total_patients = len(df)
readmission_rate = (df["readmitted_30_days"] == "Yes").mean() * 100
avg_age = df["age"].mean()
avg_bmi = df["bmi"].mean()
avg_chol = df["cholesterol"].mean()
avg_stay = df["length_of_stay"].mean()

# Figure Layout Setup
fig = plt.figure(figsize=(22, 15))
fig.suptitle(
    "Hospital Readmission Analysis Dashboard", fontsize=22, fontweight="bold"
)

# KPI Cards
fig.text(
    0.05,
    0.92,
    f"Total Patients\n{total_patients}",
    fontsize=14,
    bbox=dict(facecolor="skyblue", edgecolor="black", boxstyle="round"),
)
fig.text(
    0.21,
    0.92,
    f"Readmission Rate\n{readmission_rate:.2f}%",
    fontsize=14,
    bbox=dict(facecolor="lightcoral", edgecolor="black", boxstyle="round"),
)
fig.text(
    0.37,
    0.92,
    f"Average Age\n{avg_age:.1f}",
    fontsize=14,
    bbox=dict(facecolor="lightgreen", edgecolor="black", boxstyle="round"),
)
fig.text(
    0.52,
    0.92,
    f"Average BMI\n{avg_bmi:.1f}",
    fontsize=14,
    bbox=dict(facecolor="khaki", edgecolor="black", boxstyle="round"),
)
fig.text(
    0.67,
    0.92,
    f"Average Stay\n{avg_stay:.1f} Days",
    fontsize=14,
    bbox=dict(facecolor="plum", edgecolor="black", boxstyle="round"),
)
fig.text(
    0.83,
    0.92,
    f"Avg Cholesterol\n{avg_chol:.1f}",
    fontsize=14,
    bbox=dict(facecolor="orange", edgecolor="black", boxstyle="round"),
)

# 1. Gender Distribution
plt.subplot(3, 3, 1)
ax = sns.countplot(data=df, x="gender")
for c in ax.containers:
    ax.bar_label(c)
plt.title("Gender Distribution")

# 2. Readmission Status
plt.subplot(3, 3, 2)
ax = sns.countplot(data=df, x="readmitted_30_days")
for c in ax.containers:
    ax.bar_label(c)
plt.title("Readmission Status")

# 3. Age Group
plt.subplot(3, 3, 3)
ax = sns.countplot(data=df, x="age_group")
for c in ax.containers:
    ax.bar_label(c)
plt.title("Age Group")

# 4. Readmission by Diabetes
plt.subplot(3, 3, 4)
dia = pd.crosstab(df["diabetes"], df["readmitted_30_days"])
ax = dia.plot(kind="bar", ax=plt.gca())
for c in ax.containers:
    ax.bar_label(c)
plt.title("Readmission by Diabetes")

# 5. Readmission by Hypertension
plt.subplot(3, 3, 5)
hyp = pd.crosstab(df["hypertension"], df["readmitted_30_days"])
ax = hyp.plot(kind="bar", ax=plt.gca())
for c in ax.containers:
    ax.bar_label(c)
plt.title("Readmission by Hypertension")

# 6. BMI Distribution
plt.subplot(3, 3, 6)
sns.histplot(df["bmi"], bins=20, kde=True)
plt.title("BMI Distribution")

# 7. Length of Stay
plt.subplot(3, 3, 7)
sns.histplot(df["length_of_stay"], bins=20, kde=True)
plt.title("Length of Stay")

# 8. Cholesterol Distribution
plt.subplot(3, 3, 8)
sns.histplot(df["cholesterol"], bins=20, kde=True)
plt.title("Cholesterol Distribution")

# 9. Correlation Heatmap
plt.subplot(3, 3, 9)
corr = df.select_dtypes(include=["int64", "float64"]).corr()
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f", cbar=False)
plt.title("Correlation Heatmap")

plt.tight_layout(rect=[0, 0, 1, 0.90])
plt.show()
```

---

## 🎯 Recommendations & Strategic Takeaways
- **Target High-Risk Conditions:** Patients with **Diabetes** and **Hypertension** exhibit proportionally higher 30-day readmissions. Priority follow-up programs should focus on these pre-existing conditions.
- **Elderly Care Optimization:** Over 34% of patients belong to the **65+ age group** (`10,244`), indicating that post-discharge support and home health monitoring for seniors can substantially reduce readmission rates.

---
*Created as part of Healthcare Data Analytics Portfolio Project.*
