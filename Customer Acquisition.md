# SQL-Project
Customer Behavior Analysis- SQL 

-Customer acquisition it refers to the stage when the customers learn more about the company's offerings from visits to the website, or by testing products in a store.

//We'll discuss the following reports:
The number of registrations in the given period.
The number of registrations in the current period of time (current week, current month, etc.).
The number of registrations over time, tallying registrations in each month or in each week.

#To count the number of registrations in 2016 -
SELECT COUNT(customer_id) AS registration_count_2016
FROM customers
WHERE registration_date >= '2016-01-01'
  AND registration_date <  '2017-01-01';
  
#customers registered in the first six months of 2017
SELECT COUNT(customer_id) AS registration_count_2017
FROM customers
WHERE registration_date >= '2017-01-01'
  AND registration_date <=  '2017-06-30';
  
  
#To count the number of registrations in 2020-
SELECT COUNT(customer_id) AS registration_count_2020
FROM customers
WHERE registration_date >= '2020-01-01'
AND registration_date < '2020-01-01'::DATE + INTERVAL '1' YEAR;

//calculate the beginning of the current period which helps to find registration counts for the current year, month, quarter, etc.

#show the beginning of the current year.
SELECT
  CAST(
    EXTRACT(year FROM current_timestamp)
    || '-01'
    || '-01'
    AS DATE
  ) AS current_year_start_extract,
  CAST(
    DATE_PART('year', current_timestamp)
    || '-01'
    || '-01'
    AS DATE
  ) AS current_year_start_date_part;

#No.of Registrations in the Current Week
SELECT count(customer_id) AS Customer_count
FROM CUSTOMERS
where registration_date = DATE_TRUNC('week', CURRENT_DATE);

//We now want to find out how customer acquisition has changed over time.
This will help us understand if we're currently attracting more users (or not).

#compare the registration count values for various periods (year to year, month to month, etc.).
SELECT
  DATE_PART('year', registration_date) AS registration_year,
  COUNT(customer_id) AS registration_count
FROM customers
GROUP BY DATE_PART('year', registration_date)
ORDER BY DATE_PART('year', registration_date);

#Registration Count for each quarter for each year
SELECT
  DATE_PART('year', registration_date) AS registration_year,
  DATE_PART('quarter', registration_date) AS registration_quarter,
  COUNT(customer_id) AS registration_count
FROM customers
GROUP BY DATE_PART('year', registration_date) ,DATE_PART('quarter', registration_date)
ORDER BY DATE_PART('year', registration_date) ,DATE_PART('quarter', registration_date);

#Registration Count for each month for each year
SELECT
  DATE_PART('year', registration_date) AS registration_year,
  DATE_PART('month', registration_date) AS registration_month,
  COUNT(customer_id) AS registration_count
FROM customers
GROUP BY DATE_PART('year', registration_date) ,DATE_PART('month', registration_date)
ORDER BY DATE_PART('year', registration_date) ,DATE_PART('month', registration_date);


#displaying week label  where week = 35
-This query will show the year and week number, and the earliest date in this week.
SELECT
  DATE_PART('year', registration_date) AS registration_year,
  DATE_PART('week', registration_date) AS registration_week,
  MIN(registration_date) AS week_label,
  COUNT(customer_id) AS registration_count
FROM customers
where DATE_PART('week', registration_date)  = 35
GROUP BY DATE_PART('year', registration_date) ,DATE_PART('week', registration_date)
ORDER BY DATE_PART('year', registration_date) ,DATE_PART('week', registration_date)
;


--End of Introduction













