---
output:
  pdf_document: default
  html_document: default
---
Question 2

a. How many orders were shipped by Speedy Express in total?

CREATE VIEW Shipper_Orders AS
SELECT Orders.OrderID, Orders.ShipperID, Shippers.ShipperName
FROM Orders 
JOIN Shippers
ON Shippers.ShipperID=Orders.ShipperID;
SELECT COUNT(*) FROM [Shipper_Orders]
WHERE ShipperName = 'Speedy Express';

54 orders were shipped by Speedy Express in total. I joined the Shippers and Orders tables on the variable of ShipperID and used COUNT to identify the number of orders from Speedy Express. 

b. What is the last name of the employee with the most orders?

CREATE VIEW Employee_Orders AS 
SELECT Orders.EmployeeID, Employees.LastName, Orders.OrderID
FROM Orders
JOIN Employees
ON Employees.EmployeeID=Orders.EmployeeID; 

SELECT LastName, COUNT(*)
FROM Employee_Orders
GROUP BY LastName
ORDER BY COUNT(*) desc;

The last name of the employee with the most orders is Peacock (40 orders). 

c. What product was ordered the most by customers in Germany?

SELECT ProductName
FROM Products
LEFT JOIN OrderDetails
ON Products.ProductID = OrderDetails.ProductID 
LEFT JOIN Orders
ON OrderDetails.OrderID = Orders.OrderID
LEFT JOIN Customers
ON Orders.CustomerID = Customers.CustomerID
WHERE Country = 'Germany'
GROUP BY OrderDetails.ProductID
ORDER BY total_quantity DESC
LIMIT 1;

Boston Crab Meat was ordered the most by customers in Germany (160 orders). 
