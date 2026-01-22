# Problem Statement
How can we maximize incremental conversions [`placing an order`] without wasting incentives on users who would have converted anyway?

## Solution 
Design a controlled experimentation framework that first estimates the average impact of a promotion using A/B Testing and then extend to individual level causal inference using Uplift Modeling.

## Data
This dataset is from [UC Irvine Machine Learning](https://archive.ics.uci.edu/dataset/352/online+retail), a well-known open source resource.

- This dataset contains 8 columns and 541,909 rows.
- Out of which there are 4,060 unique customers.
- The following is the description of the columns:
    - InvoiceNo: Invoice number.
    - StockCode: Stock code.
    - Description: Description.
    - Quantity: Quantity.
    - InvoiceDate: Invoice date.
    - UnitPrice: Unit price.
    - CustomerID: Customer ID.
    - Country: Country.

** important note : There is no explicit treatment column in the dataset. We will create one. **

## Feature Engineering

- We will create the following features to understand the behavior of the customers from the dataset:
    - recency_days: Number of days since last purchase.
    - frequency: Number of purchases.
    - monetary_funds: Total amount spent.
    - tenure_days: Number of days since first purchase.
    - average_order_value: Average amount spent per order.
    - average_basket_size: Average number of items per order.
    - total_quantity: Total number of items purchased.
    - unique_products: Number of unique products purchased.
    - unique_invoices: Number of unique invoices.
    - most_common_hour: Most common hour of purchase.
    - most_common_weekday: Most common weekday of purchase.
    - last_purchase_month: Last purchase month. 

## Treatment Assignment
## A/B Test Results
- The treatment group showed a 0.56% increase in conversion rate compared to the control group.
- The p-value is 0.73, which is far above the 0.05 threshold, indicating that the treatment has no significant impact on the conversion rate.
- The overall A/B test shows no significant difference between the treatment and control groups.

## Uplift Modeling
Initially I have performed uplift modeling using the basic T-learner approach using Random Forest.

| Decile              | Treatment Rate | Control Rate | Uplift                     |
|---------------------|----------------|--------------|----------------------------|
| 0–3 (Low uplift)    | ~0%            | ~100%        | -1.0 (hurt by treatment)   |
| 4                   | 40%            | 90%          | -0.49                      |
| 5                   | 85%            | 19%          | +0.66                      |
| 6–9 (High uplift)   | 100%           | 0%           | +1.0 (benefit from treatment) |

- Customers in lower uplift deciles (0-4) actually perform worse when treated (sleeping dogs) who would have converted anyway but were negatively impacted by the treatment.
- Customers in higher uplift deciles (5-9) perform better when treated who would not have converted but were positively impacted by the treatment.  

Possible reasons for this outcome: 
- Random forest might be prone to overfitting especially on this small dataset.
- T learner approach introduces bias as it uses two different models for treatment and control groups. 
## Breaking down the Qini Curve
## XGBoost & Causal Forest
I will compare the results of XGBoost & Causal Forest with the T-learner approach.
