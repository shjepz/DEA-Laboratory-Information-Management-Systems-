-- All drug types

SELECT DISTINCT drug_type
FROM DATA$
ORDER BY Drug_Type

-- total drug type obtainment 

SELECT DISTINCT drug_type,
COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY Drug_Type
ORDER BY COUNT(drug_type) DESC

-- Total drug obtainments by year

SELECT year, COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY year
ORDER BY Year

-- Total drug type obtainment by year

SELECT year, drug_type, COUNT(drug_type) AS total_drug_type_obtainment
FROM DATA$
GROUP BY year, Drug_Type
ORDER BY Year, Drug_Type

-- running total of drug obtainments by drug type, partitioned by year
WITH cte AS(
SELECT year, drug_type, COUNT(drug_type) AS total_drug_type_obtainment
FROM DATA$
GROUP BY year, Drug_Type
)

SELECT *, 
SUM(total_drug_type_obtainment)
OVER (Partition by drug_type ORDER BY year) AS running_total
FROM cte

-- Total drug obtainment by state, order by highest to lowest 
-- drug obtainment

SELECT state, COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY state
ORDER BY COUNT(drug_type) DESC

-- total drug type obtainment by state

SELECT state, drug_type, COUNT(drug_type) AS total_drug_type_obtainment
FROM DATA$
GROUP BY state, Drug_Type
ORDER BY state, Drug_Type

-- running total drug type obtainment by state

WITH cte AS(
SELECT state, drug_type, COUNT(drug_type) AS total_drug_type_obtainment
FROM DATA$
GROUP BY state, Drug_Type
)

SELECT *,
SUM(total_drug_type_obtainment)
OVER (Partition by state ORDER BY drug_type) AS running_total
FROM cte


-- total drug obtainments per net weight

SELECT net_weight, COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY net_Weight
ORDER BY COUNT(drug_type) DESC

-- Net weight by total drug type obtainments

SELECT drug_type,  net_weight,
COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY net_Weight, Drug_Type
ORDER BY Drug_Type, COUNT(drug_type) DESC

-- total drug obtainments by month 

SELECT CASE
WHEN Month_Number = 1 THEN 'January'
WHEN Month_Number = 2 THEN 'February'
WHEN Month_Number = 3 THEN 'March'
WHEN Month_Number = 4 THEN 'April'
WHEN Month_Number = 5 THEN 'May'		
WHEN Month_Number = 6 THEN 'June'
WHEN Month_Number = 7 THEN 'July'
WHEN Month_Number = 8 THEN 'August'
WHEN Month_Number = 9 THEN 'September'
WHEN Month_Number = 10 THEN 'October'
WHEN Month_Number = 11 THEN 'November'
WHEN Month_Number = 12 THEN 'December'
END AS Month_name, COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY Month_Number
ORDER BY Month_Number

-- total drug obtainments by month order by 
-- highest total obtainment month descending

SELECT CASE
WHEN Month_Number = 1 THEN 'January'
WHEN Month_Number = 2 THEN 'February'
WHEN Month_Number = 3 THEN 'March'
WHEN Month_Number = 4 THEN 'April'
WHEN Month_Number = 5 THEN 'May'		
WHEN Month_Number = 6 THEN 'June'
WHEN Month_Number = 7 THEN 'July'
WHEN Month_Number = 8 THEN 'August'
WHEN Month_Number = 9 THEN 'September'
WHEN Month_Number = 10 THEN 'October'
WHEN Month_Number = 11 THEN 'November'
WHEN Month_Number = 12 THEN 'December'
END AS Month_name,
COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY Month_Number
ORDER BY COUNT(drug_type) DESC

-- total drug type obtainments by month

SELECT CASE
WHEN Month_Number = 1 THEN 'January'
WHEN Month_Number = 2 THEN 'February'
WHEN Month_Number = 3 THEN 'March'
WHEN Month_Number = 4 THEN 'April'
WHEN Month_Number = 5 THEN 'May'		
WHEN Month_Number = 6 THEN 'June'
WHEN Month_Number = 7 THEN 'July'
WHEN Month_Number = 8 THEN 'August'
WHEN Month_Number = 9 THEN 'September'
WHEN Month_Number = 10 THEN 'October'
WHEN Month_Number = 11 THEN 'November'
WHEN Month_Number = 12 THEN 'December'
END AS Month_name, drug_type,
COUNT(drug_type) AS total_drug_obtainments
FROM DATA$
GROUP BY Month_Number, Drug_Type
ORDER BY Month_Number, Drug_Type

-- running total by drug type per net weight obtained in California 2022

WITH cte AS(
SELECT State, Net_Weight, Drug_Type, COUNT(drug_type) AS c_drug_type
FROM DATA$
WHERE year = 2022 AND state = 'CA'
GROUP BY State, Net_Weight, Drug_Type
)

SELECT *,
SUM(c_drug_type) OVER (ORDER BY drug_type) AS r_total
FROM cte

-- running total by drug type per net weight obtained in Texas 2022

WITH cte AS(
SELECT State, Net_Weight, Drug_Type, COUNT(drug_type) AS c_drug_type
FROM DATA$
WHERE year = 2022 AND state = 'TX'
GROUP BY State, Net_Weight, Drug_Type
)

SELECT *,
SUM(c_drug_type) OVER (ORDER BY drug_type) AS r_total
FROM cte

-- 2010 vs 2022 drug obtainments 

SELECT *, 
CASE WHEN table_a.c_drug_type > table_b.c_drug_type THEN '2010'
ELSE '2022' END AS 'winner'
FROM 
(SELECT year, state, COUNT(drug_type) AS c_drug_type
FROM DATA$
WHERE year = 2010
GROUP BY year, state
) AS table_a
JOIN 
(SELECT year, state, COUNT(drug_type) AS c_drug_type
FROM DATA$
WHERE year = 2022
GROUP BY year, state
) AS table_b
ON table_a.state = table_b.state
ORDER BY table_a.c_drug_type DESC
