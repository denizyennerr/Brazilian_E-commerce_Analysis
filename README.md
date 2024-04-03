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


## Project Overview: 

This data analysis project explores a public dataset of e-commerce orders from Olist. Olist is a prominent online e-commerce platform connecting merchants to the main marketplaces of Brazil. The dataset comprises 100,000 orders between 2016 and 2018, offering valuable information on various aspects of the customer journey, including order status, pricing, payment, and customer reviews.

Presented by Olist, this dataset underscores the platform's success in streamlining e-commerce operations for merchants across Brazilian marketplaces. Olist facilitates seamless connections between merchants and consumers through innovative solutions, fostering a unified and efficient e-commerce ecosystem.

This analysis will delve deeper into understanding the customer journey, comparing seller orders and their delivery times, and analyzing payment methods and payment installment patterns across different regions. Lastly, it will conduct an RFM (Recency, Frequency, Monetary) analysis, and by using this technique marketers can tailor their marketing strategies accordingly. We can easily analyze the segmentation to reveal the loyal customers and the retention customers. By unlocking the power of Brazilian e-commerce through data-driven insights, marketers can reach important findings that can contribute to strategic decision-making and drive further growth in the e-commerce landscape.

## Tools

- Excel- Data Cleaning
   - [Download here] (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- PostgreSQL- Data Analysis
- Python- Data Visualisation

## Data Cleaning/Preparation

In the initial data preparation phase, the following tasks were performed:
1. Data Loading and inspection.
2. Data cleaning and formatting.


## Database Schema (ERD)

![ERD pgerd](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/a305011e-80b8-4e17-bcc7-a310872d9b06)

As can be depicted from the schema, the database contains eight tables. These tables are orders, sellers, order_items, order_reviews, order_payments, products, customers and the product_category_name_translation. We will examine each table independently and conduct pre-processing to minimize excess space usage.

## EDA( Exploratory Data Analysis)

**The Order Item Table, sourced from the "olist_order_items_dataset", consists of the following columns:**

- order_id: A unique identifier for each order.
- order_item_id: A sequential number indicating the position of an item within the order.
- product_id: A unique identifier for each product.
- seller_id: A unique identifier for each seller.
- shipping_limit_date: The deadline set by the seller for handing over the order to the logistics partner.
- price: The price of the item.
- freight_value: The freight cost associated with the item. If an order contains multiple items, the freight cost is divided among them.

We view the first few rows of the table using the limit from PostgreSQL.
```SQL
select * from order_items limit 10;
```

![Order_items_table](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/e4dc81e7-73b7-45f7-85fa-d62f6d691159)

**The Product Table contains the following columns:**

- product_id: A unique identifier for each product.
- product_category_head: The root category of the product, originally in Portuguese.
- product_name_length: The length of the product name in characters.
- product_description_length: The length of the product description in characters.
- product_photos_qty: The number of photos published for the product.
- product_weight_g: The weight of the product measured in grams.
- product_length_cm: The length of the product measured in centimeters.
- product_height_cm: The height of the product measured in centimeters.
- product_width_cm: The width of the product measured in centimeters.

We view the first few rows of the table using the limit from PostgreSQL.
```SQL
select * from products limit 10;
```
![products_table1](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/7b675f09-fec1-49b5-a45f-fa8fb0b8a15a)

![products_table2](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/54fbb816-018a-4616-8b3e-9f74c0551fa3)


**The Product Category Info Table contains the following columns:**

- product_category_name: The category name was originally in Portuguese.
- product_name_english: The category name is translated into English.

We view the first few rows of the table using the limit from PostgreSQL.
```SQL
select * from product_category_name_translation limit 10;
```
![product_category_name_translation_table](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/c58ac45e-65b9-41f2-aa8c-06219a828ab5)


**The Order Table, found in the olist_orders_dataset, includes the following columns:**

- order_id: a unique identifier for each order.
- customer_id: serves as a key to the customer dataset, ensuring each order is associated with a unique customer.
- order_status: indicates the status of the order (delivered, shipped, etc.).
- order_purchase_timestamp: displays the timestamp of the purchase.
- order_approved_at: denotes the timestamp when payment for the order was approved.
- order_delivered_carrier_date: represents the timestamp when the order was handed over to the logistic partner for delivery.
- order_delivered_customer_date: indicates the actual delivery date of the order to the customer.
- order_estimated_delivery_date: provides the estimated delivery date communicated to the customer at the time of purchase.

We view the first few rows of the table using the limit from PostgreSQL.
```SQL
select * from orders limit 10;
```
![orders_table1](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/d2560a3c-50a8-41a6-8e3b-264f1d45327c)

![orders_table2](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/52fb6c4d-8629-4491-950c-2becb0151f39)


**The Review Table, found in the olist_order_reviews_dataset, contains the following columns:**

- review_id: a unique identifier for each review.
- order_id: a unique identifier for each order.
- review_score: a rating ranging from 1 to 5 provided by the customer in a satisfaction survey.
- review_comment_title: the title of the comment left by the customer in Portuguese.
- review_comment_message: the message of the comment left by the customer in Portuguese.
- review_creation_date: indicates the date the satisfaction survey was sent to the customer.
- review_answer_timestamp: denotes the timestamp of the customer's response to the satisfaction survey.
```SQL
select * from order_reviews limit 10;
```
![order_reviews](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/8b44ae16-3ca8-4c1f-a295-4b65ef959d8e)


**The Order Payment Table, found in the olist_order_payments_dataset, includes the following columns:**

- order_id: a unique identifier for each order.
- payment_sequential: indicates the sequence number for payments made by a customer for an order.
- payment_type: specifies the method of payment selected by the customer.
- payment_installments: denotes the number of installments chosen by the customer for payment.
- payment_value: represents the value of the transaction.
```SQL
select * from order_payments limit 10;
```
![order_payments](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/2b6cd22a-a38f-4659-8d80-b1f6286d1a53)


**The Seller Table, found in the olist_sellers_dataset, contains the following columns:**

- seller_id: a unique identifier for each seller.
- seller_zip_code: the first 5 digits of the seller's zip code.
- seller_city: the name of the city where the seller is located.
- seller_state: the state where the seller is located.
```SQL
select * from sellers limit 10;
```
![sellers](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/d7392d3f-e172-4cc4-ba2b-c6a8dd62d456)



**The Customer Table, found in the olist_customers_dataset, includes the following columns:**

- customer_id: serves as a reference key to the orders dataset, with each order having a unique customer_id.
- customer_unique_id: provides a distinct identifier for each customer. This ensures that repeat purchases made by the same customer can be identified within the dataset. Otherwise, each order would appear associated with a different customer.

- customer_zip_code_prefix: denotes the first five digits of the customer's zip code.
- customer_city: specifies the name of the customer's city.
- customer_state: indicates the state where the customer is located.
```SQL
select * from customers limit 10;
```
![customers](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/0f4b1ce5-0c9c-4b07-9e85-f031be5632e4)



### EDA involved in exploring the Olist dataset to answer key questions for order analysis are as such:

- What does the distribution of orders look like on a monthly basis?
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


## Data Analysis

```SQL
SELECT * from orders limit 10;
``` 
To start, we view the first 10 orders of the dataset.

```SQL
SELECT count(order_id),
	EXTRACT(MONTH from order_approved_at) AS approved_month
FROM orders
GROUP BY approved_month
ORDER BY approved_month;
```

We can now see the distribution of orders on a monthly basis.

We first start with importing the relevant libraries.

``` Python
import numpy as np
import pandas as pd
import seaborn as sns
from matplotlib import pyplot as plt
```
With the help of Matplotlib alongside the Seaborn library, we employ the barplot() function to visualize the distribution of orders across different months. Additionally, we leverage functions from the Matplotlib library to enhance the aesthetic appeal of the plot. As a result, we obtain a clear representation of the monthly order distribution.
Then we import our CSV file to our Jupyter Notebook. Afterward, we remove any rows containing missing values (NaN values). This step ensures data cleanliness and prevents potential issues during analysis.

``` Python
monthly_order_data= pd.read_csv(r"C:\Users\ASUS\Desktop\monthly_order.csv")
monthly_order_data.dropna(inplace=True)
monthly_order_data.approved_month=monthly_order_data.approved_month.astype(int)
```
At last, we use the barplot() function to visualize the distribution of orders across different months.

``` Python
plt.figure(figsize=(15, 8))
sns.barplot(x='approved_month', y='count', data=monthly_order_data.astype(int), palette=['brown'], linewidth=2, ci=None)
plt.title('Monthly Orders Over Time', color='white')
plt.xlabel('Months', color='white')
plt.ylabel('Number of Orders', color='white')
plt.show()
```

![monthly_orders](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/3ee4033a-9a28-4726-80f5-e5aaeeec034a)


The query below aims to analyze the distribution of orders based on their status (e.g., delivered, shipped, processed) and the month in which they were approved. It retrieves the count of orders, along with their respective order status and the month in which they were approved. We did not filter explicitly for the order_status by using SQL, we found the order status friction of the monthly orders only. 

 ``` SQL
Select count(order_id), order_status,
		extract(month from order_approved_at) as approved_month
from orders
group by order_status, approved_month
order by order_status desc, approved_month desc;
```

We will now filter the data for orders with order status 'unavailable' or 'cancelled' with Python. And we will employ a barplot() function to visualize the unavailable or cancelled orders by month on the x-axis. The frequency of orders will be depicted on the y-axis.

``` Python
unavailable_or_cancelled_orders = order_status_distribution[(order_status_distribution['order_status'] == 'unavailable') | (order_status_distribution['order_status'] == 'cancelled')]


![undelivered_cancelled_orders](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/082592e6-6e94-49af-b0a3-d1e3d0946fd8)
plt.figure(figsize=(12, 6))
plt.bar(unavailable_or_cancelled_orders['approved_month'], unavailable_or_cancelled_orders['count'], color='brown', linewidth=3)
plt.title('Monthly Friction of Unavailable or Cancelled Orders')
plt.xlabel('Approved Month')
plt.ylabel('Frequency')
plt.xticks(rotation=45, fontsize=10)
plt.tight_layout()
plt.show()

```
![Q1](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/a97eb6ba-a691-479e-b0b5-10698ad415fd)


We will apply the same filter with orders where the order status is delivered. We will again use a barplot() function to visualize our graph. 

``` Python

delivered_orders= order_status_distribution[order_status_distribution['order_status'] == 'delivered']

plt.figure(figsize=(12, 6))
sns.barplot(x='approved_month', y='count', data=delivered_orders, color='green', ci=None)
plt.title('Monthly Friction of Delivered Orders')
plt.xlabel('Months')
plt.ylabel('Number of Orders')
plt.xticks(fontsize=10)
plt.yticks(fontsize=10)
plt.tight_layout()
plt.show()

```
![delivered](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/1de88eb4-c646-4431-9387-bfd709bd2b4a)



After we examined the order statuses of the monthly orders, we will now examine the categories that stand out during special occasions such as Valentine's Day. We took days between the first of February and the 13th of February to examine the product categories until Valentine's Day on the 14th of February. 

``` SQL
SELECT 
    COUNT(o.order_id) AS order_count,
    t.product_category_name_english,
    DATE(o.order_approved_at) AS approved_date,
    EXTRACT(YEAR FROM o.order_approved_at) AS approved_year 
FROM 
    orders AS o
LEFT JOIN 
   order_items AS b ON o.order_id = b.order_id
LEFT JOIN 
    products AS p ON b.product_id = p.product_id
LEFT JOIN 
    product_category_name_translation AS t ON p.product_category_name = t.product_category_name
WHERE 
    (EXTRACT(MONTH FROM o.order_approved_at) = 2 AND EXTRACT(DAY FROM o.order_approved_at) BETWEEN 1 AND 13)
GROUP BY 
    approved_date, approved_year, product_category_name_english
ORDER BY  order_count desc
limit 15
;
```
Once we imported our CSV file to our Jupyter Notebook, we used a barplot() to visualize the top categories that were popular during Valentine's Day shopping period.

``` Python
product_category_valentines_day= pd.read_csv(r"C:\Users\ASUS\Desktop\product_category_valentines_day.csv")
product_category_valentines_day

plt.figure(figsize=(12, 8))
sns.barplot(x='product_category_name_english', y='order_count' ,data=product_category_valentines_day, ci=None)
plt.title('Product Distribution by Valentines Day')
plt.xlabel('Category')
plt.ylabel('Number of Products')
plt.xticks(rotation=90)
plt.tight_layout()
plt.show()
```

![valentinesday](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/eb327fed-9afd-46cc-933c-aff5c387e9f1)


In the following query, we analyzed the number of orders based on the days of the week (e.g., Monday, Thursday).
``` SQL
Select count(order_id) as order_count,
to_char(order_purchase_timestamp, 'Day') as approved_day
from orders
group by approved_day
order by approved_day;
``` 
We also examined the order counts by the days of the month (e.g., 1st, 2nd, etc.).

``` SQL
Select count(order_id) as order_count, 
extract(day from order_purchase_timestamp) as days_of_the_month
from orders
group by approved_day, days_of_the_month
order by approved_day , days_of_the_month 
;
```

After importing our CSV file into Jupyter Notebook, we can proceed with visualizing our data. Depending on the nature of our analysis, we will utilize various visualization libraries such as Matplotlib, Seaborn, or Plotly.

``` Python
days_order_count = pd.read_csv(r"C:\Users\ASUS\Desktop\days_order_count.csv")
days_order_count
```

For this visualization, we used a pie chart from Plotly to visualize the distribution of order counts by days of the week. 

``` Python
plt.figure(figsize=(10, 6))
plt.pie(days_order_count['order_count'], labels=days_order_count['approved_day'], autopct='%1.1f%%', startangle=140)
plt.title('Order Count by Days of the Week')
plt.axis('equal')  
plt.show()
```

![pie](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/39364569-80df-486e-93ac-e2ae2c892a9e)



Before creating visualizations for the days of the month order count, we needed to perform data preprocessing tasks. As such as cleaning the data to make it suitable for visualization.

``` Python
days_of_the_month_order_count= pd.read_csv(r"C:\Users\ASUS\Desktop\days_of_the_month_ordercount.csv")

days_of_the_month_order_count_cleaned= days_of_the_month_order_count.dropna()
print(days_of_the_month_order_count_cleaned)
```

The bar plot displays the distribution of order count across different days of the month. Each bar represents the number of orders received on a specific day of the month. 
From the visualization, we can observe some patterns:
- There is some variation in the number of orders throughout the month, with certain days having higher order counts than others.
- Some days show peaks in order counts, indicating periods of increased sales activity.
- Other days exhibit lower order counts, suggesting quieter periods in terms of order placements.
- Overall, there seems to be some variability in order volumes across different days of the month, which could be influenced by factors such as promotions, seasonality, or customer behavior. 

Further analysis could be conducted to identify any underlying trends or patterns driving these fluctuations in order counts on different days of the month.

``` Python
plt.figure(figsize=(15, 8))
sns.lineplot(x='days_of_the_month', y='order_count', data=days_of_the_month_order_count_cleaned, ci=None, marker='o', markersize=8) 
plt.title('Order Count by Days of the Month')
plt.xlabel('Days of the Month ')
plt.ylabel('Number of Orders')
plt.show()

```













Next, we will delve deeper into customer analysis by identifying the cities with the highest number of shoppers.

``` SQL
WITH order_counts AS (
    SELECT 
        o.customer_id,
        c.customer_city,
        COUNT(o.order_id) AS order_count
    FROM 
        orders AS o 
    LEFT JOIN 
        customers AS c ON c.customer_id = o.customer_id
    GROUP BY 
        o.customer_id,
        c.customer_city
), 
customer_city_rn AS (
    SELECT 
        ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_count DESC) AS rn,
        customer_id,
        customer_city
    FROM 
        order_counts
),
customer_city AS (
    SELECT 
        customer_id,
        customer_city
    FROM 
        customer_city_rn
    WHERE 
        rn = 1
)
SELECT 
    cc.customer_city,
    COUNT(o.order_id)
FROM 
    orders AS o
LEFT JOIN 
    customer_city AS cc ON o.customer_id = cc.customer_id
GROUP BY 
    cc.customer_city
ORDER BY 
    COUNT(o.order_id) DESC;
```

The output of the query provides a list of cities along with the count of orders placed by customers residing in each city. Here is the number of orders per city:

Sao Paulo: 15,540 orders
Rio de Janeiro: 6,882 orders
Belo Horizonte: 2,773 orders
Brasilia: 2,131 orders
Curitiba: 1,521 orders
Campinas: 1,444 orders
Porto Alegre: 1,379 orders
Salvador: 1,245 orders
Guarulhos: 1,189 orders
Sao Bernardo do Campo: 938 orders

This indicates that Sao Paulo has the highest number of orders, followed by Rio de Janeiro, Belo Horizonte, and other cities in descending order of order count.

Now, we will again use Python to visualize this output. We will again employ a barplot() function from the Seaborn.

```Python
Top_orders_per_city= pd.read_csv(r"C:\Users\ASUS\Desktop\top_orders_per_city.csv")
Top_orders_per_city

plt.figure(figsize=(20,8))
sns.barplot(x='customer_city', y='count', data=Top_orders_per_city)
plt.title('City-wise Top Orders')
plt.xlabel('Customer City')
plt.ylabel('Order Count')
```	
![top_orders_per_city](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/33a1372a-a868-46a6-ad25-051bce25f928)

With the following query, we will be able to identify sellers who have a track record of delivering orders quickly while maintaining satisfactory average review scores from customers.

``` SQL
WITH fastest_delivered_products AS (
    SELECT 
        oi.seller_id,
        (o.order_delivered_customer_date - o.order_purchase_timestamp) AS delivery_time_days
    FROM 
        orders o
    LEFT JOIN 
        order_items oi ON oi.order_id = o.order_id
)
SELECT 
    f.seller_id,
    COUNT(DISTINCT oi.order_id) AS order_count,
    AVG(f.delivery_time_days) AS avg_delivery_time,
    AVG(rw.review_score) AS avg_review_score
FROM 
    fastest_delivered_products f
JOIN 
    order_items oi ON oi.seller_id = f.seller_id
LEFT JOIN 
    order_reviews rw ON rw.order_id = oi.order_id
GROUP BY
    f.seller_id
HAVING 
    AVG(f.delivery_time_days) IS NOT NULL 
    AND COUNT(DISTINCT oi.order_id) > 15
ORDER BY 
    avg_delivery_time
LIMIT 5;
```
We plot for the top 5 fastest delivery sellers by their order count.

```Python
fastest_delivery_sellers= pd.read_csv(r"C:\Users\ASUS\Desktop\fastest_delivery_sellers.csv")
fastest_delivery_sellers

plt.figure(figsize=(16, 7))
sns.barplot(x='seller_id', y='order_count', data=fastest_delivery_sellers, palette='viridis', ci=None)
plt.title('Top 5 Fastest Delivery Sellers by Order Count')
plt.xlabel('Seller ID')
plt.ylabel('Order Count')
plt.xticks(rotation=45)
plt.show()
```

![fastest_sellers_by_ordercount](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/7c8a2965-3f1d-4e79-9426-c9e5b0861383)


Now we will also plot the top 5 fastest delivery sellers by their average review scores.

```Python
top_sellers_by_review_score = fastest_delivery_sellers.sort_values(by='avg_review_score', ascending=False).head(5)

plt.figure(figsize=(16, 7))
sns.barplot(x='seller_id', y='avg_review_score', data=fastest_delivery_sellers, palette='viridis', ci=None)
plt.title('Top 5 Fastest Delivery Sellers by Average Review Score')
plt.xlabel('Seller ID')
plt.ylabel('Average Review Score')
plt.xticks(rotation=45)
plt.show()
```
![average_review_score](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/4f0f993b-07c6-44ee-8ebf-8fac209854d2)


Next, we will check the number of categories each seller sells their products in and their corresponding order counts. 

```SQL
WITH category_counts AS (
    SELECT 
        oi.seller_id,
        COUNT(DISTINCT oi.order_id) AS order_counts,
        COUNT(DISTINCT p.product_category_name) AS category_count
    FROM 
        order_items oi
    LEFT JOIN 
        sellers s ON s.seller_id = oi.seller_id
    LEFT JOIN 
        products p ON p.product_id = oi.product_id
    GROUP BY 
        oi.seller_id
)
SELECT 
    cc.seller_id,
    cc.order_counts,
    cc.category_count
FROM 
    category_counts cc
JOIN 
    (
        SELECT 
            seller_id,
            MAX(category_count) AS max_category
        FROM 
            category_counts
        GROUP BY 
            seller_id
    ) AS max_categories ON cc.seller_id = max_categories.seller_id 
                         AND cc.category_count = max_categories.max_category
ORDER BY 
		cc.category_count desc
LIMIT 10;

```
We will again visualize the query by barplot() function from the Seaborn library.

```Python
category_counts_sellers= pd.read_csv(r"C:\Users\ASUS\Desktop\category_counts_sellers.csv")
category_counts_sellers

plt.figure(figsize=(15,8))
sns.barplot(x='category_count', y='order_counts', data=category_counts_sellers, palette=('GnBu_d'), ci=None)
plt.title('Maximum Category Wise Product Sellers')
plt.xlabel('Number of Category')
plt.ylabel('Number of Products')
```
The graph indicates that there is no observable correlation between the number of product categories offered by a seller and the quantity of orders they receive.

![category_count_orders](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/365599ff-eb4b-45b5-893a-ee04b991df5f)

Next, we will conduct a customer analysis.
We will start with plotting the regions where users with the highest number of installment payments reside.

```SQL
With Data as (SELECT 
	c.customer_state,
	count( distinct o.order_id) as order_count,
    AVG(p.payment_installments) AS average_payment_installments
FROM 
    customers c 
JOIN 
    orders o ON o.customer_id = c.customer_id
JOIN 
    order_payments p ON p.order_id = o.order_id
Where p.payment_installments>12
GROUP BY 
    p.payment_installments,	c.customer_state
Order by 2 desc)
Select customer_state, 
		count(order_count) from Data
		group by 1
		order by 2 desc;
```
We will again visualize our query by barplot() function from the Seaborn library.
```Python
highest_number_of_installment_payments_reside= pd.read_csv(r"C:\Users\ASUS\Desktop\highest_number_of_installment_payments_reside.csv")
highest_number_of_installment_payments_reside

plt.figure(figsize=(15,8))
sns.barplot(x='customer_state', y='count', data=highest_number_of_installment_payments_reside)
plt.title('Analyzing Number of Payment Installments Per State')
plt.xlabel('Customer State')
plt.ylabel('Payment Installments')
plt.show()
```
![highest_number_of_installment_payments_reside](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/c00acf76-f394-47d1-bf59-119bdf06b719)

This output represents the count of users residing in different regions where users with the highest number of installment payments reside. Each region code is followed by the count of users. For instance, "SP" indicates the São Paulo region with 10 users have the highest number of installment payments. Similarly, "RJ" represents Rio de Janeiro with 8 users, "MG" represents Minas Gerais with 6 users, and so on.

Next, we will calculate the number of successful orders and the total successful payment amount based on the payment method.
```SQL
Select 	op.payment_type,
		count(distinct o.order_id), 
		sum(case when o.order_status not in ('cancelled', 'unavailable') then op.payment_value end) as succesful_payment
from order_payments op
join orders o on o.order_id = op.order_id
group by op.payment_type 
order by op.payment_type desc
;
```

We will again visualize our query by barplot() function from the Seaborn library.
```Python
payment_type= pd.read_csv(r"C:\Users\ASUS\Desktop\payment_type_segmentatiton.csv")
payment_type

plt.figure(figsize=(15,8))
sns.barplot(x='payment_type', y='count', data=payment_type, ci=None, palette=['purple','yellow','orange' ,'red', 'green'])
plt.title('Total Successful Orders Based On the Payment Method')
plt.xlabel('Payment Method')
plt.ylabel('Number of Successful Orders')
plt.show()
```
![payment_type](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/fbb66618-c876-43ff-98f5-c7d6bfdfffe5)

We can see that  the payment methods used by customers along with the corresponding order count and total successful payment amount. 

- "voucher": There are 3,866 orders made using vouchers, with a total successful payment amount of 375,539.32.
- "not_defined": There are 3 orders for which the payment method is not defined, resulting in a total successful payment amount of 0.00.
- "debit_card": There are 1,528 orders paid using debit cards, totaling 215,129.02 in the successful payment amount.
- "credit_card": The most common payment method is a credit card, with 76,505 orders and a total successful payment amount of 12,447,417.87.
- "boleto": Boletos, or bank slips, were used for 19,784 orders, amounting to 2,844,306.40 in successful payment.

We will now analyze the category-wise distribution of orders paid in single payment and in installments. We will also analyze the categories that are commonly paid in installments.

Query for orders paid in a single payment:
```SQL
WITH orders_single_payment AS (
    SELECT 
        pr.product_category_name,
        COUNT(DISTINCT o.order_id) AS order_count
    FROM
        orders o
    JOIN 
        order_payments op ON op.order_id = o.order_id
    JOIN 
        order_items oi ON oi.order_id = op.order_id
    JOIN 
        products pr ON pr.product_id = oi.product_id
    WHERE
        op.payment_installments = 1
    GROUP BY 
        pr.product_category_name
)
SELECT 
    'tek_cekim' AS payments,
    product_category_name,
    order_count
FROM 
    orders_single_payment
ORDER BY 
    order_count DESC,
    product_category_name DESC; 
```
The following data indicates the distribution of orders paid in single-payment installments across different product categories. 

- "esporte_lazer": The category of "Sports and Leisure" has the highest number of orders paid in a single payment installment, with 4,299 orders.
- "informatica_acessorios": Following closely, the "Computers and Accessories" category accounts for 4,177 orders.
- "beleza_saude": The "Beauty and Health" category ranks third with 3,880 orders paid in a single payment installment.
- "cama_mesa_banho": The category of "Bed, Bath, and Table" follows with 3,535 orders.
- "moveis_decoracao": Lastly, the "Furniture and Decoration" category has 3,152 orders paid in a single payment installment.

![single_installments](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/a3ce43bb-c31d-4188-acb3-7f7e6f6f7456)

```Python
single_payment_installments=pd.read_csv(r"C:\Users\ASUS\Desktop\single_installment.csv")
single_payment_installments

plt.figure(figsize=(16, 8))
sns.barplot(x='product_category_name', y='order_count', data=single_payment_installments, palette='viridis')
plt.title('Analyzing Category-Wise Number of Payment Installments')
plt.xlabel('Product Category')
plt.ylabel('Count of Payment Installments')
plt.xticks(rotation=90)
plt.show()
```

Query for orders paid in multiple installments:
```SQL
WITH orders_installments AS (
    SELECT 
        pr.product_category_name,
        COUNT(DISTINCT o.order_id) AS order_count
    FROM
        orders o
    JOIN 
        order_payments op ON op.order_id = o.order_id
    JOIN 
        order_items oi ON oi.order_id = op.order_id
    JOIN 
        products pr ON pr.product_id = oi.product_id
    WHERE
        op.payment_installments > 1
    GROUP BY 
        pr.product_category_name
)
SELECT 
    'taksitli' AS payments,
    product_category_name,
    order_count
FROM 
    orders_installments
ORDER BY 
    order_count DESC,
    product_category_name DESC; 
```
The following graph shows the distribution of orders paid in multiple payment installments across different product categories. As such;

- "cama_mesa_banho": There are 5,965 orders in the category of "Bed, Bath, and Table," indicating that this category has the highest number of orders paid in multiple installments.
- "beleza_saude": The "Beauty and Health" category follows closely with 5,006 orders.
- "relogios_presentes": The category of "Watches and Gifts" has 3,794 orders paid in multiple installments.
- "esporte_lazer": "Sports and Leisure" category accounts for 3,480 orders.
- "moveis_decoracao": Lastly, the "Furniture and Decoration" category has 3,353 orders paid in multiple installments.

```Python
multiple_payment_installments= pd.read_csv(r"C:\Users\ASUS\Desktop\multiple_installments.csv")
multiple_payment_installments

plt.figure(figsize=(16, 8))
sns.barplot(x='product_category_name', y='order_count', data=multiple_payment_installments, palette='GnBu_d')
plt.title('Analyzing Category-Wise Number of Payment Installments')
plt.xlabel('Product Category')
plt.ylabel('Count of Payment Installments')
plt.xticks(rotation=90)
plt.show()
```
![multiple_installments](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/ff9550da-b638-44f4-b2f9-62fc50458c2f)

Lastly, we will conduct the RFM (Recency, Frequency, Monetary) analysis and analyze customer behavior, and segment them into different categories based on recency, frequency, and monetary value. The segmentation can help in targeting specific customer groups with tailored marketing strategies.

```SQL 
WITH rfm AS (
  SELECT
    customer_id,
    MAX(invoice_date) AS max_invoice_date,
    EXTRACT(day FROM '2011-12-09'::date - MAX(invoice_date)) AS recency,
    COUNT(DISTINCT invoice_no) AS frequency,
    SUM(quantity * unit_price) AS monetary
  FROM rfm 
  WHERE quantity > 0 AND customer_id IS NOT NULL
  GROUP BY customer_id, rfm.invoice_date
 Order by 3 Desc
),
score AS (
  SELECT
    *,
    NTILE(4) OVER (ORDER BY recency DESC) AS recency_score,
    CASE
      WHEN frequency <= 1 THEN 1
      WHEN frequency <= 2 THEN 2
      WHEN frequency <= 4 THEN 3
      WHEN frequency <= 6 THEN 4
      ELSE 5
    END AS frequency_score,
    NTILE(4) OVER (ORDER BY monetary ASC) AS monetary_score
  FROM rfm
)
SELECT
  *,
  CONCAT(recency_score, frequency_score, monetary_score)::numeric AS rfm_score
FROM score;

with recency
as
(
SELECT
	customer_id,
	max(invoice_date) as last_day,
	('2011-12-09'-max(invoice_date)::date) as recency
FROM rfm
WHERE customer_id is not null and invoice_no not like 'C%'
GROUP BY customer_id
ORDER BY 3 asc
),
frequency
as
(
SELECT 
	customer_id,
	count(distinct invoice_no) as frequency
FROM rfm
WHERE customer_id is not null and invoice_no not like 'C%'
GROUP BY customer_id
ORDER BY 2 desc
),
monetary
as 
(
SELECT 
	customer_id,
	round(sum(unit_price*quantity)::decimal,2) as monetary
FROM rfm
WHERE  customer_id is not null and invoice_no not like 'C%'
GROUP BY customer_id
ORDER BY 2 desc
),
scores as
(
SELECT
	f.customer_id,
	recency,
	frequency,
	monetary,
	ntile(5) over (order by recency desc) as recency_score,
    CASE
       WHEN frequency<10 then '1'
       WHEN frequency >= 10 and frequency < 50 then '2'
       WHEN frequency >= 50 and frequency < 100 then '3'
       WHEN frequency >= 100 and frequency <= 150 then '4'
       WHEN frequency > 150 and frequency <= 250 then '5'
       END AS frequency_score,
     CASE
       WHEN monetary<5000 then '1'
       WHEN monetary >= 5000 and monetary < 15000 then '2'
WHEN monetary >= 15000 and monetary < 40000 then '3'
WHEN monetary >= 40000 and monetary <= 100000 then '4'
WHEN monetary > 100000 and monetary <= 300000 then '5'
END AS monetary_score		
FROM recency as r
LEFT JOIN frequency as f
on r.customer_id=f.customer_id
LEFT JOIN monetary as m
on r.customer_id=m.customer_id
ORDER BY 7 desc
),
mix_score
as
(
SELECT 
	customer_id,
	recency_score,
	frequency_score,
	monetary_score,
	(frequency_score::integer+monetary_score::integer) as mix_score
FROM scores
ORDER BY 5
),
final_scores as 
(
SELECT 
	customer_id,
	recency_score,
	frequency_score,
	monetary_score,
	CASE
		WHEN mix_score=2 then '1'
		WHEN mix_score>2 and mix_score<=3 then '2'
		WHEN mix_score>3 and mix_score<=5 then '3'
		WHEN mix_score>=6 and mix_score<=7 then '4'
		ELSE '5' end as mixscore
FROM mix_score
ORDER BY mix_score desc
)
SELECT 
	customer_id,
	recency_score,
	mixscore,
	CASE 
		WHEN recency_score::varchar similar to  '[1-2]%' and mixscore::varchar similar to '[1-2]%' then 'Hibernating'
		WHEN recency_score::varchar similar to  '[1-2]%' and mixscore::varchar similar to '[3-4]%' then 'At_Risk'
		WHEN recency_score::varchar similar to  '[1-2]%' and mixscore::varchar similar to '[5]%' then 'Cant_Loose'
		WHEN recency_score::varchar similar to  '[3]%' and mixscore::varchar similar to '[1-2]%' then 'About_to_Sleep'
		WHEN recency_score::varchar similar to  '[3]%' and mixscore::varchar similar to '[3]%' then 'Need_Attention'
		WHEN recency_score::varchar similar to  '[4]%' and mixscore::varchar similar to '[1]%' then 'Promising'
		WHEN recency_score::varchar similar to  '[5]%' and mixscore::varchar similar to '[1]%' then 'New_Customers'
		WHEN recency_score::varchar similar to  '[4-5]%' and mixscore::varchar similar to '[2-3]%' then 'Potential_Loyaltist'
		WHEN recency_score::varchar similar to  '[3-4]%' and mixscore::varchar similar to '[4-5]%' then 'Loyal_Customers'
		WHEN recency_score::varchar similar to  '[5]%' and mixscore::varchar similar to '[4-5]%' then 'Champions'
		END AS customer_segmentation
FROM final_scores 
ORDER BY 2 desc;
```
We will visualize our query using the barplot() function from the Seaborn Library.
```Python
RFM_Analysis= pd.read_csv(r"C:\Users\ASUS\Desktop\RFM.csv")
RFM_Analysis

plt.figure(figsize=(10, 5))
percentage = (RFM_Analysis['customer_segmentation'].value_counts(normalize=True) * 100).reset_index(name='percentage')
g = sns.barplot(x=percentage['percentage'], y=percentage['index'], data=percentage, palette="viridis")
sns.despine(bottom=True, left=True)
for i, v in enumerate(percentage['percentage']):
    g.text(v, i + 0.20, "  {:.2f}".format(v) + "%", color='black', ha="left")
g.set_ylabel('Segmentation')
g.set(xticks=[])
plt.show()
```
![RFM](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/d5260871-b1ed-4f88-8562-6818c11b5aa8)

Based on the analysis of customer segments derived from the query results, the following insights and CRM strategies can be outlined:

**Hibernating (39.82%):*

Customers who made purchases in the past, but infrequently and with low spending.
CRM Strategy: Send standard communications with offers and relevant product deals to encourage repeat purchases.

**About to Sleep (19.73%):*

Description: Recent buyers who are unsure about future purchases from the company or competitors.
CRM Strategy: Run promotional campaigns for a limited time, provide product recommendations based on their behavior, and emphasize the benefits of purchasing from the company.

**Promising (17.03%):*

- Description: Customers who show potential for becoming loyal due to their recent engagement and moderate spending.
- CRM Strategy: Nurture these customers with personalized recommendations, exclusive offers, and incentives to encourage repeat purchases and loyalty.


**New Customers (13.83%):*

- Description: Recently acquired customers who have yet to establish long-term engagement with the company.
- CRM Strategy: Provide a warm welcome with personalized onboarding messages, introductory offers, and guidance on product selection to encourage future interactions and repeat purchases.

**Potential Loyalist (8.57%):*

Description: Recent buyers with good spending habits and multiple purchases.
CRM Strategy: Offer a loyalty program, maintain engagement through personalized recommendations, and provide incentives for continued loyalty.

**Champions (0.48%):*

Description: Top-tier customers with significant spending and loyalty.
CRM Strategy: Maintain personalized communication, offer exclusive benefits, and provide VIP treatment to reinforce loyalty and advocacy.

**Need Attention (0.25%):*
- Description: Customers who have made recent purchases but exhibit signs of uncertainty or hesitation.
- CRM Strategy: Reach out to these customers with targeted communications, addressing any concerns or questions they may have, and providing reassurance to encourage continued engagement and loyalty.

**At Risk (0.18%):*

Description: Customers who used to purchase frequently but have not made recent purchases, indicating potential disengagement.
CRM Strategy: Reconnect with personalized communications, offer attractive deals, and emphasize the value of continued patronage.

**Loyal Customers (0.09%):*

Description: High-value customers who make frequent purchases.
CRM Strategy: Engage in personalized communication, avoid mass mailing of offers, provide tailored product recommendations, and encourage product reviews.




## Results/Findings

1. Order Count by Days of the Week:
   - The distribution of orders across different days of the week shows variations, with certain days seeing higher order volumes compared to others.
   - Further analysis could identify potential factors influencing daily order trends, such as promotional activities, customer behavior patterns, or external factors like holidays.

2. Monthly Orders for Delivered Orders:
   - The visualization illustrates the monthly distribution of delivered orders, providing insights into the volume of orders processed over time.
   - Peaks and troughs in order volumes may coincide with seasonal trends, marketing campaigns, or other external factors affecting consumer behavior.

3. Top 5 Fastest Delivery Sellers by Average Review Score:
   - This analysis identifies the top five sellers based on their average delivery times and review scores.
   - Sellers with fast delivery times and high review scores may enjoy a competitive advantage in attracting and retaining customers.

4. Category-Wise Distribution of Payment Installments:
   - The analysis reveals the distribution of payment installments across different product categories.
   - Understanding payment preferences can help optimize payment processing systems and tailor promotional offers to match customer preferences.

5. Top Regions with Highest Number of Installment Payments:
   - By identifying regions with the highest number of installment payments, businesses can target marketing efforts and tailor product offerings to meet the needs of these regions.

6. **Distribution of Orders Paid in Single and Multiple Installments:**
   - The analysis compares the distribution of orders paid in single and multiple installments across various product categories.
   - Insights from this analysis can inform inventory management and pricing strategies to accommodate different payment preferences.

7. Customer Segmentation Analysis:
   - Through RFM (Recency, Frequency, Monetary) analysis, customers are segmented into distinct groups based on their transactional behavior.
   - Customer segments such as "Champions," "Promising," and "New Customers" offer valuable insights for targeted marketing and customer relationship management strategies.

8. Customer Segmentation Results:
   - The segmentation analysis categorizes customers into distinct groups based on their RFM scores and behavioral patterns.
   - Each customer segment requires tailored marketing and retention strategies to maximize engagement and drive profitability.

These findings provide valuable insights for decision-making across various aspects of e-commerce operations, including marketing, customer service, logistics, and product management. Further exploration and refinement of these insights can lead to improved customer satisfaction, retention, and overall business performance.


## Recommendations
-On top of the RFM analysis, a customer lifetime value can be calculated to assess the long-term profitability of different customer segments. Therefore, marketers can better understand which customer segments contribute the most to revenue and prioritize marketing efforts to the target market accordingly.

### Limitations
- The e-commerce landscape in Brazil is constantly evolving, influenced by factors such as technology advancements, regulatory changes, and competitive pressures. Historical data may not fully capture these dynamic shifts.
- The dataset primarily focuses on transactions within the Olist platform, limiting insights into the broader e-commerce ecosystem in Brazil. Understanding competitive dynamics or market share may require data from multiple platforms.
  
### References

1. [PostgreSQL.org] (https://www.postgresql.org/docs/current/datatype-datetime.html)
2. Olist Store Ecommerce Dataset. Retrieved from [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce] 
4. Brazilian Institute of Geography and Statistics (IBGE), (1972). Brazilian Zip Code Geolocation Dataset. Retrieved from [https://www.ibge.gov.br/en/]
5. Pagan Research [https://paganresearch.io/company/olist]
6. VINICIUS DUZAC CERUTTI(2022) Retrieved from: [https://www.kaggle.com/code/ceruttivini/rfm-segmentation-and-customer-analysis]
7. KHUSHEE KAPOOR(2022) Retrieved from: [https://www.kaggle.com/code/khusheekapoor/relational-database-eda-data-preparation]

   


