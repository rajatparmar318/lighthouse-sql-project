Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SELECT als.city,als.country, SUM (als..productprice*sbs.total_ordered) AS total_revenue
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.city,als.country
ORDER BY total_revenue DESC;








**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries: SELECT als.country,als.city,AVG (sbs.total_ordered) as avg_prod
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.country,als.city
ORDER BY avg_prod DESC








**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
SELECT DISTINCT (v2productcategory) AS product_category, als.city,als.country
FROM all_sessions als
WHERE als.v2productcategory LIKE '%Home/Apparel%'
GROUP BY als.city,als.country
ORDER BY product_category









**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
SELECT DISTINCT COUNT(p.name) as top_orders,
COUNT (als.productsku) as products_ordered,als.city as city_top,als.country as country_top,
RANK() OVER (ORDER BY COUNT(als.productsku) DESC) AS ranking
FROM all_sessions als
JOIN products p
ON als.productsku = p.sku
WHERE als.city NOT LIKE 'not available in demo dataset'
GROUP BY p.name,als.city,als.country
ORDER BY products_ordered DESC;









**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
SELECT als.city,SUM(als.productprice*sbs.total_ordered) as impact_generated,
RANK() OVER (ORDER BY COUNT(als.city) DESC) as ranking
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.city
ORDER BY impact_generated DESC;
--for city


SELECT als.country,SUM(als.productprice*sbs.total_ordered) as impact_generated,
RANK() OVER (ORDER BY COUNT(als.country) DESC) as ranking
FROM all_sessions als
JOIN sales_by_sku sbs
ON als.productsku=sbs.products_sku
GROUP BY als.country
ORDER BY impact_generated DESC;
--for country












