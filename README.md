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

![ERD pgerd](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/a305011e-80b8-4e17-bcc7-a310872d9b06)

As can be depicted from the schema, the database contains seven eight tables. These tables are orders, sellers, order_items, order_reviews, order_payments, products, customers and the product_category_name_translation. We will examine each table independently and conduct pre-processing to minimize excess space usage.


### EDA( Exploratory Data Analysis)

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



### Data Analysis
```SQL
SELECT * from orders limit 10;
# To start, we view the first 10 orders of the dataset.

# The Customer Table, found in the customers_dataset, includes the following columns:
# customer_id: serves as the key to the orders dataset, ensuring each order has a unique customer_id.
# customer_unique_id: provides a unique identifier for each customer.

# In this system, each order is linked to a distinct customer_id, meaning the same customer may have different IDs for different orders. The inclusion of customer_unique_id allows for the identification of customers who have made repeat purchases from the store. Otherwise, each order would appear associated with a different customer.
# customer_zip_code_prefix: denotes the first five digits of the customer's zip code.
# customer_city: indicates the name of the customer's city.
# customer_state: specifies the customer's state.

SELECT count(order_id),
	EXTRACT(MONTH from order_approved_at) AS approved_month
FROM orders
GROUP BY approved_month
ORDER BY approved_month;

#We can now see the distribution of orders on a monthly basis.
```
- With the help of Matplotlib alongside the Seaborn library, we employ the barplot() function to visualize the distribution of orders across different months. Additionally, we leverage functions from the Matplotlib library to enhance the aesthetic appeal of the plot. As a result, we obtain a clear representation of the monthly order distribution.

``` Python

# We first start with importing the relevant libraries.

import numpy as np
import pandas as pd
import seaborn as sns
from matplotlib import pyplot as plt

# Then we import our CSV file to our Jupyter Notebook. Afterward, we remove any rows containing missing values (NaN values). This step ensures data cleanliness and prevents potential issues during analysis.

monthly_order_data= pd.read_csv(r"C:\Users\ASUS\Desktop\monthly_order.csv")
monthly_order_data.dropna(inplace=True)
monthly_order_data.approved_month=monthly_order_data.approved_month.astype(int)

#At last, we use the barplot() function to visualize the distribution of orders across different months.

plt.figure(figsize=(15, 8))
sns.barplot(x='approved_month', y='count', data=monthly_order_data.astype(int), palette=['brown'], linewidth=2, ci=None)
plt.title('Monthly Orders Over Time', color='white')
plt.xlabel('Months', color='white')
plt.ylabel('Number of Orders', color='white')
plt.show()

```

![monthly_order](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/9730eb6f-6e95-49ef-96d0-2eed594d2281)


 ``` SQL
#Although we did not filter explicitly for the order_status by using SQL, we found the order status friction of the monthly orders. 

Select count(order_id), order_status,
		extract(month from order_approved_at) as approved_month
from orders
group by order_status, approved_month
order by order_status desc, approved_month desc;

```


``` Python
# We will now filter the data for orders with order status 'unavailable' or 'cancelled' with Python. And we will again use a barplot() function to visualize the unavailable or cancelled orders by month on the x-axis. The frequency of orders will be depicted on the y-axis.

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

``` Python
#We will apply the same filter with orders where the order status is delivered. We will again use a barplot() function to visualize our graph. 

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

![order_satus_delivered](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/1f4f1003-91f9-4977-86c4-12727f07f442)


- After we examined the order statuses of the monthly orders, we will now examine the categories that stand out during special occasions such as Valentine's Day.
  
-- The Item Table, sourced from the "olist_order_items_dataset", consists of the following columns:

- order_id: A unique identifier for each order.
- order_item_id: A sequential number indicating the position of an item within the order.
- product_id: A unique identifier for each product.
- seller_id: A unique identifier for each seller.
- shipping_limit_date: The deadline set by the seller for handing over the order to the logistics partner.
- price: The price of the item.
- freight_value: The freight cost associated with the item. If an order contains multiple items, the freight cost is divided among them.

-- The Product Table contains the following columns:

- product_id: A unique identifier for each product.
- product_category_head: The root category of the product, originally in Portuguese.
- product_name_length: The length of the product name in characters.
- product_description_length: The length of the product description in characters.
- product_photos_qty: The number of photos published for the product.
- product_weight_g: The weight of the product measured in grams.
- product_length_cm: The length of the product measured in centimeters.
- product_height_cm: The height of the product measured in centimeters.
- product_width_cm: The width of the product measured in centimeters.

-- The Product Category Info Table contains the following columns:

- product_category_name: The category name was originally in Portuguese.
- product_name_english: The category name is translated into English.
  
``` SQL
#We took days between the first of February and the 13th of February to examine the product categories until Valentine's Day on the 14th of February. 

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
``` Python
#Once we import our CSV file to our Jupyter Notebook, we used a barplot() to visualize the top categories that were popular during the Valentine's Day shopping craze.

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

![valentines_day](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/803ac2fc-dc77-42b2-82be-532c1df4191b)

``` SQL
# Analyzing the number of orders based on the days of the week (e.g., Monday, Thursday) and the days of the month (e.g., 1st, 2nd, etc.).

Select count(order_id) as order_count,
to_char(order_purchase_timestamp, 'Day') as approved_day
from orders
group by approved_day
order by approved_day;

# Examining the order counts by the days of the week (e.g., Monday, Thursday) and the days of the month (e.g., 1st, 2nd, etc.).

Select count(order_id) as order_count, 
extract(day from order_purchase_timestamp) as days_of_the_month
from orders
group by approved_day, days_of_the_month
order by approved_day , days_of_the_month 
;
```
``` Python

#After importing our CSV file into Jupyter Notebook, we can proceed with visualizing our data. Depending on the nature of our analysis, we will utilize various visualization libraries such as Matplotlib, Seaborn, or Plotly.

days_order_count = pd.read_csv(r"C:\Users\ASUS\Desktop\days_order_count.csv")
days_order_count

# For this visualization, we used a pie chart to visualize the distribution of order counts by days of the week. 
plt.figure(figsize=(10, 6))
plt.pie(days_order_count['order_count'], labels=days_order_count['approved_day'], autopct='%1.1f%%', startangle=140)
plt.title('Order Count by Days of the Week')
plt.axis('equal')  
plt.show()

#Before creating visualizations for the days of the month order count, we needed to perform data preprocessing tasks. As such as cleaning the data to make it suitable for visualization.

days_of_the_month_order_count= pd.read_csv(r"C:\Users\ASUS\Desktop\days_of_the_month_ordercount.csv")

days_of_the_month_order_count_cleaned= days_of_the_month_order_count.dropna()
print(days_of_the_month_order_count_cleaned)

#The bar plot displays the distribution of order count across different days of the month. Each bar represents the number of orders received on a specific day of the month. 
From the visualization, we can observe some patterns:
- There is some variation in the number of orders throughout the month, with certain days having higher order counts than others.
- Some days show peaks in order counts, indicating periods of increased sales activity.
- Other days exhibit lower order counts, suggesting quieter periods in terms of order placements.
- Overall, there seems to be some variability in order volumes across different days of the month, which could be influenced by factors such as promotions, seasonality, or customer behavior. 

Further analysis could be conducted to identify any underlying trends or patterns driving these fluctuations in order counts on different days of the month.

plt.figure(figsize=(15, 8))
sns.lineplot(x='days_of_the_month', y='order_count', data=days_of_the_month_order_count_cleaned, ci=None) 
plt.title('Order Count by Days of the Month')
plt.xlabel('Days of the Month ')
plt.ylabel('Number of Orders')
plt.show()

```
![pie](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/c1331989-b400-4b79-aa99-e39c65a46dfa)

![linechart](https://github.com/denizyennerr/Brazilian_E-commerce_Analysis/assets/160275199/98ed5608-e7ab-4c63-9c5a-db88f8f58139)









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

   


