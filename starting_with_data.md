Question 1: Find duplicate entries for visitors in table all_sessions.




SELECT fullvisitorid,
COUNT (fullvisitorid)
FROM all_sessions als
GROUP BY fullvisitorid
HAVING COUNT (fullvisitorid) > 1
ORDER BY COUNT DESC





Question 2: Find the total unique visitors in all_sessions table


SELECT COUNT (DISTINCT fullvisitorid) as unique_visitors
from all_sessions





Question 3: Find the total number of unique visitors by referring sites


SELECT COUNT (DISTINCT(fullvisitorid)) as unique_visitor
FROM all_sessions
WHERE pagetitle LIKE '%Office%';


-- We can traverse the dataset with changing the keyowrd that we want to look for and the column we want to traverse in.




Question 4: Find each unique product viewed by each visitor 


SELECT DISTINCT (fullvisitorid) AS unique_visitor, 
	(SELECT DISTINCT (v2productname)) AS unique_prod
FROM all_sessions als
GROUP BY als.v2productname,als.fullvisitorid 






Question 5: Compute the percentage of visitors to the site that actually makes a purchase

SQL Queries:
SELECT fullvisitorid, COUNT (fullvisitorid) AS fullvisitorid_count,
COUNT(*) * 100.0/ SUM(COUNT(*)) OVER () AS fullvisitorid_percent
FROM all_sessions als
	WHERE als.productprice > 0
GROUP BY fullvisitorid
ORDER BY fullvisitorid ASC


