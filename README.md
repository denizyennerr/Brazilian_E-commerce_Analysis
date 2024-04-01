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

### Project Overview

This data analysis project aims to analyze a public dataset of e-commerce orders from the Olist Store. The dataset comprises information on 100,000 orders made between 2016 and 2018 across multiple marketplaces in Brazil. 
It provides insights into various aspects of the orders, including order status, pricing, payment and freight performance, customer location, product attributes, and customer reviews.

### Data Sources

Olist Store E-commerce Dataset: A public dataset provided by Olist contains information on 100,000 e-commerce orders made between 2016 and 2018 across multiple marketplaces in Brazil. 

Brazilian Zip Code Geolocation Dataset: A supplementary dataset that relates Brazilian zip codes to latitude/longitude coordinates.


### Tools

- Excel- Data Cleaning
   - [Download here] (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- PostgreSQL- Data Analysis
- Python- Data Visualisation


#Data Cleaning/Preparation

In the initial data preparation phase, the following tasks were performed:
1. Data Loading and inspection.
2. Handling missing values.
3. Data cleaning and formatting.

### EDA( Exploratory Data Analysis)

EDA involved exploring the Olist dataset to answer key questions, such as:

- How have the order statuses (e.g., delivered, shipped, canceled) varied over the years 2016-2018?
- In which regions do users who have more installments for payment primarily live?
- Which sellers sell products across a wider range of categories? Do sellers with a wider range of categories also have higher order counts?

### Data Analysis

- In which regions do users who have more installments for payment primarily live?

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

   


