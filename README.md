# PROJECT TITLE: LITA_CAPSTONE_PROJECT SALES DATA

[Project Overiew](#project-overview)

[Analysis Tools](#analysis-tools)

[OUTCOME OF SALES DATA PROJECT USING MICROSOFT EXCEL](#outcome-of-sales-data-project-using-microsoft-excel)

[Structured Query Language (SQL)](#structured-query-language-sql)

[Microsoft Power BI](#microsoft-power-bi)

[FINDINGS AND RECOMMENDATIONS](#findings-and-recommendations)

## Project Overiew

This is a Sales Performance Analysis for a Retail Store, I am tasked  with analyzing the sales performance of a retail store.
You will need to explore sales data to uncover key insights such as top-selling products, regional
performance, and monthly sales trends. The goal is to produce an interactive Power BI
dashboard that highlights these findings


## Analysis Tools

i. Microsoft Excel [Download Here](https://www.microsoft.com)
ii. Structured Query Language
iii. Microsoft PowerBI

I am to explore the Sales Data to uncover key insights such as top-selling products, regional
performance, and monthly sales trends. With my Excel tool i will 
- Perform an initial exploration of the sales data.
- Use pivot tables to summarize; Total sales by product, region, and month.
- Use Excel formulas to calculate metrics such as average sales per product and total revenue by region.
- Create any other interesting report.

## OUTCOME OF SALES DATA PROJECT USING MICROSOFT EXCEL 

The first thing I did was to calculate the revenue for each of the row on the Sale Dataset by multiplying the Quantity row by the UnitPrice row

```excel
=F2*G5

```

For the result i got from the dataset worked on

[githubsales.xlsx](https://github.com/user-attachments/files/17611792/githubsales.xlsx)


For easier visualization I added a screenshoot of my outcome

![Screenshot (15)](https://github.com/user-attachments/assets/6b361139-27fb-49a5-8d1a-359eec088c9b)

I thereaffter went on to use Pivot Table to create beautiful and interesting reports showcasing 

a. Total Sales by Product
b. Total Sales by Region
c. Total Sales by Month
d. Top-Selling Product
e. Average Sales by Product

          TOTAL SALES BY PRODUCT	
![image](https://github.com/user-attachments/assets/de5a50f4-f34f-4a56-a27f-6c69a39fae66)

         TOTAL SALES BY REGION	
![image](https://github.com/user-attachments/assets/2b3e18a2-0533-4039-b23c-51fff26718e5)


         TOTAL SALES BY MONTH	
![image](https://github.com/user-attachments/assets/786dcd11-3d6b-4e58-afb3-d0c3aa2dd5ac)


        TOP SELLING PRODUCT BY REVENUE					
![image](https://github.com/user-attachments/assets/6947daa6-a0cf-4760-b313-f58ebc403ac4)


        TOP SELLING PRODUCT	
![image](https://github.com/user-attachments/assets/db5ab314-e904-419b-9f0c-e14567f14cfc)


         AVERAGE SALE PER PRODUCT BY REVENUE		
![image](https://github.com/user-attachments/assets/fb6c2837-1dd0-411b-81f0-fb636aa067c6)


        AVERAGE SALES PER PRODUCT		
![image](https://github.com/user-attachments/assets/5e6c2630-bcf2-4e22-b185-a9aca8235802)


Pivort Charts were also added in order for the Sales Overview to be visualized


![image](https://github.com/user-attachments/assets/1473f90f-4515-4a9d-bcc9-133b36735164)


![image](https://github.com/user-attachments/assets/beffa1c9-478b-40b1-9cc3-dad73d79fced)


![image](https://github.com/user-attachments/assets/41e24773-78d3-4e73-9a5b-deca48cf7f05)



## Structured Query Language (SQL)

This is the second Analysis tool I used in exploring the Sales Dataset in this project. SQL means standard language for accessing, managing and modifying data in a relational dtatabase.

I used the SQL Tool to answer the following questions after I had successfully imported my data into a database i created which I named LITA_DB.

- retrieve the total sales for each product category.
- find the number of sales transactions in each region.
- find the highest-selling product by total sales value.
- calculate total revenue per product.
- calculate monthly sales totals for the current year.
- find the top 5 customers by total purchase amount.
- calculate the percentage of total sales contributed by each region.
- identify products with no sales in the last quarter.

I ran various codes in order to be able to extract the neccesary information i needed which are embedded in the Salesdata Table on my LITA_DB

```sql
select *from[dbo].[SalesData]

      
- TOTAL REVENUE PER PRODUCT

```sql

SELECT sum (revenue)as totalsale4hat FROM SalesData WHERE PRODUCT = 'HAT'

SELECT sum(revenue) as totalsale4shoes FROM SalesData WHERE PRODUCT = 'SHOES'

SELECT sum(revenue) as totalsales4shirt FROM SalesData WHERE PRODUCT = 'SHIRT'

SELECT sum(revenue) as totalsales4gloves FROM SalesData WHERE PRODUCT = 'GLOVES'

SELECT sum(revenue)as totalsales4socks FROM SalesData WHERE PRODUCT = 'SOCKS'

SELECT sum(revenue) as totalsale4jacket  FROM SalesData WHERE PRODUCT = 'JACKET'

```

- Find The Number Of Sales Transactions In Each Region.

```sql

SELECT REGION,
count(orderid)as regionalsales from [dbo].[SalesData] 
GROUP BY REGION
ORDER BY regionalsales DESC

```

- HIGHEST SELLING PRODUCT BY TOTAL SALES VALUE

```sql

select top 1 (product),
sum (revenue) as totalsales from [dbo].[SalesData]
group by product

```
- TOTAL REVENUE PER PRODUCT

```sql

SELECT PRODUCT,
SUM(REVENUE) AS TOTALREV FROM[dbo].[SalesData]
GROUP BY PRODUCT
ORDER BY TOTALREV DESC

```
- MONTHLY SALES TOTAL FOR THE CURRENT YEAR

```sql

SELECT MONTH (ORDERDATE)AS MONTHS,
SUM (REVENUE) AS MONTHLYSALES
FROM[dbo].[SalesData]
WHERE
YEAR(ORDERDATE)= YEAR (GETDATE())
GROUP BY MONTH (ORDERDATE) 
ORDER BY MONTHS

```

- TOP 5 CUSTOMERS BY TOTAL PURCHASE AMOUNT

  ```sql
  
SELECT TOP 5 (CUSTOMER_ID) AS TOPCUSTOMER,
SUM (REVENUE) AS TOTAL_PURCHASEPRICE FROM [dbo].[SalesData] 
GROUP BY Customer_Id 
ORDER BY TOPCUSTOMER DESC

```
- PERCENTAGE OF TOTAL SALES CONTRIBUTED BY EACH REGION

```sql
SELECT REGION,
SUM(REVENUE) AS TOTAL_SALES,
(SUM(REVENUE)*100.0/(SELECT SUM(REVENUE) FROM[dbo].[SalesData]))
AS PERCENTAGE_TOTAL_SALES
FROM [dbo].[SalesData] 
GROUP BY REGION
ORDER BY PERCENTAGE_TOTAL_SALES DESC

```
- PRODUCTS WITH NO SALES IN THE LAST QUARTER

```sql

SELECT OrderID,
Product 
FROM [dbo].[SalesData] WHERE OrderID  NOT IN (SELECT OrderID 
FROM [dbo].[SalesData]
WHERE OrderDate >=
DATEADD (QUARTER, -1,GETDATE ()))

```

```sql

SELECT OrderID  
 FROM SalesData 
 WHERE Product NOT IN (
 SELECT DISTINCT Product  
 FROM SalesData  WHERE OrderDate between
 dateadd (quarter, -1, getdate())
 and getdate())

```


## Microsoft Power BI

 This is the third Analysis Tool I used in exploration of the Sales Data. PowerBI is a business analytics service by Microsoft that enables users
 to visualize and Analyze data from various sources. It provides interactive dashboards, reports and data visualization tools
 to help organizations make data-driven decisions.

 I am tasked to use PowerBI to:
 
- Create a dashboard that visualizes the insights found in Excel and SQL. The dashboard should include a sales overview, top-performing products, and
regional breakdowns.

The first step I took was to get my data from Excel Workbook, transform my data and check the data quality, profile and distribution. After transfroming my data into a clean state 
I proceeded to create the following Visuals from my dataset.


![Screenshot (26)](https://github.com/user-attachments/assets/6d7bba5a-dd33-40fc-8185-950557ae8ac3)

- Regional Performance
- Monthly Overview of Sales for Year 2023 and 2024
- Sum of Quantity by Product
- Sum of Revenue by Product

![Screenshot (25)](https://github.com/user-attachments/assets/a32c4e43-904d-4de9-ab56-7bae55a20a90)

Slicers for Product and Region was added to create and interesting report and dashboard



## FINDINGS AND RECOMMENDATIONS  

 #### Prouct Performance 
 
 - My analysis reveals that 'Hat' has the highest sales with a total of 15,929 showing a strong and steady market demand.
 - Shoes generated the most revenue with a total of 613,380.
 - There is room for sales improvement by conducting regular customer feedbacks in order to know why some products are raking in low sales.

![image](https://github.com/user-attachments/assets/a956dc78-c7e1-47d9-acfb-f30eedca61ce)

![image](https://github.com/user-attachments/assets/52c73d78-bd0a-4f31-9125-c24c6a9968ab)


   
#### Regional Performance

- Amongst the four (4) regions in the dataset, South had the most sales with a total 927,820
while West generated the lowest sales with a total of 300,345.
- This shows that there need for sales awareness e.g advertising, marketing to be created in the West region in order to boost their sales.
   Offer Sales plan and also Easy buy plan in the West.
![image](https://github.com/user-attachments/assets/3c4dec63-f6b4-46b1-a800-48a872c279a6)


#### Monthly Sales Trend 

- Sales were higher in the month of February of both year 2023 and 2024 while in year 2023 April sales was
the lowest with a total sales of 7,425 and in year 2024 July had the lowest sales with a total of 37,200.
- There is need for the organization to conduct a sales poll in order to know why sales are particularly low in April of 2023 and 2024
  this will give an insight into how sales can be boosted in those months in the coming year.
 
![image](https://github.com/user-attachments/assets/f05d7c68-7d7d-48e9-892b-3f0d84f8f995)







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

## Power BI 

This is the third tool I used to create a report and visualization of all findings.Firstly, I imported my Customer Data from Excel Workbook then transfrom the data to see how clean it is. 
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

The Organizaton can improve their customer's subscription pattern by making subscription types more attractive and not too expensive.








