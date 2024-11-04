# PROJECT TITLE: LITA_CAPTONE_CUSTOMER-DATA

[Project Overview](#project-overview)

[Data Analysis Tools](#data-analysis-tools)

 [Structured Query Language](#structured-query-language)
 
 [Power BI](#power-bi)

[FINDINGS AND RECOMMENDATIONS](#findings-and-recommendations)

### Project Overview 

This is a Customer Segmentation for a Subscription Service , I am tasked with  analyzing customer data for a subscription service to identify
segments and trends. My goal is to understand customer behavior, track subscription types,
and identify key trends in cancellations and renewals.

### Data Analysis Tools

i. Microsoft Excel 
ii. Structured Query Language (SQL)
iii. Power BI

The first analytic tool I used in exploring the Customer Data is Excel and i used it to answer the following questions:

- Calculate the average subscription duration and identify the most popular subscription types.
- Analyze customer data using pivot tables to find subscription patterns.
- Create any other interesting reports.

I initially explored the dataset on an Excel Workbook and I used the Average formular and Count formular to calculate the average subscription duration 
and to identify the most popular subscription type.

```excel

=average(subscriptionstart,subscriptionend)= subscription duration

```

```excel
=count(subscriptiontypes colunm, a subscriptiontype)= most popular subscription type

```

The result of my Customer data can be found on my excel workbook [githubsales.xlsx](https://github.com/user-attachments/files/17618330/githubsales.xlsx)

I used Pivort tables and Pivort Charts to analyze subscription pattern

	
       Sum of Revenue by SUBSCRIPTION TYPE	

![image](https://github.com/user-attachments/assets/099625bb-c22c-4d36-9896-114ecb350c38)

    	Count of Subscription Duration by Region

![image](https://github.com/user-attachments/assets/abfdd535-1706-4a76-b1e8-9fb50755341d)
	
         Count of CustomerID in each Region per Subscription type

![image](https://github.com/user-attachments/assets/4a650420-585e-47d9-b52e-1beea92d9aab)


![image](https://github.com/user-attachments/assets/8a4cbbc6-e227-47ca-a6cb-9a44ca705abc)

![image](https://github.com/user-attachments/assets/d914525d-8130-4f27-9638-e62e57fa08dc)

![image](https://github.com/user-attachments/assets/8ca6498c-4b58-4dd2-a2e5-0dcfba887f85)




### Structured Query Language

This is the second tool i used to analyze the Customer Data. I imported the data into a databased I had created and started writing queries which i ran in order to get 
answers to the questions below:
In order to know if my data is correctly entered i ran this query to see my table

```sql

select * from customerdata

```
- retrieve the total number of customers from each region.
```sql

 select region, count (distinct customerid) as total_customers
 from [dbo].[CustomerData]
 group by Region 
 order by total_customers desc

```

 - find the most popular subscription type by the number of customers.

```sql

select subscriptionType ,
 count (customerid) as num_customers
 from CustomerData 
 group by SubscriptionType 
 order by num_customers desc

```

- find customers who canceled their subscription within 6 months.

```sql

select customerid, SubscriptionType ,SubDuration 
 as sub_duration
 from CustomerData 
 where Canceled = 'TRUE' AND SubDuration  <=180

```

- calculate the average subscription duration for all customers.

```sql

SELECT AVG(DATEDIFF(MONTH,SUBSCRIPTIONSTART,
 COALESCE(SUBSCRIPTIONEND, SUBSCRIPTIONSTART))) AS AVG_SUBDURATION
 FROM CUSTOMERDATA

```

 - find customers with subscriptions longer than 12 months.

```sql

SELECT CUSTOMERNAME,
 SUBSCRIPTIONSTART,SUBSCRIPTIONEND,
 DATEDIFF(MONTH, SUBSCRIPTIONSTART, COALESCE(SUBSCRIPTIONEND,SUBSCRIPTIONSTART))
 AS SUBDURATION FROM customerdata 
 WHERE DATEDIFF (MONTH,SUBSCRIPTIONSTART, COALESCE (SUBSCRIPTIONEND,SUBSCRIPTIONSTART))<=12
 ORDER BY SUBDURATION DESC

```

- calculate total revenue by subscription type.

```sql

SELECT REGION,
 SUM(REVENUE) AS TOTAL_REGIONAL_REVENUE
 FROM customerdata 
 GROUP BY REGION
 ORDER BY TOTAL_REGIONAL_REVENUE ASC

```

- find the top 3 regions by subscription cancellations.

```sql

SELECT TOP 3 REGION,
 COUNT (Canceled ) AS TOTALCANCELATION
 FROM customerdata 
 WHERE Canceled  IS NOT NULL
 GROUP BY REGION ORDER BY TOTALCANCELATION DESC
 
 ```
 
-  find the total number of active and canceled subscriptions.

```sql

SELECT SUM (CASE WHEN CANCELED IS NULL AND SUBSCRIPTIONEND>SUBSCRIPTIONSTART
 THEN 1 ELSE 0 END) AS TOTAL_ACTIVE_SUBS,
 SUM(CASE WHEN CANCELED IS NOT NULL THEN 1 ELSE 0 END) AS TOTAL_CANCELEDSUBS
 FROM CUSTOMERDATA

```

## Power BI: the third tool I used to create a report and visualization of all findings.

Firstly, I imported my Customer Data from Excel Workbook then transfrom the data to see how clean it is. 
I created some measures such as 

i. Average revenue
ii. Average Subscription Duration
iii. Total revenue



Include slicers for interactive analysis.

![Screenshot (29)](https://github.com/user-attachments/assets/9fb42112-80df-479a-a769-c26d48671c20)


## FINDINGS AND RECOMMENDATIONS

From the Analysis conducted on the Customer Data, the following are the findings:

a. There are theree Subscription Types namely Basic, Premium and Standard.
b. The Most Popular Subscription Type is Basic with 16,921 Subscribers while others had 8446, 8420 respectively.
c. The Average Duration Subscription for all the subscription types is 365.
d. 





