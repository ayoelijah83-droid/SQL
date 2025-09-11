Categories of Questions Part - 1
Basic SQL - SOLUTION
•	Questions related to basic SQL commands such as SELECT, INSERT, UPDATE, and DELETE.
•	Queries related to basic data manipulation and retrieval from simple tables.
Query Questions:
1.	How do you display all columns and rows from the customers table?
SELECT *
FROM     customers
2.	Write a query to retrieve only the customerName and phone from the customers table?
SELECT customerName, phone
FROM     customers
3.	How do you list all rows where country is 'USA' in the customers table?
SELECT *
FROM     customers
WHERE  (country = 'USA')

4.	Write a query to find all products in the products table with a buyPrice less than 50?
SELECT productName, productCode,buyPrice
FROM     products
WHERE  (buyPrice < 50)
5.	How do you fetch all orders with a status of 'Shipped' from the orders table?
SELECT orderNumber, status
FROM     orders
WHERE  (status = 'Shipped')
6.	Write a query to display the productName and quantityInStock for all products in the products table?
SELECT productName, quantityInStock
FROM     products
7.	How do you find the distinct country values in the customers table?
SELECT DISTINCT country
FROM     customers
8.	Write a query to count the total number of customers in the customers table?
SELECT COUNT(*) AS Total_Customer
FROM     customers
9.	How do you retrieve all employees whose jobTitle is 'Sales Rep'?
SELECT employeeNumber, lastName, firstName, jobTitle
FROM     employees
WHERE  (jobTitle = 'Sales Rep')
10.	Write a query to sort the products table by productName in ascending order?
SELECT *
FROM     products
ORDER BY productName
11.	How do you fetch the customerName and city of all customers located in 'Paris'?
SELECT customerName, city
FROM     customers
WHERE  (city = 'Paris')
12.	Write a query to display the top 10 orders from the orders table based on the orderDate?
SELECT Top 10 orderNumber, orderDate
FROM     orders
ORDER BY orderDate DESC
13.	How do you retrieve all offices located in the USA?
SELECT  *
FROM     offices
WHERE  (country = 'USA')
14.	Write a query to display all employees who work in the office located in 'San Francisco'?
SELECT employees.employeeNumber, offices.city
FROM     employees INNER JOIN
      offices ON employees.officeCode = offices.officeCode
WHERE  (offices.city = 'San Francisco')
15.	How do you calculate the total number of orders placed in the orders table?
SELECT COUNT(orderNumber) AS Expr1
FROM     orders
16.	Write a query to display the productName of all products in the products table where productLine is 'Classic Cars'?
SELECT productName, productLine
FROM     products
WHERE  (productLine = 'Classic Cars')
17.	How do you find the customerName of all customers whose creditLimit is greater than 50,000?
SELECT customerName, creditLimit
FROM     customers
WHERE  (creditLimit > 50000)
18.	Write a query to fetch all products that have a quantityInStock between 10 and 100?
SELECT productCode, productName, quantityInStock
FROM     products
WHERE  (quantityInStock BETWEEN 10 AND 100)
19.	How do you retrieve all orders placed in the year 2003?
SELECT orderNumber, orderDate
FROM orders
WHERE orderDate >= '2003-01-01' 
  AND orderDate < '2004-01-01';
20.	Write a query to display the employeeNumber and firstName of employees whose last names start with 'B'?
SELECT employeeNumber, firstName
FROM     employees
WHERE  (lastName LIKE 'B%')


L1: Intermediate SQL - SOLUTION
•	Queries that involve working with multiple tables, using JOIN, GROUP BY, HAVING, and complex WHERE conditions.
•	Introduction to subqueries, aggregate functions, and case statements.
Questions:
1.	Write a query to retrieve the customerName and city for customers in 'USA' and 'France'?
SELECT customerName, city
FROM     customers
WHERE  (country = 'USA') OR
                  (country = 'France')
2.	How do you fetch the employeeNumber, lastName, and officeCode of all employees who work in the 'San Francisco' office?
SELECT employees.employeeNumber, employees.lastName, offices.officeCode
FROM     employees INNER JOIN
                  offices ON employees.officeCode = offices.officeCode
WHERE  (offices.city = 'San Francisco')
3.	Write a query to find the total number of orders for each customer using orders and customers tables?
SELECT customers.customerNumber, COUNT(orders.orderNumber) AS Expr1
FROM     customers INNER JOIN
                  orders ON customers.customerNumber = orders.customerNumber
GROUP BY customers.customerNumber
4.	How do you retrieve the productName, quantityInStock, and buyPrice for products that have been ordered more than 10 times?
SELECT p.productName, p.quantityInStock, p.buyPrice, SUM(od.quantityOrdered) AS totalOrdered
FROM products p
INNER JOIN orderdetails od ON p.productCode = od.productCode
GROUP BY p.productName, p.quantityInStock, p.buyPrice
HAVING SUM(od.quantityOrdered) > 10;

5.	Write a query to fetch the orderNumber, status, and customerName for orders placed by a customer whose customerNumber is 103?
SELECT orders.orderNumber, orders.status, customers.customerName, customers.customerNumber
FROM     customers INNER JOIN
                  orders ON customers.customerNumber = orders.customerNumber
WHERE  (customers.customerNumber = 103)
6.	Write a query to find the total sales value (quantityOrdered * priceEach) for each order in the orderdetails table.
SELECT quantityOrdered, priceEach, quantityOrdered * priceEach AS [Total Sales Value]
FROM     orderdetails
GROUPBY OrderNumber
7.	How do you find the average quantityOrdered for each orderNumber in the orderdetails table?
SELECT orderNumber, AVG(quantityOrdered) AS Expr1
FROM     orderdetails
GROUP BY orderNumber
8.	Write a query to list the productLine with the highest total revenue (quantityOrdered * priceEach) in the orderdetails table?
SELECT Top 1 productCode, SUM(quantityOrdered * priceEach) AS [Highest Total Revenue]
FROM     orderdetails
GROUP BY productCode
ORDER BY [Highest Total Revenue] DESC

9.	Write a query to display the employeeNumber, firstName, lastName, and the office code where the employee works by joining the employees and offices tables?
SELECT employees.employeeNumber, employees.firstName, employees.lastName, offices.officeCode
FROM     employees INNER JOIN
                  offices ON employees.officeCode = offices.officeCode
10.	How do you find the customers who have never placed an order?
SELECT customers.customerName, orders.orderNumber
FROM     customers LEFT OUTER JOIN
                  orders ON customers.customerNumber = orders.customerNumber
WHERE orders.orderNumber IS NULL
11.	Write a query to retrieve the customerName and the total number of orders placed by each customer (include customers who haven’t placed any orders)?
SELECT customers.customerName, COUNT(orders.orderNumber) AS Expr1
FROM     customers LEFT JOIN
                  orders ON customers.customerNumber = orders.customerNumber
GROUP BY customers.customerName
12.	Write a query to find the productName and quantityOrdered for all orders where the quantity of the product ordered is greater than 50?
SELECT products.productName, orderdetails.quantityOrdered
FROM     products INNER JOIN
                  orderdetails ON products.productCode = orderdetails.productCode
WHERE  (orderdetails.quantityOrdered > 50)
13.	Retrieve the employeeNumber, firstName, and orderNumber of employees who are assigned as sales representatives to customers that have placed an order?
SELECT employees.employeeNumber, employees.firstName, orders.orderNumber
FROM     orders INNER JOIN
                  customers ON orders.customerNumber = customers.customerNumber INNER JOIN
                  employees ON customers.salesRepEmployeeNumber = employees.employeeNumber
14.	Write a query to calculate the average price of products in the products table based on buyPrice?
SELECT productName, AVG(buyPrice) AS Average_Price
FROM     products
GROUP BY productLine
15.	How do you fetch the top 3 most expensive products in the products table?
SELECT TOP (3) productName, buyPrice
FROM     products
ORDER BY buyPrice DESC
16.	Write a query to retrieve the customerName, orderNumber, and orderDate of all orders that have a status of 'Shipped'?
SELECT customers.customerName, orders.orderNumber, orders.orderDate
FROM     orders INNER JOIN
                  customers ON orders.customerNumber = customers.customerNumber
WHERE  (orders.status = 'Shipped')
17.	How do you display the total number of products sold for each productLine?
SELECT products.productLine, Sum(orderdetails.quantityOrdered) AS [Total Number of Product Sold]
FROM     products INNER JOIN
                  orderdetails ON products.productCode = orderdetails.productCode
GROUP BY products.productLine
18.	Write a query to find employees who report directly to the employee with employeeNumber = 1143.?
SELECT 
    e.employeeNumber,
    e.lastName AS EmployeeLastName,
    e.firstName AS EmployeeFirstName,
    m.lastName AS ManagerLastName,
    m.firstName AS ManagerFirstName
FROM employees e
INNER JOIN employees m 
    ON e.reportsTo = m.employeeNumber
WHERE e.employeeNumber = 1143;

19.	Write a query to calculate the total number of orders in the orders table, grouped by status.?
SELECT status, COUNT(*) AS Expr1
FROM     orders
GROUP BY status
20.	List employees with their manager’s name.?
SELECT 
    e.employeeNumber,
    e.lastName AS EmployeeLastName,
    e.firstName AS EmployeeFirstName,
    m.lastName AS ManagerLastName,
    m.firstName AS ManagerFirstName
FROM employees e
LEFT JOIN employees m 
    ON e.reportsTo = m.employeeNumber
