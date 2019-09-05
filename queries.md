# Database Queries

## find all customers that live in London. Returns 6 records.

SELECT City, CustomerName, ContactName
From Customers
WHERE City= 'London'

## find all customers with postal code 1010. Returns 3 customers.

SELECT City, CustomerName, ContactName
From Customers
WHERE PostalCode= '1010'

## find the phone number for the supplier with the id 11. Should be (010) 9984510.

SELECT phone FROM [Suppliers] Where SupplierID='11'

## list orders descending by the order date. The order with date 1997-02-12 should be at the top.

SELECT * FROM [Orders] order by OrderDate desc

## find all suppliers who have names longer than 20 characters. You can use `length(SupplierName)` to get the length of the name. Returns 11 records.

SELECT * 
FROM [Suppliers]
WHERE length(SupplierName) > 20

## find all customers that include the word "market" in the name. Should return 4 records.

SELECT * From Customers
WHERE CustomerName like '%market%'

## add a customer record for _"The Shire"_, the contact name is _"Bilbo Baggins"_ the address is _"1 Hobbit-Hole"_ in _"Bag End"_, postal code _"111"_ and the country is _"Middle Earth"_.

insert into [Customers] (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ('Shire', 'Bilbo Baggins', '1 Hobbit-Hole', 'Bag End', '111', 'Middle Earth')

## update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.

UPDATE [Customers]
SET ContactName = 'Bilbo Baggins'
Where PostalCode = '11122'

## list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 7 orders.

SELECT Customers.CustomerName, COUNT(Orders.CustomerID) AS NumberOfOrder From Orders
LEFT Join Customers ON Orders.CustomerID = Customers.CustomerID
Group By CustomerName

## list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Ernst Handel_ should be at the top with 10 orders followed by _QUICK-Stop_, _Rattlesnake Canyon Grocery_ and _Wartian Herkku_ with 7 orders each.

SELECT Customers.CustomerName, COUNT(Orders.CustomerID) AS NumberOfOrder From Orders
LEFT Join Customers ON Orders.CustomerID = Customers.CustomerID
Group By CustomerName Order by NumberOfOrder desc

## list orders grouped by customer's city showing number of orders per city. Returns 58 Records with _Aachen_ showing 2 orders and _Albuquerque_ showing 7 orders.

SELECT Customers.City, COUNT(Orders.CustomerID) AS NumberOfOrder From Orders
LEFT Join Customers ON Orders.CustomerID = Customers.CustomerID
Group By City Order by NumberOfOrder asc

## delete all users that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.

DELETE FROM Customers WHERE CustomerID not in (select CustomerID from orders)

// SELECT City, CustomerName, ContactName 

// from Customers
// WHERE City= 'Berlin'
//--------------------------
//your can use and / or statements in the where field

// SELECT City, CustomerName, ContactName 

// from Customers
// WHERE Country = "France" and City ="Paris"

//----------------------
//write a query to get the list of products with category id of 2

// SELECT * from products WHERE CategoryID = 2

//-----------------------

// slect by price

//SELECT * FROM Products order by Price

//---------------------
// slect by price in descending order

//SELECT * FROM Products order by Price desc

//-------------------------------------
// write a query to get the list of products that cost more than 50 organized by price desc

// SELECT * 
// FROM Products 
// WHERE Price > 50
// ORDER BY price desc

//-----------------------
//count the rows of orderdetails

// SELECT count(*) from OrderDetails

//---------------------------
// add an alias

// SELECT count(*) as Banana
// From OrderDetails

// SELECT CustomerName as Name, 
// ContactName as Contact, 
// length(CustomerName) as NameLength
// From Customers

//------------------------------------
//get unique records back

// SELECT DISTINCT City
// From Customers


//------------------WildCards
// find the firs tname that starts with a J and follow with an n

// SELECT * From Employees 
// Where FirstName like 'J_n%'

// slected distinct(no dublicats) city that has an ar somewhere in the middle and put in alphabetical order. you can add desc to make order decent after City on last line

// SELECT DISTINCT City
// FROM Customers
// WHERE City like '%ar%'
// ORDER by City

// find emplyess who have notes that inlude sales ordered by last name Ascending
// SELECT * FROM Employees
// WHERE Notes like '%sales%'
// ORDER BY LastName ASC

// select cities that dont have %ar% in their name with the "NOT" operation
// SELECT DISTINCT City
// FROM Customers
// WHERE City NOT like '%ar%'
// Order By City