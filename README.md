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












2. SQL:
Hint – You need to load the dataset into your SQL Server environment to write
and validate your queries.
Write queries to extract key insights based on the following questions.
o retrieve the total number of customers from each region.
o find the most popular subscription type by the number of customers.
o find customers who canceled their subscription within 6 months.
o calculate the average subscription duration for all customers.
o find customers with subscriptions longer than 12 months.
o calculate total revenue by subscription type.
o find the top 3 regions by subscription cancellations.
o find the total number of active and canceled subscriptions.
3. Power BI:
o Build a Power BI dashboard that visualizes key customer segments,
cancellations, and subscription trends. Include slicers for interactive analysis.
