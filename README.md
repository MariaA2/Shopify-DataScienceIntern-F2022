# Shopify-DataScienceIntern-F2022

**Question 1:**

***-Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.*** 

What is going wrong is that all the order_amount is being added and divided by total number of orders. Which is
the average. This is a naive approach since it doesn't account for outliers. Data point of someone ordering alot in bulk is not a true
reflection of the dataset.

***-What metric would you report for this dataset?***

I would report the median for this dataset.

***-What is its value?***

import pandas as pd

info = pd.read_csv('2019 Winter Data Science Intern Challenge Data Set - Sheet1.csv')

#original calculations done for AOV\
ordersadded = info['order_amount'].sum()\
aov = ordersadded/(len(info))\
print(aov.round(2))

3145.13

#calculation to get median\
medianvalue = "{:,.2f}".format(info['order_amount'].median())\
print(medianvalue)

284.00\
#The median for this data set is $284.00


**Question 2:**

***-How many orders were shipped by Speedy Express in total?***

SELECT COUNT(Orders.OrderID) AS OrdersShipped FROM Orders\
INNER JOIN Shippers ON (Orders.ShipperID = Shippers.ShipperID)\
WHERE Shippers.ShipperName = 'Speedy Express'\
GROUP BY Shippers.ShipperName

54

***-What is the last name of the employee with the most orders?***

SELECT Employees.LastName FROM Employees\
INNER JOIN Orders ON (Orders.EmployeeID = Employees.EmployeeID)\
GROUP BY Employees.LastName\
ORDER BY COUNT(Orders.OrderID) DESC LIMIT 1

Peacock

***-What product was ordered the most by customers in Germany?***

SELECT DISTINCT(Products.ProductName) FROM Customers\
INNER JOIN Orders ON (Customers.CustomerID = Orders.CustomerID)\
INNER JOIN OrderDetails ON (OrderDetails.OrderID = Orders.OrderID)\
INNER JOIN Products ON (Products.ProductID = OrderDetails.ProductID)\
WHERE Customers.Country = 'Germany'\
GROUP BY Products.ProductName\
ORDER BY COUNT(Products.ProductID) DESC LIMIT 1

Gorgonzola Telino
