# Data Science Intern challenge

Question 1: Given some sample data, write a program to answer the following: click here to access the required data set

On Shopify, we have exactly 100 sneaker shops, and each of these shops sells only one model of shoe. We want to do some analysis of the average order value (AOV). When we look at orders data over a 30 day window, we naively calculate an AOV of $3145.13. Given that we know these shops are selling sneakers, a relatively affordable item, something seems wrong with our analysis. 

  a) Think about what could be going wrong with our calculation. Think about a better way to evaluate this data. 
  
  b) What metric would you report for this dataset?
  
  c) What is its value?
  
Answer 1) See jupyter notebook

------------------------------------------


Question 2: For this question you’ll need to use SQL. Follow this link to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

  2a) How many orders were shipped by Speedy Express in total?
  
  //Solution 1
  
  SELECT count(ShipperID)  as [Total Orders Shipped] FROM Orders where ShipperID==1
  
  or 
  
  //Solution 2
  
  SELECT COUNT(o.ShipperID)
  FROM Orders AS o
  WHERE (SELECT ShipperID 
      FROM Shippers AS s
      WHERE s.ShipperName == "Speedy Express") == o.ShipperID;
      
 Answer => 54
    
--------

2b) What is the last name of the employee with the most orders?


What is the last name of the employee with the most orders?

// Solution 1

SELECT e.LastName
FROM Employees AS e
WHERE (SELECT o.EmployeeID
FROM Orders AS o
GROUP BY o.EmployeeID
ORDER BY COUNT(o.EmployeeID) DESC
LIMIT 1) == e.EmployeeID;

Or 

// Solution 2

SELECT e.LastName from Employees As e 
JOIN Orders As o 
ON e.EmployeeID = o.EmployeeID
GROUP BY e.EmployeeID, e.LastName
ORDER BY COUNT(o.EmployeeID) Desc Limit 1

Answer => Peacock
______________________________________

2c) What product was ordered the most by customers in Germany?


SELECT  p.ProductName As [Most Ordered Product] 
FROM OrderDetails as od, Products as p, Orders As o, Customers as c 
WHERE c.Country = "Germany" AND od.ProductID = p.ProductID  AND  od.OrderID = o.OrderID AND c.CustomerID = o.CustomerID
GROUP BY p.ProductID
ORDER BY SUM(od.Quantity) desc
Limit 1

Answer =>  Boston Crab Meat

