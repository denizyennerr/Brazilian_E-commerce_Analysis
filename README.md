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

This data analysis project focuses on exploring a public dataset of e-commerce orders from Olist. Olist is a prominent online e-commerce platform connecting merchants to the main marketplaces of Brazil. The dataset comprises of 100,000 orders between 2016 and 2018, and it offers valuable information on various aspects of the customer journey, including order status, pricing, payment, and customer reviews.

Presented by Olist, this dataset underscores the platform's success in streamlining e-commerce operations for merchants across Brazilian marketplaces. Through innovative solutions, Olist facilitates seamless connections between merchants and consumers, fostering a unified and efficient e-commerce ecosystem.

This analysis will delve deeper into understanding the customer journey, comparing seller orders and their delivery times, and analyzing payment methods and payment installment patterns across different regions. Lastly, it will conduct an RFM (Recency, Frequency, Monetary) analysis, and thanks to this segmentation it will reveal the loyal customers and potential retention customers. By unlocking the power of Brazilian e-commerce through data-driven insights, one can reach important findings that can contribute to strategic decision-making and drive further growth in the e-commerce landscape.


### Tools

- Excel- Data Cleaning
   - [Download here] (https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)
- PostgreSQL- Data Analysis
- Python- Data Visualisation

### Data Cleaning/Preparation

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
5. Pagan Research [https://paganresearch.io/company/olist]

   


