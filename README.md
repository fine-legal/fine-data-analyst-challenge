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

- Provide a SQL script file containing the queries, with comments describing what each query does.

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

## DBT

### DBT project design

__Scenario:__

Imagine you are tasked with setting up a new dbt project to transform raw sales data into a format that is useful for analysis. The raw data is loaded into raw data lake every night and needs to be transformed into a star schema for the analytics team.

__Raw Data Tables:__

- __raw_sales:__ Contains raw sales data with fields such as sale_id, product_id, customer_id, sale_amount, sale_date.
- __raw_products:__ Contains product information with fields like product_id, product_name, category_id.
- __raw_customers:__ Contains customer information with fields such as customer_id, first_name, last_name, email.
- __raw_categories:__ Contains category data with fields category_id, category_name.

__Task:__
Please think about useful transformations. 
You are not required to write any code nor to set up an evironment.

__Model Planning:__
Describe the models you would create for the transformation process, including names and a brief description of their purpose.
Outline the transformations you would apply to the raw data to convert it into a star schema format.

__Testing Strategy:__
Explain how you would ensure the integrity of the transformed data. 
Include examples of tests you think make sense for the models, such as uniqueness, referential integrity, and not-null tests.

### Calculating Average Order Status Duration

__Scenario:__
You have a stg_orders table in your data warehouse that gets updated every 4 hours with new order data. Your task is to track changes to the status column of this table and calculate the average time an order spends in each status.

__stg_orders Table Structure:__

__order_id__ (unique identifier for each order)
__status__ (current status of the order, e.g., 'pending', 'shipped', 'delivered', 'canceled')
__updated_at__ (timestamp of the last update to the order)

__Deliverables:__
- SQL query to do the calculation

## Google Sheet
Please provide a google sheet witht he solution and a description what you did and your thoughts while doing it. 

### Date formatting
Please imagine you have a column with dates with the following format "Dec/1/23 16:11" and *Google Sheet is not recognising it as a date*. Now you should format this to a list of dates with the following format: yyyy-mm-dd

Don't use the on boarding formatting capabilities of Google Sheets.

### Amount formatting
You have a list of amounts formatted in the following way 'EUR200,000.12'. Please reformat the amounts so they can be used to takes sums etc. 

### Additional data
The ECB is offering lists of exchange rates per day. Find this data and download it.

Set up a list of dummy data with an amount and a date formatted as shown above.
Add a column with the exchange rate per day and calculate the Euro amount assuming all amounts are in USD.

## Additional task: Text to CSV
Imagine you have the following textfile and you have the task to create a table from it. How do you do it, what do you use?

The table should have the columns like the first row in the file:
- UserID
- DataType
- TransactionID
- TransactionIDKey
- TransactionTenantID
- Time
- TransactionTypeName
- SessionDurationMins
- IP
- DeviceType
- ID
- GameType
- GameName
- GameVendorName
- TransactionName
- PaymentProvider
  
Please request the text file with me if you want to take on the challenge.


