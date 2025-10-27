# 🧠 Case Study – *Post-Pandemic Remote Work Health Impact (Week 6 – 7)* 


### 📘 **Context**

The **Post-Pandemic Remote Work Health Impact 2025** dataset captures how remote, hybrid, and on-site work arrangements affect employee well-being in the post-COVID era.

Collected globally across six continents in June 2025, it reflects diverse age groups, industries, and job roles — providing a broad view of how work habits intersect with mental and physical health.

---

### 🧩 **Data Preparation and Cleaning (Excel + Power BI Phase)**

1. **Initial Cleaning in Excel**
    - Checked for duplicates — none found.
    - Dropped the `Survey_Date` column as the time range was narrow and added no insight.
    - Split `Salary_Range` (e.g., "$40K–60K") into two columns, took the average to create a new `Average_Salary` metric.
    - Added a **Reference Index** as a primary key to maintain table relationships in Power BI.
2. **Handling Multi-Value Columns**
    - The `Physical_Health_Issues` column had multiple issues in a single cell (e.g., "Back Pain; Shoulder Pain; Neck Pain").
    - Created a separate table containing these issues and later used **Split Text → Rows** in Power BI to expand them properly for visualization.
3. **Dashboard Construction in Power BI**
    - Initially struggled with layout and slicer interactions, especially when many customer or postal records overlapped.
    - Discovered duplicate relationships between Region, State, and City, later removed through the **Power Query Editor**.
    - Designed KPIs combining **Average Hours per Week**, **Salary Trend**, and **Burnout Count**, plus a **Gauge Chart** for *Average Work-Life Balance Score* and a **Card** for *Average Salary*.
    - Final dashboard successfully connected mental health, workload, and compensation metrics — one of my cleanest dashboards yet.

Burnout is widespread across industries, with a significant percentage of employees experiencing it, and it is often driven by high workload, lack of support, and poor work-life balance. While levels vary, many studies show over one-third of employees report high burnout

### 📊 Key Insights

- **Professional Services** and **Technology** industries showed the **highest average work hours**, often linked with higher burnout levels.
- Average **Work-Life Balance Score = 3.0**, meaning employees are moderately satisfied.
- **Average Salary = 78.03K USD**, but industries with higher salaries didn’t necessarily have better work-life balance.
- **Burnout levels** were notably higher in regions like **South America**, **Africa** and **Oceania**, possibly due to work-hour extremes.
- **Social Isolation Index** showed that over **29.43%** of respondents scored 3 (moderate isolation), suggesting that remote work still affects social well-being whereas only **18.09%** have good social life.

---

### 🧠 **Machine Learning Phase (Week 7)**

After completing the analytical dashboard, I reused the same dataset to explore **predictive modeling** — focusing on *Burnout Level* as the target variable.

### 🧹 **Preprocessing & Feature Engineering**

- **Dropped** `Survey_Date` (non-predictive) and kept only meaningful demographic and behavioral columns.
- **Gender Cleaning:**
    
    Normalized variations using `.str.strip().str.title()` and filtered out rare categories —
    
    *Non-Binary* (90) and *Prefer Not to Say* (32) — totaling only 3.8% of data.
    
    > "These categories were excluded to prevent bias and improve model generalization."

- **Physical & Mental Health Columns:**
    - Converted multi-value physical issues into a numerical count (`Physical_Health_Count`).
    - Instead of dropping missing mental-health data (25%), added an **"Unknown"** category to preserve integrity.
    - Mapped mental-health categories by real-world severity:
        
        ```
        Unknown:0, ADHD:1, Stress Disorder:2, Anxiety:3,
        Burnout:4, Depression:5, PTSD:6
        
        ```  
    - Mapped burnout levels as `Low:0`, `Medium:1`, `High:2`.

- **Feature Summary:**
    - **Numeric:** `Age`, `Hours_Per_Week`, `Work_Life_Balance_Score`, `Social_Isolation_Score`, `Avg_Salary`, `Physical_Health_Count`, `Mental_Health_Score`.
    - **Categorical:** `Gender`, `Region`, `Industry`, `Work_Arrangement`.
    - Encoded categorical features with **One-Hot Encoding** and standardized numeric ones using a **ColumnTransformer**.

---

### ⚙️ **Model Development**

Trained multiple models:

`LogisticRegression`, `DecisionTree`, `RandomForest`, `GradientBoost`, `SGDClassifier`, `OneVsRest SVC`, and plain `SVC`.

After hyperparameter tuning via **RandomizedSearchCV** and balancing experiments with **SMOTE**, results stabilized:

| Model | Accuracy | F1-Score | Precision | Recall |
| --- | --- | --- | --- | --- |
| **SVM (no SMOTE)** | **0.44** | **0.35** | 0.34 | 0.44 |
| Gradient Boost | 0.43 | 0.43 | 0.44 | 0.43 |
| Random Forest | 0.42 | 0.42 | 0.43 | 0.42 |

> Observation: Despite moderate metrics, SVM achieved the most balanced and consistent results across all folds.

---

### 📊 **Interpretation**

- The dataset is **subjective and noisy**, reflecting real-world mental-health variability.
- Traditional accuracy metrics are misleading; **recall and interpretability** matter more here.
- Beyond 45% accuracy, further tuning yielded diminishing returns — a clear case of **data limitation, not model weakness**.

---

### 💭 **Reflection**

> "When I saw Sam Altman talk about taking time to bring GPT-8 into the healthcare domain, I finally understood why. Even this small-scale mental-health dataset was messy, uncertain, and imbalanced. Scaling such complexity to real-world data would be exponentially harder. Data in healthcare isn't just big — it's unpredictable, emotional, and deeply human."

---

### 🧾 **Summary**

- Built full analytics pipeline: cleaning → dashboard → ML modeling.
- Learned how subjective data challenges even advanced algorithms.
- Understood the trade-off between interpretability and performance in health-related AI.

> Final Verdict: Gradient Boost and SVM offered the most balanced and realistic predictions. The case underscores how data quality, not algorithm choice, often defines success in real-world analytics.

