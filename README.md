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
  -most of the orders takes place from 8AM to 6 PM
<p align="center">
  <img width="400" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Total%20Orders%20per%20Day%20of%20Week.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Total%20Orders%20by%20Customers.png">
</p>  

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Day%20of%20week%20Vs%20Hour%20of%20day.png">
</p>  
  
- **products:** This file contains the list of total 49688 products and their aisle as well as department. The number of products in different aisles and different departments are different.

- **order_products_prior:** This file gives information about which products were ordered and in which order they were added in the cart. It also tells us that if the product was reordered or not.
    
    - In this file there is an information of total 3214874 orders through which total 49677 products were ordered.
    - From the 'Count VS Items in cart' plot, we can say that most of the people buy 1-15 items in an order and there were a maximum of 145 items in an order.
    - The percentage of reorder items in this set is 58.97%.

<p align="center">
  <img width="600" height="300" src= "https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/Data%20Analyzation/Frequency%20of%20Items%20in%20Cart%20in%20Prior%20set.png">
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
<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Total%20Orders%20and%20Reorders%20From%20Most%20Popular%20Aisles.png">
</p>
- As we can see in plot below the reorder percentage of day-to-day food items is high and for other products such as vitamins, first-aids, beauty products, etc. reorder percentage is low. This is true as we buy only groceries regularly and do not buy those items in every order.

<p align="center">
<img width="400" height="220" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Aisles%20with%20Highest%20Reorder%20Ratio.png"> 
<img width="400" height="220" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Aisles%20with%20Lowest%20Reorder%20Ratio.png"> 
<p/>

- The below plot shows popular departments. The store layout should be in a way that popular departments are very near to each other.

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Total%20Orders%20and%20Reorders%20From%20Departments.png">
</p>

- The below plot shows most popular products. As we can see there are many organic products in the most popular products.

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Most%20Popular%20Products.png">
</p>

- We can see that there are less number of organic products, but their Mean reorder percentage is high. This tells us that we should focus more on organic products in the store.

<p align="center">
    <img width="400" height="250" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Total%20Organic%20and%20Inorganic%20products.png"/> 
    <img width="400" height="250" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Mean%20Reorder%20Ratio%20of%20Organic_Inorganic%20Products.png"/>
</p>


- We can plot add-to-cart-order and mean reorder percentage. As we can see the lower the add-to-cart-order higher is the reorder percentage. This makes sense as we mostly buy things first that are required on a day-to-day basis.

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Add%20to%20Cart%20Order%20VS%20Reorder%20Ratio.png">
</p>

- In the below plot of reorder percentage and number of product purchases, we see a ceiling effect. Many people try different product once and they do not reorder again. Also, there are users who buy certain products regularly. 

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Reorder%20Percentage%20VS%20Total%20Orders.png">
</p>

- We can see that the total unique users of products having the highest reorder ratio are only a few (1-15 only). This means that these users like these products and would buy regularly.
  

<p align="center">
  <img width="500" height="400" src= "https://github.com/archd3sai/Instacart-Market-Basket-Analysis/blob/master/Plots/reorder-df.png" >
</p>

- In the below plot of cumulative total users per product vs products, we can see that 85% of the users buy only 10000 products out of 49688 products. If we are interested in shelf space optimization, we should have only these 10000 products. Here, I assume that the profit from remaining 39688 products are not significant high. If we had prices of these products, we could have considered the products having high revenue, high reorder percentage and high total product sale.

<p align="center">
  <img width="600" height="300" src= "https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/EDA/Cumulative%20Sum%20of%20Unique%20Users.png">
</p>

## Markest Basket Analysis

Market Basket Analysis (MBA) is a data mining technique used to understand consumer purchase behavior. It is based on the idea that if a customer buys a specific set of items, they are more likely to buy other related items in the future.

Association Rule Mining is used when we want to find an association between different objects in a set, find frequent patterns in a transaction database, relational databases or any other information repository.

The most common approach to find these patterns is Market Basket Analysis, which is a key technique used by large retailers like Amazon, Flipkart, etc to analyze customer buying habits by finding associations between the different items that customers place in their “shopping baskets”. The discovery of these associations can help retailers develop marketing strategies by gaining insight into which items are frequently purchased together by customers. The strategies may include:

- Changing the store layout according to trends
- Customers behavior analysis
- Catalog Design
- Cross marketing on online stores
- Customized emails with add-on sales, etc.

### Matrices
**Support** : Its the default popularity of an item. In mathematical terms, the support of item A is the ratio of transactions involving A to the total number of transactions.

**Confidence** : Likelihood that customer who bought both A and B. It is the ratio of the number of transactions involving both A and B and the number of transactions involving B.
```
Confidence(A → B) = Support(A,B) / Support(A)
```
Example:

If bread and butter appear together in 20 transactions, and bread appears in 30 transactions
Confidence(bread → butter) = 20/30 = 0.67 or 67%
This means 67% of customers who buy bread also buy butter.

**Lift**:

Lift measures how much more likely items are to be bought together compared to by random chance.
```
Lift(A → B) = Confidence(A → B) / Support(B)
```
**Lift = 1** Items are independent

Products have no effect on each other's sales


**Lift > 1**: Positive correlation

Products complement each other
Example: Lift = 2 means customers are twice as likely to buy B when they buy A


**Lift < 1**: Negative correlation

Products substitute each other.
Example: Lift = 0.5 means customers are half as likely to buy B when they buy A

**Apriori Algorithm:** Apriori algorithm assumes that any subset of a frequent itemset must be frequent. Its the algorithm behind Market Basket Analysis. Say, a transaction containing {Grapes, Apple, Mango} also contains {Grapes, Mango}. So, according to the principle of Apriori, if {Grapes, Apple, Mango} is frequent, then {Grapes, Mango} must also be frequent.

I utilized apriori algorithm from Mlxtend python library and found out associations from top 100 most frequent products which resulted in 28 product pairs (total 56 rules) that have lift highr than 1. The top 10 product pairs having highest lift are shown below:

| Product A  | Product B | Lift |
| ------------- | ------------- | ---- |
| Limes  | Large Lemons  | 3 |
| Organic Strawberries | Organic Raspberries | 2.21 |
| Organic Avocado | Large Lemon | 2.12 |
| Organic Strawberries | Organic Blueberries | 2.11 |
| Organic Hass Avocado | Organic Raspberries | 2.08 |
| Banana | Organic Fuji Apple | 1.88 |
| Bag of Organic Bananas | Organic Raspberries | 1.83 |
| Organic Hass Avocado | Bag of Organic Bananas | 1.81 |
| Honeycrisp Apple | Banana | 1.77 |
| Organic Avocado | Organic Baby Spinach | 1.70 |


## ML Model to Predict Product Reorders

We can utilize this anonymized transactional data of customer orders over time to predict which previously purchased products will be in a user’s next order. This would help recommend the products to a user. 

To build a model, I need to extract features from previous order to understand user's purchase pattern and how popular the particular product is. I extract following features from the user's transactional data.

**Product Level Features:** To understand the product's popularity among users
```
(1) Product's average add-to-cart-order
(2) Total times the product was ordered
(3) Total times the product was reordered
(4) Reorder percentage of a product
(5) Total unique users of a product
(6) Is the product Organic?
(7) Percentage of users that buy the product second time
```

**Aisle and Department Level Features:** To capture if a department and aisle are related to day-to-day products (vegetables, fruits, soda, water, etc.) or once-in-a-while products (medicines, personal-care, etc.) 
```
(8) Reorder percentage, Total orders and reorders of a product aisle
(9) Mean and std of aisle add-to-cart-order
(10) Aisle unique users
(10) Reorder percentage, Total orders and reorders of a product department
(11) Mean and std of department add-to-cart-order
(12) Department unique users
(13) Binary encoding of aisle feature (Because one-hot encoding results in many features and make datarame sparse)
(14) Binary encoding of department feature (Because one-hot encoding results in many features and make datarame sparse)
```

**User Level features:** To capture user's purchase pattern and behavior
```
(15) User's average and std day-of-week of order
(16) User's average and std hour-of-day of order
(17) User's average and std days-since-prior-order
(18) Total orders by a user
(19) Total products user has bought
(20) Total unique products user has bought
(21) user's total reordered products
(22) User's overall reorder percentage
(23) Average order size of a user
(24) User's mean of reordered items of all orders
(25) Percentage of reordered itmes in user's last three orders
(26) Total orders in user's last three orders
```

**User-product Level Features:** To capture user's pattern of ordering-reordering specific products 
```
(27) User's avg add-to-cart-order for a product
(28) User's avg days_since_prior_order for a product
(29) User's product total orders, reorders and reorders percentage
(30) User's order number when the product was bought last
(31) User's product purchase history of last three orders
```
### ML Model

Using the extracted features, I prepared a dataframe which shows all the products user has bought previously, user level features, product level features, asile and department level features, user-product level features and the information of current order such as order's day-of-week, hour-of-day, etc. The Traget would be 'reordered' which shows how many of the previously purchased items, user ordered this time. 

Since the dataframe is huge, I reduced the memory consumption of it by downcasting to fit the data int my memory. I preferred MinMaxScaler over StandardScaler as the latter requires 16 GB of RAM for its operation. I followed standard process for model building and I relied on XGBoost as it handles large data, can be parallelized and gives feature importance. I also built Neural Network to see what would be the best performance from this model disregarding some inherent randomness from both of these models.  To balance the data, I have used cost-sensitive learning by assigning class weightage (~{0:1, 1:10}). I have not used random-upsampling/SMOTE as it would increase the data size and I do not have much memory. Also, since random-down-sampling discards information which might be important and would result in bias. 

Since, we can hack the F1 score by changing the threshold, I relied on AUC Score for model evaluation. The performance of both of these models is shown below using Confusion Matrix, ROC curve and classification report. The feature important plot from XGBoost model is also shown to understand important features which help predict product's reorder. The performance of both models is almost similar and XGBoost slightly performs better in terms of ROC-AUC.

**Neural Network Model Architecture and Performance:**

<p align="center">
  <img width="500" height="200" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/archie-ann.png">
</p>

<p align="center">
  <img width="450" height="200" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/report-ann.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/metrics-ann.png">
</p>

**XGBoost Model's Performance and Feature Importance:**


<p align="center">
  <img width="400" height="200" src="https://github.com/archd3sai/Instacart-Market-Basket-Analysis/blob/master/Plots/XGBoost-Report.png">
</p>

<p align="center">
  <img width="600" height="300" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/xgboost%20model/cofusion%20matrix_ROC.png">
</p>

<p align="center">
  <img width="500" height="750" src="https://github.com/kotlasaicharan/Instacart-Data-Analysis/blob/main/plots/xgboost%20model/feature_importance.png">
</p>

