What are your risk areas? Identify and describe them.
Remove Unwanted or Irrelavent Observations
Ensure Accurate Datatypes
Address Missing Values
Fixing Typos


QA Process: In the Excel files we start cleaning our data as follows
-- Using the trim function helps us remove leading and trailing spaces in cells having text value. eg [=TRIM(cellnumber)],[=TRIM(a2,c45)]
-- To separate messy data having different types of information combined we use Text to columns option in Excel.
-- Using filter on columns having blank cells and running operations on them.
-- Using clean function can get rid of non printable characters such as a line break.
-- Using left,right and mid functions to trim certain parts of a text getting rid of redundant information of parts in a cell.
-- Using upper, lower and proper function to convert text values to desired case.
-- In the home page click find and select, click on go to special or just select the cells to be updated and press f5. It has an option to go to empty cells and fill in values like 0 or just for data exploration.

Describe your QA process and include the SQL queries used to execute it.

#SELECT COUNT((DISTINCT(city))
FROM all_sessions_view


-- It gives unique values in city column in the all_sessions table (all_sessions_view is a view created with relevant columns)



SELECT * FROM all_sessions_view
WHERE city LIKE 'not available in demo dataset'


-- It gives all the visitors in the view all_sessions_view with having city specified as 'not available in demo dataset'


SELECT column_name, data_type, is_nullable
FROM information_schema.columns
WHERE table_name = 'all_sessions';


--Get column data types and nullability for the employees table



SELECT fullvisitorid, COUNT(*)
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1;


--checking for duplicate data in all_sessions table for fullvisitorid column



UPDATE all_sessions_view
SET country = CASE
    WHEN country IN ('USA', 'United States') THEN 'United States'
    WHEN country = 'UK' THEN 'United Kingdom'
    ELSE country
    END;



--standardizing the country names in view all_sessions_view.



