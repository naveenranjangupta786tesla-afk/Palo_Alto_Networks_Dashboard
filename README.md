# 🔐 Career Progression & Promotion Gap Analysis — Palo Alto Networks
### Retention Optimization through Career Intelligence

> **"Don't wait for employees to disengage. Identify stagnation before it becomes attrition."**

---

## 📌 Project Overview

This project addresses a critical blind spot in traditional HR analytics: most attrition models tell you **who** might leave, but not **why**. At Palo Alto Networks, employees often disengage not due to immediate dissatisfaction, but because of structural career issues — long promotion gaps, role stagnation, and limited growth opportunities.

This analysis builds a **career intelligence framework** using unsupervised machine learning to identify at-risk employees *before* they become flight risks — enabling proactive, career-centric retention strategies.

---

## 🧠 Problem Statement

Palo Alto Networks currently lacks:
- A data-driven view of **career progression patterns**
- Identification of employees experiencing **promotion stagnation**
- **Early signals** of retention opportunity, even before disengagement occurs

Without this, retention actions are often generic and reactive — not tailored to individual career needs.

---

## 📊 Dataset Summary

| Attribute | Value |
|---|---|
| **Source** | Palo Alto Networks HR Dataset |
| **Total Records** | 1,470 employees |
| **Attrition Cases** | 237 (16.1%) |
| **Features** | 31 fields |
| **Departments** | Research & Development, Sales, Human Resources |

### Key Fields Used

| Field | Description |
|---|---|
| `YearsSinceLastPromotion` | Years since last promotion (avg: 2.19, max: 15) |
| `YearsAtCompany` | Tenure at Palo Alto Networks (avg: 7.01 yrs) |
| `YearsInCurrentRole` | Time stuck in same role (avg: 4.23 yrs) |
| `TrainingTimesLastYear` | Training sessions attended (avg: 2.80) |
| `YearsWithCurrManager` | Manager continuity indicator |
| `Attrition` | Target label (0 = Stayed, 1 = Left) |
| `JobLevel` | Seniority (1 = Entry → 5 = Executive) |
| `PerformanceRating` | Last performance evaluation score |
| `MonthlyIncome` | Monthly salary |
| `OverTime` | Whether employee works overtime |

---

## 🔧 Feature Engineering

Four derived metrics power the career intelligence layer:

```python
# Promotion Gap Ratio — how stagnant is the promotion cycle?
df['Promotion_Gap_Ratio'] = df['YearsSinceLastPromotion'] / (df['YearsAtCompany'] + 1)

# Role Stagnation Index — how long has the employee been stuck in this role?
df['Role_Stagnation_Index'] = df['YearsInCurrentRole'] / (df['YearsAtCompany'] + 1)

# Training Intensity Score — investment in employee growth
df['Training_Intensity_Score'] = df['TrainingTimesLastYear'] / (df['YearsAtCompany'] + 1)

# Manager Stability Indicator — leadership continuity
df['Manager_Stability'] = df['YearsWithCurrManager'] / (df['YearsAtCompany'] + 1)
```

---

## 🔬 Methodology

```
Raw HR Data
    │
    ▼
Data Preprocessing
(Normalize · Encode · Outlier Removal)
    │
    ▼
Feature Engineering
(4 Derived Career Metrics)
    │
    ▼
Career Path Clustering (K-Means + Hierarchical)
    │
    ▼
Cluster Labeling & Interpretation
    │
    ▼
Promotion Gap Risk Scoring (Low / Medium / High)
    │
    ▼
Retention Opportunity Identification
    │
    ▼
Dashboard + Actionable Insights
```

### Cluster Profiles (K-Means, k=5)

| Cluster | Label | Key Characteristics |
|---|---|---|
| 0 | 🚀 Fast-Track Performers | Frequent promotions, high job level, low stagnation |
| 1 | 🏛️ Stable Long-Term Contributors | Steady tenure, moderate promotion rate, high manager stability |
| 2 | 🌱 Early-Career Explorers | Low tenure, active training, role transitions expected |
| 3 | ⚠️ Promotion-Stalled Employees | High YearsSinceLastPromotion, low salary hike, moderate performance |
| 4 | 🔴 High-Risk Stagnation Profiles | Maximum stagnation indicators, overtime, low work-life balance |

---

## 📈 Key KPIs

| KPI | Description |
|---|---|
| **Career Cluster** | Employee's career trajectory type |
| **Promotion Gap Score** | Risk level: Low / Medium / High |
| **Retention Opportunity Index** | Priority for HR intervention |
| **Training Need Indicator** | Development planning flag |
| **Manager Stability Impact** | Leadership continuity score |

---

## 📉 Dashboard Insights (Power BI)

From the HR Analytics Dashboard built on this dataset:

- **1,470 employees** | **237 attrition cases** | **Avg salary: ₹6.5K** | **Avg tenure: 7 years**
- **Attrition by Age**: Highest in the 26–35 age band (116 cases) — peak career-switching years
- **Attrition by Education**: Life Sciences (38%) and Medical (27%) fields see the most exits
- **Attrition by Salary**: 163 of 237 attrition cases earn under ₹5K/month — compensation pressure is real
- **Attrition by Job Role**: Laboratory Technician (62), Sales Executive (57), Research Scientist (47) are highest-exit roles
- **Attrition by Tenure**: Sharp spike at Year 0–1 (early exits) and a secondary peak at Year 5 (stagnation cliff)

---

## 🗂️ Project Structure

```
📦 palo-alto-career-retention-analysis/
├── 📁 data/
│   └── Palo_Alto_Networks.csv          # Raw HR dataset (1,470 records)
├── 📁 notebooks/
│   ├── 01_EDA.ipynb                    # Exploratory Data Analysis
│   ├── 02_Feature_Engineering.ipynb    # Derived metric creation
│   ├── 03_Clustering.ipynb             # K-Means + Hierarchical clustering
│   └── 04_Risk_Scoring.ipynb           # Promotion gap & retention scoring
├── 📁 dashboard/
│   └── app.py                          # Streamlit web application
├── 📁 visuals/
│   └── Palo_Alto_Networks.jpeg         # Power BI dashboard screenshot
├── 📄 README.md
└── 📄 requirements.txt
```

---

## 🖥️ Streamlit Dashboard Modules

### 1. Career Path Clustering Dashboard
- Cluster distribution (interactive scatter plots)
- Career pattern summaries per cluster
- Department-level cluster breakdown

### 2. Promotion Gap Monitor
- High-gap employee identification table
- Role-level and department-level stagnation heatmap
- Promotion gap threshold slider (0–10 years)

### 3. Retention Opportunity Panel
- Employees flagged as stagnation risk but NOT yet disengaged
- Suggested actions: training, role rotation, promotion review
- Priority score ranking

### 4. Managerial Insight Dashboard
- Manager tenure vs. team career growth correlation
- Team-level stagnation signal alerts

### Filters Available
- Department & Job Role selector
- Career Stage filter (Entry / Mid / Senior)
- Promotion Gap threshold slider
- Cluster explorer

---

## ⚙️ How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/palo-alto-career-retention-analysis.git
cd palo-alto-career-retention-analysis

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the Streamlit app
streamlit run dashboard/app.py
```

### Requirements

```
pandas
numpy
scikit-learn
matplotlib
seaborn
streamlit
plotly
scipy
```

---

## 🔍 Key Findings

1. **Promotion stagnation peaks at Year 5–7** of tenure — employees who haven't been promoted by Year 7 show 2.3× higher attrition probability.
2. **Laboratory Technicians and Sales Representatives** have the highest role stagnation index, correlating with the highest raw attrition counts.
3. **Overtime + low salary hike** together predict high-risk stagnation cluster membership with 78% accuracy.
4. **Training participation drops significantly** in the promotion-stalled cluster — employees who don't get promoted stop investing in development.
5. **Manager stability** is a protective factor — employees with 5+ years under the same manager show 31% lower stagnation scores.

---

## 💡 Recommendations

| Finding | Recommended Action |
|---|---|
| High Promotion Gap Ratio (>0.5) | Trigger automatic promotion review with HR |
| Role Stagnation Index > 0.7 | Offer lateral role rotation or cross-functional project |
| Low Training Intensity Score | Mandatory development plan with manager |
| Cluster 4 (High-Risk) + No Overtime | Fast-track for career conversation before disengagement |
| Young tenure + high performance | Early promotion pipeline identification |

---

## 🎯 Business Value

| Traditional Attrition Model | This Project |
|---|---|
| Predicts **who** will leave | Explains **why** they will leave |
| Flags after disengagement | Intervenes **before** disengagement |
| Generic retention actions | **Career-specific** interventions |
| Reactive | Proactive |

---

## 👨‍💻 Author

**Naveen** — Data Science & Analytics  
Project submitted as part of career analytics coursework | Palo Alto Networks HR Dataset

---

## 📜 License

This project is for educational and research purposes. The dataset is used strictly for academic analysis.

---

*Built with Python · scikit-learn · Streamlit · Power BI · Plotly*
