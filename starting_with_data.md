Question 1: Find duplicate entries for visitors in table all_sessions.


SQL Queries: SELECT fullvisitorid,
COUNT (fullvisitorid)
FROM all_sessions als
GROUP BY fullvisitorid
HAVING COUNT (fullvisitorid) > 1
ORDER BY COUNT DESC





Question 2: Find the total unique visitors in all_sessions table

SQL Queries:SELECT COUNT (DISTINCT fullvisitorid) as unique_visitors
from all_sessions





Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
