# LITA_CAPTONE_CUSTOMER-DATA

### Project 2 Overview Customer Segmentation for a Subscription Service

### Microsoft Excel 

This is the first analytic tool I used in exploring the Customer Data and i used it to answer the following questions:

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

### Power BI: the third tool I used
o Build a Power BI dashboard that visualizes key customer segments,
cancellations, and subscription trends. Include slicers for interactive analysis.
