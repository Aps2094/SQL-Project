# SQL-Project
Customer Behavior Analysis- SQL 

-Customer acquisition it refers to the stage when the customers learn more about the company's offerings from visits to the website, or by testing products in a store.

We'll discuss the following reports:
The number of registrations in the given period.
The number of registrations in the current period of time (current week, current month, etc.).
The number of registrations over time, tallying registrations in each month or in each week.

#To count the number of registrations in 2016 -
SELECT COUNT(customer_id) AS registration_count_2016
FROM customers
WHERE registration_date >= '2016-01-01'
  AND registration_date <  '2017-01-01';
  
#customers registered in the first six months of 2017


