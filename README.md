# Uplift Modeling & A/B Testing Simulation

> [!IMPORTANT]
> **Project Status: Active / Work in Progress**  
> This project is currently under active development. The results and models presented below are preliminary and subject to refinement.

## 📌 Project Overview

**Goal:** Maximize incremental conversions by targeting the *right* customers—those who are persuaded by promotions—while avoiding "Sleeping Dogs" (customers who react negatively to promotions) and "Sure Things" (customers who buy regardless).

This project simulates an **A/B Test** and implements **Uplift Modeling** (using the T-Learner approach) to estimate the Conditional Average Treatment Effect (CATE). By shifting from traditional "average treatment effect" to "individual treatment effect," we aim to optimize promotional spend and increase overall ROI.

## 🚀 Key Features & Methodology

*   **A/B Test Simulation:**
    *   Simulated a randomized controlled trial (RCT) by assigning a binary treatment variable.
    *   Evaluated the Average Treatment Effect (ATE) using difference-in-means.
*   **Uplift Modeling (T-Learner):**
    *   Implemented a **T-Learner** meta-learner using **Logistic Regression**.
    *   Modeled the control and treatment response functions separately to estimate individual uplift.
*   **Customer Segmentation:**
    *   Analyzed "Persuadables," "Sleeping Dogs," "Lost Causes," and "Sure Things" based on predicted uplift.
*   **Data Processing:**
    *   Cleaned and preprocessed the [Online Retail Dataset](https://archive.ics.uci.edu/dataset/352/online+retail).
    *   Engineered RFM (Recency, Frequency, Monetary) features to capture customer behavior.

## 📊 Preliminary Results

### A/B Test Findings
*   **Conversion Rate Lift:** The treatment group showed a **0.56%** increase in conversion rate compared to the control group.
*   **Statistical Significance:** The p-value was **0.73**, indicating that the overall average impact of the promotion was *not* statistically significant across the entire population. This highlights the need for targeted (uplift) modeling.

### Uplift Model Insights (T-Learner)
We observed heterogeneous treatment effects across customer deciles:
*   **Sleeping Dogs (Deciles 0-3):** Customers in these segments had a *negative* uplift (approx. -1.0), meaning the promotion actively reduced their likelihood to convert.
*   **Persuadables (Deciles 5-9):** High positive uplift (up to +1.0), indicating these customers are strong candidates for the promotion.

> **Business Insight:** Treating the entire population is inefficient. By targeting only the top deciles (Persuadables), we can avoid wasting budget on "Sure Things" and alienating "Sleeping Dogs."

## 🛠️ Tech Stack

*   **Python:** Core programming language.
*   **Pandas & NumPy:** Data manipulation and numerical operations.
*   **Scikit-learn:** Machine learning models (Logistic Regression) and evaluation metrics.
*   **Matplotlib & Seaborn:** Data visualization.

## 📂 Project Structure

```
A-B Testing/
├── data/                   # Dataset files (Raw and Cleaned)
│   ├── Online Retail.xlsx
│   ├── Customer.csv
│   └── cleaned_data.csv
├── notebooks/              # Jupyter Notebooks
│   ├── data_cleaning.ipynb       # Data preprocessing
│   ├── feature_engineering.ipynb # RFM feature creation
│   ├── AB_Test.ipynb             # A/B Test simulation & analysis
│   └── T-learner.ipynb           # Uplift modeling (T-Learner)
├── .venv/                  # Virtual environment
└── README.md               # Project documentation
```

## 🗓️ Roadmap

- [ ] **Advanced Models:** Implement **XGBoost** and **Causal Forest** for more robust uplift estimation.
- [ ] **Evaluation:** Plot Qini curves and calculate Qini coefficients to quantify model performance.
- [ ] **Feature Engineering:** meaningful feature creation beyond basic RFM.
- [ ] **Deployment:** Create a simple API to serve uplift predictions.

## 💻 Usage

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd A-B-Testing
    ```
2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt 
    # (Note: manually install pandas, numpy, scikit-learn, openpyxl if requirements.txt is missing)
    ```
3.  **Run the notebooks:**
    Start with `data_cleaning.ipynb`, then `feature_engineering.ipynb`, followed by the analysis notebooks.

---
*Created for portfolio demonstration*
