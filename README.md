# Kultra Mega Stores Inventory


# Kultra Mega Stores Inventory 
## Company Overview 
Kultra Mega Stores (KMS), headquartered in Lagos, specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria. 
You have been engaged as a Business Intelligence Analyst to support the Abuja division of KMS. The Business Manager has shared an Excel file containing order data from 2009 to 2012 and has requested that you analyze the data and present your key insights and findings. 
Apply your SQL skills from the DSA Data Analysis class and solve both case scenarios as shared in the document. 

## Case Scenario I 
1. Which product category had the highest sales? 
2. What are the Top 3 and Bottom 3 regions in terms of sales? 
3. What were the total sales of appliances in Ontario? 
4. Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers 
5. KMS incurred the most shipping cost using which shipping method? 
6. Who are the most valuable customers, and what products or services do they typically purchase? 
7. Which small business customer had the highest sales? 
8. Which Corporate Customer placed the most number of orders in 2009 – 2012? 
9. Which consumer customer was the most profitable one? 
10. Which customer returned items, and what segment do they belong to? 
11. If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority? Explain your answer


# 1. Which product category that has the highest 
```SQL
- Select top 1 Product_NAME, sales
from Kultra_Mega_Stores
order by sales desc;
``` 

# 2. What are the top 3 and buttom 3 region in terms of sales 
``` SQL
Top 3 sales

Select top 3 region, sales
from Kultra_Mega_Stores
order by sales desc;
``` 
Bottom 3 sales
``` SQL
Select top 3 region, sales
from Kultra_Mega_Stores
order by sales asc;
``` 
# 3. what were  the Total Sales of applicants in ontario?
``` SQL
-Select  sum(sales) as Total_sum_Ontario
from Kultra_Mega_Stores
where region in ('Ontario')
Group by region
``` 
# 4. Advice the management of KMS on what to do to increase the revenue from the buttom 10 customer 
``` SQL
-Select top 10 discount, sales, Shipping_cost
from Kultra_Mega_Stores
order by sales asc;
``` 
- my advise  to the management of KMS to increase the revenue from the bottom 10 customers  is to either increse the discount  for the customers or reduce the shipping cost this  may motivate them to buy more. As shown in the data these customers have lowest discount  although their shipping cost is not high

# 5. KMS incurred the Most shipping cost using which shipping method ?
``` SQL
-Select Ship_Mode as Ship_Mode2,  
sum (shipping_cost) as
total_shipping_cost
from Kultra_Mega_Stores
group by ship_mode
order by total_shipping_cost desc
``` 
# 6. Who are the most valuable customer, and what products or services did they typically purchase?
``` SQL
select customer_name, product_name
-sum (Sales) as total_spent
from Kultra_Mega_Stores
group by customer_name, product_name
order by total_spent desc;
``` 

# 7. Which small business customer have the highest sales ?
``` SQL
-select top 1 * from Kultra_Mega_Stores
where Customer_Segment in ('Small Business')

``` 
# 8. Which corporate customer placed the most number of orders in 2019 -2012?
``` SQL
-select top 1 Customer_name, Order_date, Customer_Segment, Order_Quantity
from Kultra_Mega_Stores
where Customer_Segment = 'Corporate' and Order_Date > '2008'
order by Order_Quantity desc
``` 
# 9. Which consumer customer was the most profitable one?
``` SQL
-select top 1 Customer_name, profit, Customer_Segment, Order_Quantity
from Kultra_Mega_Stores
where Customer_Segment = 'consumer' 
order by profit desc
``` 
# 10. Which customer returned items, and what segments do they belong to?
``` SQL
-select Customer_Name,Customer_Segment,[Status]
from [Kultra_Mega_Stores1]
join [dbo].[Order_Status]
on [Kultra_Mega_Stores1].Order_ID = [dbo].[Order_Status].[Order_ID]
``` 
# 11. If the delivery truck is the most economical but the lowest shipping method and express air is the fastest.
but the most expensive one, did you think the company appropriately spent shipping costs based on the order priority.
``` SQL
-Select Order_Priority, Ship_Mode,
    COUNT([Order_ID]) AS [order count],
    SUM(sales - profit) AS [Estimated shipping cost],
    AVG(DATEDIFF(DAY, [Order_Date], [Ship_Date])) AS [Avg ship date]
from  [KMS Sql Case Study1] 
group by Order_Priority,Ship_Mode
order by  Order_Priority,Ship_Mode desc
``` 
