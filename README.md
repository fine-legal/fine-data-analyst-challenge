# Fine Data Analyst Challenge @ fine.

## SQL

### Queries

__Scenario:__
You have been given access to a sample e-commerce database. The database contains several tables including Customers, Orders, OrderDetails, Products, and Categories. The relationships between tables are as follows:

- __Customers__ have a one-to-many relationship with Orders.
- __Orders__ have a one-to-many relationship with OrderDetails.
- __Products__ have a one-to-many relationship with OrderDetails.
- __Products__ have a many-to-one relationship with Categories.
Each table's relevant columns are outlined below:

- __Customers:__ CustomerID, FirstName, LastName, Email, Phone
- __Orders:__ OrderID, CustomerID, OrderDate, ShipDate
- __OrderDetails:__ OrderDetailID, OrderID, ProductID, UnitPrice, Quantity
- __Products:__ ProductID, ProductName, CategoryID, UnitPrice, UnitsInStock
- __Categories:__ CategoryID, CategoryName

__Task:__
Write SQL queries to retrieve the following information:

List of Customers and Their Orders:
Generate a list of all customers along with their respective order IDs and order dates. Sort this list by the order date in descending order.

Sales Summary by Category:
Provide a summary of total sales (calculated as UnitPrice * Quantity) grouped by CategoryName for the last year. Display CategoryName and the total sales, and order the results by total sales in descending order.

Product Backorder Report:
Create a report of products that are on backorder (i.e., UnitsInStock is 0). Include ProductName, CategoryName, and UnitsInStock. Order the report alphabetically by ProductName.

Customer Purchases with Subtotals:
For a given customer (use a parameterized customer ID), show all the products they have purchased, including the product name, unit price, quantity, and subtotal for each product (calculated as UnitPrice * Quantity). Include the order date and sort the result by it in ascending order.

High-Value Orders:
Identify orders where the total amount (sum of UnitPrice * Quantity in OrderDetails) exceeds a certain threshold (e.g., $500). List the OrderID, OrderDate, and the total amount, and order the results by the total amount in descending order.

Guidelines:
- Assume you have read-only access to the database and can execute SELECT statements.
- Please use aliases, aggregate functions, JOINs, subqueries, and/or CTEs where necessary.
- Query readability and efficiency is important.

Deliverables:
The student should provide a SQL script file containing the queries, with comments describing what each query does.
This task is designed to test various levels of SQL knowledge, including joining multiple tables, aggregating data, sorting results, and applying filters. It also checks the student's ability to think about data from a business perspective, such as identifying sales trends or inventory issues.

### SQL Performance Tuning

__Scenario:__
The database of an e-commerce platform is experiencing slow performance with the following SQL query, which is intended to generate a report of monthly sales for each product within the last year:

```sql
SELECT p.ProductName, 
       EXTRACT(YEAR FROM o.OrderDate) AS SaleYear,
       EXTRACT(MONTH FROM o.OrderDate) AS SaleMonth,
       SUM(od.Quantity * od.UnitPrice) AS TotalSales
FROM Products p
JOIN OrderDetails od ON p.ProductID = od.ProductID
JOIN Orders o ON od.OrderID = o.OrderID
WHERE o.OrderDate >= DATEADD(year, -1, GETDATE())
GROUP BY p.ProductName, 
         EXTRACT(YEAR FROM o.OrderDate),
         EXTRACT(MONTH FROM o.OrderDate)
ORDER BY p.ProductName, 
         SaleYear, 
         SaleMonth;
```
This query runs particularly slowly, and your task is to optimize it.

__Assumptions:__
There are large numbers of records in the Orders, OrderDetails, and Products tables.
Indexes may or may not exist; you can suggest creating new indexes as part of your solution.

__Task:__
Analyze and rewrite the query to improve its performance with a justification for each change you make.

__Deliverables:__

- The optimized query.
- An explanation of the changes made to the original query.
- Any recommendations for further database or query optimizations such as indexing strategies.

## Excel 
Following you will find a list with excel tasks. Please explain how you would approach them and try to solove them with the used formulas. An Excel could be helpful to show case how you did it.

### A 
Please imagine you have a column with dates with the following format "Dec/1/23 16:11" and you should format this to a list of dates with the following format: yyyy-mm-dd
