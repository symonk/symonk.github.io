---
layout: post
title: 'Basic SQL Querying and functions'
subtitle: SQL Data Definition/Manipulation Language
bigimg: /img/path.jpg
published: true
---

This post is a short article outlining some simple uses of the SQL Queries.  SQL In short stands for Structured Query Language.  For the purpose of this blog post, I will be discussing Microsoft SQL Server and SQL Server Management Studio.


- Microsoft SQL Server - This is our actual instance which houses our database(s) and corresponding data (and various other things, but for the purpose of this post, those are out of scope)

- SQL Server Management Studio - This is an application we can use to connect to our database instance to manage the database(s), data, stored procedures and users etc (again, various other things are available using this, but for the purpose of this post, those are out of scope).  We use this studio user interface as a means to write SQL queries to communicate with our database(s).

In order to execute queries we need to connect to our database instance using SSMS (SQL Server Management Studio).  We can Launch the application and depending on how the instance was setup initially, connect via windows authentication or SQL Server Authentication, providing a Login/Password.  note: Default super admin username will be "sa" - Tho it is highly advised to disable this account for security/permissions reasons, some ISO compliance and other certification actually requires it.


### View all records in a particular database table
List all columns with every record in Employees:

    Select * FROM Employees
    
---
    
### View certain columns from a particular database table
Lists all records in the Employees table, however results will only return the EmployeeID and FirstName columns:

	Select EmployeeID, Employee FirstName FROM Employees 
    
---
    
### Utilising the WHERE clause to filter out unwanted data
Lists every record from the Employees table (displaying their EmployeeID and FirstName column data only, However - Only records where the Firstname is "Simon" will be displayed to the user:

	Select EmployeeID, Employee FirstName FROM Employees WHERE FirstName = 
	'Simon' 
    
---
    
### WHERE clause opposition - where something is not
Lists every record from the Employees table (displaying their EmployeeID and FirstName column data only, However - Only records where the Firstname is not "Simon" will be displayed to the user:

	Select EmployeeID, Employee FirstName FROM Employees WHERE FirstName <> 
	'Simon' 
    
---
    
### BEFORE or AFTER a particular Date
Lists all employees who where hired After this particular date.  We can also use WHERE HireDate <= '1-June-2016' to get employees who were hired Before this particular date.  Pay attention to the select columns, we will only be getting back EmployeeID and FirstName columns (comma seperated):

	SELECT EmployeeID, FirstName FROM Employees WHERE HireDate >= '1-June-2016'

    
### Multiple WHERE clauses using the AND operator, BETWEEN operator too!
As you can imagine, we will return every employee who was hired between these two dates, displaying only their ID and First name columns.  However this can be rewritten using a fancier BETWEEN operator.  WHERE HireDate BETWEEN '1-JULY-2016' AND '10-July-2016'

	SELECT EmployeeID, FirstName FROM Employees WHERE (HireDate >= '1-July-2016')
    AND (HireDate <= '10-July-2016') 
    
### Multiple Choice WHERE clause : IN and OR operators
Previous examples are ok for short examples, however what if we need to find employees of certain ages? 18, 25, 31 ?  Here we utilise the IN operator, we can however use the OR operator in a two case scenario.
    
    SELECT * FROM Employees WHERE Age = 18 OR 20  -> OR Operator
    SELECT * FROM Employees WHERE Age IN (18, 25, 31) -> IN Operator
    
### Reversing the IN Operator to find results NOT IN
We can also use the NOT IN to reverse the IN operator, similar to how we reversed = with <> previously.  Here is an example of all employees who's age is NOT 18, 25, 31 or 40
    
    SELECT * FROM Employees WHERE Age NOT IN (18,25,31,40) -> NOT IN Operator
    
### The Powerful LIKE operator and its magnitude of uses

 The LIKE operator uses pattern matching with wildcard chararcters.  these wildcards are listed below:

      _ (underscore) : matches any single character
      % : matches a string of one or more characters
      [] : matches any single character within the specified range (e.g. [d-g]
      [^] : matches any single character not within a specified range (e.g [d-g]

      Doesn't make much sense yet I would imagine, lets look at some examples then.

      WHERE FirstName LIKE '_im' -> All 3 letter firstnames that end in "im" - Tim
      WHERE FirstName LIKE '%mon' -> All firstnames that end with mon -> simon
      WHERE FirstName LIKE '%mon%' -> All firstnames that contain mon -> Monty
      WHERE FirstName LIKE '[JT]im' -> All 3 letter firstnames that end in "im" but
      also begin with J or T -> e.g Tim & Jim, Dim/Nim/Bim would not be returned
      WHERE FirstName LIKE 'm[^c]%' -> All firstnames beginning with M and the 2nd
      letter is not c -> excluding all Mcc names e.g McCutchin

NOT IN can also be used with these operator/wildcards and we can also apply
multiple of them into the WHERE clause, see below:

    SELECT * FROM Employee WHERE (FirstName NOT LIKE '%mon%') AND (Surname NOT 
    LIKE '%Ker'
    
### Get some ORDER in your results

Order Ascending -> 

	SELECT * FROM Employees WHERE Firstname <> 'Simon'ORDER BY FirstName ASC
	
Above we simply find ALL employees whos firstname IS NOT Simon and order the results by Firstname Ascending
    
    SELECT * FROM Employees WHERE Firstname <> 'Simon'ORDER BY FirstName DESC
	
Above we simply find ALL employees whos firstname IS NOT Simon and order the results by Firstname Descending
    
### Counting how many records exist in the table

	SELECT COUNT(*) FROM Employee (Returns a numerical value for every record in
	the table
    
### INSERT new rows into the table

	INSERT INTO Employees (Firstname, Surname, Role) VALUES ('Simon', 'Kerr', 
	'QA Engineer')
	
### UPDATE and SET Data (Used to update existing records)
Update a record with EmployeeID of 250 and set the First and Surname.

NOTE: If you forget to include the WHERE clause here you will update EVERY 
record in the table, its always advised to take backups when tinkering with
the data outside of READ ONLY scenarios.

	UPDATE EMPLOYEES SET FirstName = 'Simon', Surname = 'Kerr' WHERE EmployeeID
    = 250 
    
### DELETE records from the table
Delete all employees with an employeeID of 250 (single typically)

	DELETE FROM EMPLOYEES WHERE EmployeeID = 250 
    
Delete all employees where the country is Northern Ireland (multiple)

    DELETE FROM EMPLOYEES WHERE Country = 'Northern Ireland'
    
Delete every record, tread carefully!

    DELETE * FROM Employees 
    
### Selecting a number of records
Return the top 1000 records showing only EmployeeID only
 
    SELECT TOP 1000 EmployeeID FROM Employee
   
Return the top 5% records showing EmployeeID and FirstName
    
    SELECT TOP 5 PERCENT EmployeeID, FirstName FROM Employee

    
### Min() and Maximum() Functions
Find the cheapest product in the Items table
    
    SELECT MIN(Price) AS smallestPrice FROM Items
   
Find the dearest product in the Products table

    SELECT MAX(Price) AS smallestPrice FROM Products
