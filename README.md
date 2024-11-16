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
  - There are a total of 3421083 orders made by a total of 206209 users.
  - There are three sets of orders: Prior, Train, and Test. The distributions of orders in Train and Test sets are similar whereas the distribution of orders in Prior set is different.
  - The total orders per customer range from 0 to 100.
  - Based on the plot of 'Orders VS Day of Week', we can map 0 and 1 as Saturday and Sunday, respectively, based on the assumption that most people buy groceries on weekends.
  - The majority of the orders are made during the day.  
  - Based on the heatmap between 'Day of Week' and 'Hour of Day,' we can say that Saturday afternoons and Sunday mornings are prime time for orders.

<p align="center">
  <img width="400" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Total%20Orders%20per%20Day%20of%20Week.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Total%20Orders%20by%20Customers.png">
</p>  



<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Day%20of%20week%20Vs%20Hour%20of%20day.png">
</p>  
  -most of the orders takes place from 8AM to 6 PM
- **products:** This file contains the list of total 49688 products and their aisle as well as department. The number of products in different aisles and different departments are different.

- **order_products_prior:** This file gives information about which products were ordered and in which order they were added in the cart. It also tells us that if the product was reordered or not.
    
    - In this file there is an information of total 3214874 orders through which total 49677 products were ordered.
    - From the 'Count VS Items in cart' plot, we can say that most of the people buy 1-15 items in an order and there were a maximum of 145 items in an order.
    - The percentage of reorder items in this set is 58.97%.

<p align="center">
  <img width="600" height="300" src=" https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Items%20in%20Cart%20in%20Prior%20set.png">
</p>  

- **order_products_train:** This file gives information about which products were ordered and in which order they were added in the cart. It also tells us that if the product was reordered or not.
    - In this file there is an information of total 131209 orders through which total 39123 products were ordered.
    - From the 'Count VS Items in cart' plot, we can say that most of the people buy 1-15 items in an order and there were a maximum of 145 items in an order.
    - The percentage of reorder items in this set is 59.86%.

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Items%20in%20Cart%20in%20Train%20set.png">
</p>
  
## Exploratory Data Analysis
For the analysis I combined all of the separate data files into one single dataframe and to fit the dataframe in my memory I reduced its size to 50% (4.1 GB to 2.0 GB) by type conversion and without loosing any information.

- This plot shows most popular aisles based on total products bought.




