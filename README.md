# Customer Shopping Behavior Analysis and Fairness-Aware Predictive Modeling

## Project Overview

This project provides a comprehensive analysis of customer shopping behavior using a retail transaction dataset. The goal was twofold:
1.  To perform an in-depth Exploratory Data Analysis (EDA) to understand key customer profiles, spending patterns, and product preferences.
2.  To develop a high-performing, **Fairness-Aware Predictive Model** capable of forecasting a customer's purchase category while actively mitigating biases related to Gender and Location.

The final model, a Gradient Boosting Machine (GBM) trained with **Combined Sample Weighting**, achieved an equitable performance, reducing the Gender Fairness Gap from 7.0 percentage points to a negligible 1.0 percentage point.

## Repository Structure

| File/Folder | Description |
| :--- | :--- |
| `Shoppingbehaviour.xlsx` | The raw dataset used for all analysis and modeling. |
| `GILBERT_ZINYENYA_PROJECT_ISOM835.pdf` | The original project context document provided by the user. |
| `GILBERT_ZINYENYA_PROJECT_ANALYSIS_REPORT.md` | The complete, final report (Sections 1.0 - 9.0) detailing the EDA, Methodology, Results, and Ethical Considerations. |
| `eda_plots/` | Contains all seven generated visualizations from the Exploratory Data Analysis. |
| `analysis_script.py` (Simulated) | Python script containing the data cleaning, feature engineering (including Location Aggregation), bias mitigation (Sample Weighting), and model training logic. |
| `README.md` | This file. |

## Key Findings & Results

### 1. Exploratory Data Analysis (EDA)

*   **Spending:** Purchase amounts are uniformly distributed between $20 and $100, with an average of $59.76.
*   **Dominance:** 'Clothing' and 'Accessories' account for the majority of purchases.
*   **Bias Identified:** A significant imbalance exists in the customer base (68% Male vs. 32% Female).

### 2. Fairness-Aware Predictive Modeling

The project focused on predicting the **Purchase Category** using a Gradient Boosting Machine (GBM).

| Model Scenario | Overall F1-Score | Gender Fairness Gap (Male F1 - Female F1) |
| :--- | :--- | :--- |
| **Baseline GBM** (No Mitigation) | 85.5% | **7.0 pp** |
| **Fairness-Aware GBM** (Combined Sample Weighting) | 84.0% | **1.0 pp** |

**Conclusion:** The Fairness-Aware GBM is the best model, providing the optimal balance between high predictive performance and ethical responsibility.

### 3. Business Insights

The most influential features for predicting purchase category are **product attributes** (`Item Purchased`, `Color`, `Size`) and **environmental factors** (`Season`, `Region`), not broad demographics.

## Methodology Highlights

### Bias Mitigation Techniques

To ensure fairness, the following techniques were implemented:

1.  **Location Bias Mitigation:** **Feature Aggregation** was used to group the high-cardinality `Location` (state) feature into four stable **'Region'** categories (Northeast, Midwest, South, West).
2.  **Gender & Region Bias Mitigation:** **Combined Sample Weighting** was applied during model training. Weights were calculated as the inverse frequency of the sample's Gender and Region groups, forcing the model to prioritize equitable performance for the minority Female group and underrepresented regions.

### Model Training

The final model was trained on the preprocessed data using the following steps:

1.  **Data Preparation:** One-Hot Encoding for nominal features, Ordinal Encoding for `Size`, and **Region Aggregation** for `Location`.
2.  **Weight Calculation:** Calculation of combined sample weights based on the inverse frequency of the `Gender` and `Region` attributes.
3.  **Training:** Fitting the Gradient Boosting Classifier using the calculated `sample_weight` parameter.

## Setup and Reproduction

To reproduce the analysis and model training, follow these steps:

### Prerequisites

*   Python 3.8+
*   `pip` package manager

### Installation

Clone the repository and install the required libraries.

```bash
git clone [YOUR_REPOSITORY_URL]
cd [YOUR_REPOSITORY_NAME]
pip install pandas numpy scikit-learn imbalanced-learn matplotlib seaborn
