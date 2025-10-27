# 🧠 Post-Pandemic Remote Work Health Impact (2025)

### 📌 Overview

This project explores how remote, hybrid, and onsite work arrangements influence employees’ **mental and physical health** in the post-pandemic era.
The dataset includes responses from different regions, industries, and job roles worldwide — collected in **June 2025**.

I used this dataset to:

* 🧹 Clean and preprocess data in **Excel & Python**
* 📊 Build an interactive **Power BI dashboard**
* 🤖 Train machine learning models to predict **Burnout Level**

---

### ⚙️ Project Workflow

1. **Data Cleaning & Feature Engineering**

   * Processed `Salary_Range` to extract average salary
   * Quantified `Physical_Health_Issues` and encoded `Mental_Health_Status`
   * Removed rare gender categories for balance

2. **Visualization**

   * Created Power BI dashboard with KPIs for *Work-Life Balance*, *Hours per Week*, and *Average Salary*
   * Added dynamic slicers for interactive filtering

3. **Machine Learning**

   * Tested multiple classifiers: Logistic Regression, Random Forest, SVM, XGBoost, etc.
   * **Best Model:** Despite moderate metrics, SVM achieved the most balanced and consistent results across all folds.

---

### 🔗 Resources

* 📘 **Case Study:** [View Full Case Study (PDF)](docs/case_study.md)
* 📊 **Dashboard Screenshot:** [View Dashboard](output/Impact_Dashboard.png)
* 📂 **Dataset Source (Kaggle):** [Post-Pandemic Remote Work Health Impact 2025](https://www.kaggle.com/datasets/pratyushpuri/remote-work-health-impact-survey-2025)

* 💻 **Notebooks:**

  * `data_preprocessing.ipynb`
  * `model.ipynb`

---

### 🧠 Key Insight

> This project highlighted how **subjective and complex** mental health data can be for predictive modeling — even advanced algorithms struggle with human unpredictability.

---

### 🧰 Tech Stack

`Python`, `Pandas`, `Scikit-learn`, `SMOTE`, `Power BI`, `Excel`
