
# Sales-Dashboard

## Problem Statement

This dashboard helps a pizza company gain insights into its sales performance and customer preferences. By visualizing data such as sales trends, customer demographics, and product popularity, the company can identify areas for operational and marketing improvements. The analysis provides actionable recommendations to enhance customer satisfaction and increase revenue.


### Steps followed 

- Data Extraction with SQL: 
    
    (a) Queried the database to extract relevant data, focusing on key metrics like sales by product, customer segments, and regional performance.
   
    (b) Wrote SQL queries to calculate KPIs such as total revenue, average order value, total pizzas sold, total orders, and average pizzas per order.

    (c) Developed queries for trends, including daily and monthly order trends, percentage sales by pizza category and size, and total pizzas sold by category.

    (d) Identified top 5 best and worst-selling pizzas by revenue, total quantity sold, and total orders.

    (e) Documented all SQL queries for reproducibility and data transparency.

- Data Preparation and Cleaning: Ensured data completeness and accuracy by handling missing values and refining datasets.

- Dashboard Development in Power BI:
    
    (a) Loaded the cleaned data into Power BI Desktop.

    (b) Created DAX measures for calculating KPIs and enhancing visual interactivity.

    (c) Designed interactive visuals, including: Column & Line charts for sales trends over time. Bar charts for and product-level sales. Slicers for filtering by product categories and time periods.

    (d) Developed two Power BI slides:
    
    Trend Analysis Slide: Displays daily and monthly trends for total orders, percentage sales by pizza category and size, and total pizzas sold by category.Includes KPIs such as total revenue, average order value, total pizzas sold, total orders, and average pizzas per order.

    Best and Worst Sellers Slide: Highlights top 5 best and worst-selling pizzas based on revenue, quantity, and total orders. Includes KPIs for a comprehensive performance summary

        
# SQL queries
### KPIs

    (1)Total Revenue – Sum of total price

select cast(SUM(total_price) as decimal(10,3)) as Total_Revenue from Pizza_sales

![SQL pizza 1](https://github.com/user-attachments/assets/be123b9c-2302-42bb-b2d0-709201452593)

    (2) Avg Order value – Sum of total price/ Count of Total orders (Distinct)

select cast(sum(total_price)/ count(distinct order_id) as decimal(10,2)) as Avg_Order_Value from pizza_sales

![image](https://github.com/user-attachments/assets/e771126d-51c2-4f4e-b6b1-500ce9821f09)

    (3)Total Pizzas sold – Sum of quantity

select SUM(quantity) as Total_Pizzas_Sold from pizza_sales

![kpi pizza 3](https://github.com/user-attachments/assets/614eb4dd-7b36-4bc4-aa95-bfd69b165a35)

    (4)Total Orders – Distinct count of orders

select count(distinct order_id) as Total_Orders from pizza_sales

![kpi pizza 5](https://github.com/user-attachments/assets/ef774a74-4a77-4330-a8b3-d7adedb4d673)

    (5)Avg Pizzas per order –Sum of quantity/Count of orders (Distinct)

select cast(sum(quantity) as decimal(10,2))/ cast(Count(distinct order_id) as decimal(10,2)) as Avg_Pizzas_Per_Order from pizza_sales

## Chart Requirements

    (1)Daily Trend for Orders
select datename(DW, order_date) as WeekDay, count(distinct order_id) as Total_Orders from pizza_sales
group by datename(DW, order_date)

![image](https://github.com/user-attachments/assets/d8f7aacc-a567-4c9c-81bb-45e7641227b9)

    (2) Monthly Trend for the orders
select datename(Month, order_date) as Month, count(distinct order_id) as Total_Orders from pizza_sales
group by datename(Month, order_date)
order by Total_Orders DESC

![image](https://github.com/user-attachments/assets/2197c68c-3a2d-4009-9b45-127297b3cd14)

    (3) Percentage of sales by pizza category

select * from pizza_sales
select pizza_category, sum(total_price)*100/(select sum(total_price)from pizza_sales where month(order_date)=1) as PCT from pizza_sales
where month(order_date)=1
group by pizza_category

![image](https://github.com/user-attachments/assets/f6b9bcfc-68b2-4077-ae9e-f636fd0fdbaa)

    (4) Percentage of sales by Pizza size
select pizza_size, sum(total_price)*100/(select sum(total_price) from pizza_sales) as PCT from pizza_sales
Group by pizza_size
order by PCT DESC

![image](https://github.com/user-attachments/assets/45e7d6da-605b-46ac-a194-53e38beb4cd2)


    (5) Top 5 best/ worst sellers by revenue, Total Quantity, Total Orders

- Five Best (Revenue)

select Top 5 pizza_name, sum(total_price) as Total_revenue from pizza_sales
group by pizza_name
order by Total_revenue DESC

![image](https://github.com/user-attachments/assets/a2c47c5b-f91a-45f8-88e3-bc8c02a91bdd)


- Five Best (Total Quantity)

select Top 5 pizza_name, sum(quantity) as Quantity from pizza_sales
group by pizza_name
order by Quantity DESC

![image](https://github.com/user-attachments/assets/a64217e4-414d-406c-bd56-32c8b1daba38)


- Five Best (Total Orders)

select Top 5 pizza_name, count(distinct order_id) as Total_Orders from pizza_sales
group by pizza_name
order by Total_Orders DESC

![image](https://github.com/user-attachments/assets/ab526e71-293e-4462-8e73-d013730fe390)


- Five Worst (Revenue)

select Top 5 pizza_name, cast(sum(total_price) as decimal(10,0)) as Total_revenue from pizza_sales
group by pizza_name
order by Total_revenue ASC

![image](https://github.com/user-attachments/assets/92ca6603-e918-4632-8699-4cc278b0201a)


- Five Worst (Total Quantity)

select Top 5 pizza_name, sum(quantity) as Quantity from pizza_sales
group by pizza_name
order by Quantity ASC

![image](https://github.com/user-attachments/assets/08a32158-889f-4369-8d1e-48874d87c335)


- Five Worst (Total Orders)

select Top 5 pizza_name, count(distinct order_id) as Total_Orders from pizza_sales
group by pizza_name
order by Total_Orders ASC

![image](https://github.com/user-attachments/assets/115b6879-e825-4684-8674-5d6da459bb33)


# Snapshot of Dashboard (Power BI) -Trend Analysis
![Pizza 1](https://github.com/user-attachments/assets/f64ae94c-dba0-47c2-ad5b-ca554e8bf603)

# Snapshot of Dashboard (Power BI) - Best/Worst Sellers
![Pizza 2](https://github.com/user-attachments/assets/2537599d-d3e9-44d2-9f86-7d3eb2fadb5b)

# Insights

- Top-Selling Products: Identified the most popular pizza types, enabling targeted marketing campaigns.

- Customer Segmentation: Recognized customer groups with the highest purchasing frequency, guiding loyalty program development.

- Sales Trends: Daily and monthly analysis provides granular insights into ordering patterns.

- Performance Insights: Top 5 best and worst-selling pizzas by revenue, total quantity sold, and total orders provide actionable intelligence for inventory and menu optimization.

# Key Visuals
- Trend Analysis:
    
    (a) Column and Line chart for daily and monthly order trends.

    (b) Donut charts for percentage sales by pizza category and size.

    (c) Category funnel for Total pizzas sold by category.

    (d) KPI cards for total revenue, average order value, total pizzas sold, total orders, and average pizzas per order.

- Best and Worst Sellers:

    (a) Bar charts highlighting top 5 best and worst sellers based on revenue, total quantity, and total orders.

    (b) KPI cards for quick performance insights.

# Tools Used
- SQL: For data extraction and transformation.

- Power BI: For data visualization and dashboard creation.

- DAX: For creating custom measures and KPIs.
