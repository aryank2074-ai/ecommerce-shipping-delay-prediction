# ecommerce-shipping-delay-prediction
# 📦 E-Commerce Shipping Delay Prediction

Exploratory data analysis (EDA) of an e-commerce shipping dataset to understand what factors are associated with products **not reaching customers on time**, as groundwork for a delivery-delay prediction model.

---

## 📌 Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Analysis Workflow](#analysis-workflow)
- [Key Findings](#key-findings)
- [Roadmap](#roadmap)
- [License](#license)

---

## Overview

Late deliveries hurt customer satisfaction and increase support load. This project explores an e-commerce shipping dataset to answer questions such as:

- How many shipments arrive late, and is it a big problem?
- Does the **mode of shipment** (Ship / Flight / Road) affect delays?
- Do **warehouse blocks** or **product importance** show different delay patterns?
- Which numerical features (cost, discount, weight, ratings, etc.) separate on-time from delayed orders?

## Dataset

- **Rows:** 10,999 orders
- **Columns:** 12 (no missing values)
- **Target:** `Reached.on.Time_Y.N` → `0` = reached on time, `1` = delayed

| Column | Type | Description |
|---|---|---|
| `ID` | int | Unique order ID |
| `Warehouse_block` | categorical | Warehouse block (A, B, C, D, F) |
| `Mode_of_Shipment` | categorical | Ship, Flight, or Road |
| `Customer_care_calls` | int | Number of calls made to enquire about the shipment |
| `Customer_rating` | int | Customer rating (1–5) |
| `Cost_of_the_Product` | int | Product cost |
| `Prior_purchases` | int | Number of previous purchases |
| `Product_importance` | categorical | low, medium, or high |
| `Gender` | categorical | F or M |
| `Discount_offered` | int | Discount offered on the product |
| `Weight_in_gms` | int | Product weight in grams |
| `Reached.on.Time_Y.N` | int | Target variable (see above) |

> The dataset is not included in this repo. Download the training file (`Train.csv`) from the source you obtained it from (commonly the Kaggle "Customer Analytics / E-Commerce Shipping Data" dataset) and place it in the `data/` folder.

## Project Structure

```
ecommerce-shipping-delay-prediction/
├── data/
│   └── Train.csv                          # dataset (add manually)
├── notebooks/
│   └── Ecomm_Shipping_Prediction.ipynb    # EDA notebook
├── requirements.txt
└── README.md
```

## Tech Stack

- Python 3
- pandas, NumPy
- Matplotlib, Seaborn
- Jupyter Notebook

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<aryank2074-a>/ecommerce-shipping-delay-prediction.git
cd ecommerce-shipping-delay-prediction

# 2. (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add the dataset to data/Train.csv, then launch Jupyter
jupyter notebook
```

> **Note:** The notebook reads the file as `Train (2).csv`. Update the path in the `pd.read_csv(...)` cell to `data/Train.csv` (or match your filename).

**`requirements.txt`**
```
pandas
numpy
matplotlib
seaborn
jupyter
```

## Analysis Workflow

1. **Data inspection** – shape, dtypes, missing values, summary statistics
2. **Univariate analysis** – box plots, histograms with KDE, category counts
3. **Correlation analysis** – heatmap of numerical features
4. **Bivariate analysis** – categorical features and numerical distributions vs. the target
5. **Insight generation** – on-time vs. delayed rates by shipment mode, product importance, and warehouse block

## Key Findings

- **Data quality is good:** 10,999 rows, no missing values, appropriate data types.
- **Delays are common:** 6,563 orders (~59.7%) were delayed vs. 4,436 (~40.3%) delivered on time.
- **Shipment mode:** Ship carries the bulk of orders (7,462 of 10,999), but the delay *rate* is nearly identical across modes (~59–60% for Ship, Flight and Road), so mode alone doesn't explain delays.
- **Warehouse block:** Block F handles about double the volume of the others (3,666 orders), yet delay rates are similar across all blocks (~59–60%).
- **Product importance:** High-importance products show a somewhat higher delay rate (~65%) than low/medium (~59%), though they make up only 948 orders.
- **Class balance:** The target is moderately imbalanced (≈60/40), which is worth handling during modeling.

## Roadmap

- [ ] Feature encoding and scaling
- [ ] Train/test split and baseline models (Logistic Regression, Decision Tree, Random Forest, XGBoost)
- [ ] Evaluate with accuracy, precision, recall, F1, ROC-AUC
- [ ] Hyperparameter tuning and feature importance analysis
- [ ] Save the best model and build a simple prediction app

