What issues will you address by cleaning the data?

Data-type Constraints: values in a particular column must be of a particular type. 
Range Constraints: data should fall within a range. For example, the order date should not be in the future.
Mandatory Constraints: certain columns cannot be empty. For example, orderid, customerid should never be empty.
Unique Constraints: some fields must be unique. For customerid should always be unique.





Queries:
Below, provide the SQL queries you used to clean your data.

UPDATE all_sessions
SET ecommerceaction_option='online'
WHERE ecommerceaction_option IS NULL
--similarly we can add data into columns having no information

DELETE FROM all_sessions_view
WHERE fullvisitorid NOT IN 
(SELECT MIN(fullvisitorid)
	FROM all_sessions_view
	GROUP BY city,country)
 --deletes duplicate data in different rows

 UPDATE all_sessions
SET date = DATE_FORMAT(date, '%Y-%m-%d');
--standardizes date

SELECT *
FROM all_sessions
WHERE productprice <= 10000;
--handles outliers

UPDATE analytics
SET unit_price = REGEXP_REPLACE(unit_price, '[^0-9]', '');
--removing non numeric values from a column

UPDATE all_sessions
SET v2productname = LOWER(v2productname);
--standardize text case


SELECT productprice/1000 AS new_unit_cost
FROM all_sessions


--divides the column
