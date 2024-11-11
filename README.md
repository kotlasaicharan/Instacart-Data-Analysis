# Instacart-Data-Analysis
## Introduction
Instacart is an American technology company that operates as a same-day grocery delivery and pick-up service in the U.S. and Canada. Customers shop for groceries through the Instacart mobile app or Instacart.com from various retailer partners. The order is shopped and delivered by an Instacart personal shopper

## Objectives
- Analyze the anonymized [DATA](https://www.kaggle.com/c/instacart-market-basket-analysis/data) of 3 million grocery orders from more than 200,000 Instacart users open-sourced by Instacart.
- Find out the hidden associations between products for better cross-selling and upselling.
- Build a machine learning model to predict which previously purchased product will be placed in the user’s next order.

## Repo details
```
├── Plots/                                      : Contains all plots 
├── Instacart Data Analysis.ipynb               : Initial analysis to understand data
├── Instacart EDA.ipynb                         : EDA to analyze customer purchase pattern
├── Instacart Market Basket Analysis.ipynb      : Market Basket Analysis to find products association
├── Instacart Feature Extraction.ipynb          : Feature engineering and extraction for a ML model
├── Instacart data preparation.ipynb            : Data preparation for modeling
├── Instscart XGBoost Model.ipynb               : XGBoost model for product reorder prediction
└── README.md                                   : Project Report
```

## Data Description
- **aisles**: This file contains different aisles and there are total 134 unique aisles.

- **departments**: This file contains different departments and there are total 21 unique departments.

- **orders**: This file contains all the orders made by different users.
  - There are total 3421083 orders made by total 206209 users.
  - There are three sets of orders: Prior, Train and Test. The distributions of orders in Train and Test sets are similar whereas the distribution of orders in Prior set is different.
  - The total orders per customer ranges from 0 to 100.
          ![image](https://github.com/user-attachments/assets/8fafeee9-c246-45dd-b311-91aa98471ce8)
  - kjdfhvhfvhef
  - kjnvjfvefj




