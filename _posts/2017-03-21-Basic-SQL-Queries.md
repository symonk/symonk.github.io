---
layout: post
title: Basic SQL Queries all QA engineers should know
subtitle: SQL Server - by Simon Kerr
bigimg: /img/path.jpg
published: true
---

This post is a short article outlining some simple uses of the SQL Queries.  SQL In short stands for Structured Query Language.  For the purpose of this blog post, I will be discussing Microsoft SQL Server and SQL Server Management Studio.


- Microsoft SQL Server - This is our actual instance which houses our database(s) and corresponding data (and various other things, but for the purpose of this post, those are out of scope)

- SQL Server Management Studio - This is an application we can use to connect to our database instance to manage the database(s), data, stored procedures and users etc (again, various other things are available using this, but for the purpose of this post, those are out of scope).  We use this studio user interface as a means to write SQL queries to communicate with our database(s).

In order to execute queries we need to connect to our database instance using SSMS (SQL Server Management Studio).  We can Launch the application and depending on how the instance was setup initially, connect via windows authentication or SQL Server Authentication, providing a Login/Password.  note: Default super admin username will be "sa" - Tho it is highly advised to disable this account for security/permissions reasons, some ISO compliance and other certification actually requires it.


## View all records in a particular database table

	Select * FROM Employees (Lists all columns with every record in Employees)
    
## View certain columns from a particular database table

	Select EmployeeID, Employee FirstName FROM Employees (Lists all records in
	the Employees table, however results will only return the EmployeeID and 
	FirstName columns




