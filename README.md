# SQL Restaurant Analysis Project

## Problem Statement
You've just been hired as a Data Analyst for a restaurant that offers a diverse menu and serves generous portions. The restaurant debuted a new menu at the start of the year, and You have been asked to delve into the customer data to determine which menu items are performing well or poorly and to identify the preferences of our top customers


## Dataset

[Rsetaurant_Orders _Database](https://mavenanalytics.io/data-playground?page=2&pageSize=10)


## Objective

1. Explore the menu_items table to get an idea of what's on the new menu.
2. Explore the order_details table to get an idea of the data that's been collected.
3. Use both tables to understand how customers are reacting to the new menu.


## Common Questions For Analysis

#### View the menu _ items table.

    select * from menu_items;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/1.png)


#### Find the number of items on the menu.

    select count(*) from menu_items;


![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/2.png)
 
 There are total 32 items on menu.

#### What are the least and most expensive items on the nenu?

    select * from menu_items order by price;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/3.1.png)



    select * from menu_items
    order by price desc;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/3.png)

#### How many Italian dishes are on the menu?

    select * from menu_items 
    where category ="Italian";

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/4.png)

#### What are the least and most expensive Italian dishes on the menu?

    select * from menu_items 
    where category ="Italian"
    order by price;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/5.1.png)

    select * from menu_items 
    where category ="Italian"
    order by price desc;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/5.2.png)


#### How many dishes are in each category?

    select category, count(menu_item_id) from menu_items 
    group by category;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/6.png)

 #### What is the average dish price within each category?

    select category, avg(price) from menu_items 
    group by category;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/7.png)

#### View the order details table.

    select * from order_details;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/8.png)

#### What is the date range of the table?

    select min(order_date), max(order_date) from order_details;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/9.png)

#### How many orders were made within this date range?

    select  count(distinct order_id) from order_details;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/10.png)

#### How many items were ordered within this date range?

    select count(*) from order_details;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/11.png)

#### Which orders had the most number of items?

    select order_id, count(item_id) as num_items from order_details
    group by order_id order by num_items desc;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/12.png)

#### How many orders had more than 12 items?

    select count(*) from
    
    (select order_id, count(item_id) as num_items from order_details
    group by order_id having num_items > 12) as num_orders ;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/13.png)

#### Combine the menu _ Items and order_details tables into a single table.

    select * 
    from order_details od left join menu_items mi
    	on od.item_id=mi.menu_item_id;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/14.png)

#### What were the least and most ordered items? What categories were they in?

    select item_name,category, count(order_details_id) as num_purchases
        from order_details od left join menu_items mi
        	on od.item_id=mi.menu_item_id
            group by item_name, category
            order by num_purchases ; 


![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/15.2.png)

    select item_name,category, count(order_details_id) as num_purchases
    from order_details od left join menu_items mi
    	on od.item_id=mi.menu_item_id
        group by item_name, category
        order by num_purchases desc; 

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/15.1.png)

#### what were the top 5 orders that spent the most money?

    select order_id, sum(price) as total_spend
    from order_details od left join menu_items mi
    	on od.item_id=mi.menu_item_id
        group by order_id
        order by total_spend desc
        limit 5;


![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/16.png)

#### View the details of the highest spend order. What insights can you gather from the results?

    select category, count(item_id) as num_item
    from order_details od left join menu_items mi
    	on od.item_id=mi.menu_item_id
        where order_id= 440
        group by category;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/17.png)

#### View the details of the top 5 highest spend orders. What insights can you gather from the results?

    select order_id, category , count(item_id) as num_item
    from order_details od left join menu_items mi
    	on od.item_id=mi.menu_item_id
        where order_id in (440, 2075, 1957, 330, 2675)
        group by order_id, category;

![enter image description here](https://github.com/DataAnalystChetan/Restaurant-Orders-Analysis-SQL-Project/blob/main/Query%20Output%20Images/18.png)







