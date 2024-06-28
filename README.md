# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
Project Goal is to create a database ecommerce in pgadmin. After that we have to import five csv files i.e all sessions, products, analytics, sales by sku and sales report. Then we have to clean our data inside the five datasets given and transform it to reach our objectives that are the five questions asked in starting with questions file.
## Process
### 
Provide relevant data types to the columns after scrutinizing the table.
Clean the data given in Excel using functions.
Clean the data in the given tables by using queries.
Create a view for each table so that if any function performed would not hamper the original table.


### 
Create an algorithm for each question first.
Apply relevant functions to retrieve data to reach objective.
## Results
SELECT als.city,als.country, SUM (als..productprice*sbs.total_ordered) AS total_revenue
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.city,als.country
ORDER BY total_revenue DESC;
-- uses alias als for all_sessions and sbs for sales_by_sku
uses a join with primary key being productsku
uses the sum of the product of column productprice in all_sessions and total_ordered in sales_by_sku to create a new column total_revenue.
I grouped the query by city and country to retrieve data.


 SELECT als.country,als.city,AVG (sbs.total_ordered) as avg_prod
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.country,als.city
ORDER BY avg_prod DESC
--used a join to calculate average products ordered by visitors in different city and country


SELECT DISTINCT (v2productcategory) AS product_category, als.city,als.country
FROM all_sessions als
WHERE als.v2productcategory LIKE '%Home/Apparel%'
GROUP BY als.city,als.country
ORDER BY product_category
--to see a specific pattern we can use LIKE keyword to search for specific strings in a column. Here I selected Home/Apparel which can be changed accordingly.




SELECT DISTINCT COUNT(p.name) as top_orders,
COUNT (als.productsku) as products_ordered,als.city as city_top,als.country as country_top,
RANK() OVER (ORDER BY COUNT(als.productsku) DESC) AS ranking
FROM all_sessions als
JOIN products p
ON als.productsku = p.sku
WHERE als.city NOT LIKE 'not available in demo dataset'
GROUP BY p.name,als.city,als.country
ORDER BY products_ordered DESC;

## Challenges 
Time constraint 
Data cluttered

## Future Goals
To clean data more efficiently with merging queries and more distinct functions to provide optimal solution
