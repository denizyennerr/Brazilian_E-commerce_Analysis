# Brazilian E-commerce Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning & Preparation](#data-cleaning-preparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results&Findings](#results/findings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)


### Project Overview: 

This data analysis project explores a public dataset of e-commerce orders from Olist. Olist is a prominent online e-commerce platform connecting merchants to the main marketplaces of Brazil. The dataset comprises 100,000 orders between 2016 and 2018, offering valuable information on various aspects of the customer journey, including order status, pricing, payment, and customer reviews.

Presented by Olist, this dataset underscores the platform's success in streamlining e-commerce operations for merchants across Brazilian marketplaces. Olist facilitates seamless connections between merchants and consumers through innovative solutions, fostering a unified and efficient e-commerce ecosystem.

This analysis will delve deeper into understanding the customer journey, comparing seller orders and their delivery times, and analyzing payment methods and payment installment patterns across different regions. Lastly, it will conduct an RFM (Recency, Frequency, Monetary) analysis, and thanks to this segmentation it will reveal the loyal customers and potential retention customers. By unlocking the power of Brazilian e-commerce through data-driven insights, one can reach important findings that can contribute to strategic decision-making and drive further growth in the e-commerce landscape.

### Tools

- Excel- Data Cleaning
   - [Download here] (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- PostgreSQL- Data Analysis
- Python- Data Visualisation

### Data Cleaning/Preparation

In the initial data preparation phase, the following tasks were performed:
1. Data Loading and inspection.
2. Data cleaning and formatting.


### Database Schema (ERD)
[Download Here](ERD.pgerd.png)
As can be depicted from the schema, the database contains seven eight tables. These tables are orders, sellers, order_items, order_reviews, order_payments, products, customers and the product_category_name_translation. We will examine each table independently and conduct pre-processing to minimize excess space usage.


### EDA( Exploratory Data Analysis)

### EDA involved in exploring the Olist dataset to answer key questions for order analysis are as such:

- What does the distribution of orders look like on a monthly basis, and how do monthly order counts vary across the years from 2016 to 2018?
- How have the order statuses "unavailable" and "canceled" varied over the years 2016-2018?
- How has the order status "delivered" varied over the years 2016-2018?
- After examining the order counts broken down by product category. Which categories stand out during special occasions such as Valentine's Day?
- What is the distribution of order counts based on both the days of the week (e.g., Monday, Thursday) and the days of the month (e.g., 1st, 2nd, etc.)? Additionally, how do these patterns differ across different days of the week and dates within a month?

  
### EDA involved in exploring the Olist dataset to answer key questions for customer analysis is as such:

- Which cities have customers who make the most purchases? Determine the city where each customer places the highest number of orders and conduct the analysis accordingly.


### EDA involved in exploring the Olist dataset to answer key questions for seller analysis are as such:

- Who are the top 5 sellers that deliver orders to customers most efficiently? Bring the top 5 sellers who deliver orders to customers most efficiently? Analyze and interpret their order counts along with the reviews and ratings of their products.
- Which sellers sell products across a wider range of categories? Do sellers with a wider range of categories also have higher order counts?

### EDA involved in exploring the Olist dataset to answer key questions for payment analysis are as such:

- In which regions do users that have more installments for payment primarily live?
- What is the breakdown of successful orders and total successful payment amounts based on payment methods?
- What is the distribution of orders based on payment method, specifically comparing single payments versus installments across different product categories? Which categories are most frequently paid for in installments?



### Data Analysis
```SQL
SELECT * from orders limit 10;
# To start off, we view the first 10 orders of the dataset.

# The Customer Table, found in the customers_dataset, includes the following columns:
# customer_id: serves as the key to the orders dataset, ensuring each order has a unique customer_id.
# customer_unique_id: provides a unique identifier for each customer.

# In this system, each order is linked to a distinct customer_id, meaning the same customer may have different IDs for different orders. The inclusion of customer_unique_id allows for the identification of customers who have made repeat purchases from the store. Otherwise, each order would appear associated with a different customer.
# customer_zip_code_prefix: denotes the first five digits of the customer's zip code.
# customer_city: indicates the name of the customer's city.
# customer_state: specifies the customer's state.

SELECT count(order_id),
	EXTRACT(MONTH from order_approved_at) AS approved_month
FROM ORDERS
GROUP BY approved_month
ORDER BY approved_month;

#- We can now see the distribution of orders on a monthly basis.

and how do monthly order counts vary across the years from 2016 to 2018?
![image](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/e516b517-8205-4a52-b344-0bf8d69fc09b)


```

### Results/Findings

The query results are summarised as follows:
1. Users who opt for more installments during payment primarily reside in São Paulo (SP), followed by Rio de Janeiro (RJ), Minas Gerais (MG), and Paraná (PR). 
2. The number of users choosing more installments decreases gradually in these regions. 
3. Other regions such as Rio Grande do Sul (RS), Bahia (BA), and Paraíba (PB) also have higher installments, although to a lesser extent.


### Recommendations

### Limitations
I had to remove all zero values

### References

1. [PostgreSQL.org] (https://www.postgresql.org/docs/current/datatype-datetime.html)
2. Olist Store Ecommerce Dataset. Retrieved from [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce] 
4. Brazilian Institute of Geography and Statistics (IBGE), (1972). Brazilian Zip Code Geolocation Dataset. Retrieved from [https://www.ibge.gov.br/en/]
5. Pagan Research [https://paganresearch.io/company/olist]

   


