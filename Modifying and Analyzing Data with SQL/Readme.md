# Modifying and Analyzing Data with SQL

All of the questions in this quiz refer to the open source Chinook Database. 
Please familiarize yourself with the ER diagram below in order to familiarize yourself with the table and column names in order to write accurate queries and get the appropriate answers.
<p align = "center">
<img src= "https://user-images.githubusercontent.com/94797745/147788917-b2a638a4-47a3-4f44-89da-772ab892b5f0.png" width = "500" height = "400">
  
## 🧙‍♂️ Coding Questions & 🚀 Solutions
### 1. Pull a list of customer ids with the customer’s full name, and address, along with combining their city and country together. Be sure to make a space in between these two and make it UPPER CASE. (e.g. LOS ANGELES USA)
  
                SELECT CustomerId
                  ,(Customers.FirstName || " " || Customers.LastName) AS CustomerFullName
                  ,(Customers.Address || ", " || UPPER(Customers.City) || " " || UPPER(Customers.Country)) AS CustomerAddress
                FROM Customers
 
### 2. Create a new employee user id by combining the first 4 letters of the employee’s first name with the first 2 letters of the employee’s last name. Make the new field lower case and pull each individual step to show your work.
  
                SELECT LOWER(SUBSTR(Customers.FirstName, 1, 4) || SUBSTR(Customers.Lastname, 1, 2)) AS NewID
                FROM Customers
  
 ### 3. Show a list of employees who have worked for the company for 15 or more years using the current date function. Sort by lastname ascending.

                SELECT FirstName
                ,LastName
                ,HireDate
                ,(STRFTIME('%Y', 'now') - STRFTIME('%Y', HireDate)) - (STRFTIME('%m-%d', 'now') < STRFTIME('%m-%d', HireDate)) AS YearsWorked
              FROM Employees
              WHERE YearsWorked >= 15
              ORDER BY LastName ASC
  
### 4.   Profiling the Customers table, answer the following question. Are there any columns with null values?

              SELECT *
              FROM Customers
              WHERE Fax IS NULL;

### 5. Find the cities with the most customers and rank in descending order.

                SELECT City
                  ,Count(DISTINCT (CustomerID)) AS NumofCustomers
                FROM Customers
                GROUP BY City
                ORDER BY NumofCustomers DESC LIMIT 7  
  
### 6. Create a new customer invoice id by combining a customer’s invoice id with their first and last name while ordering your query in the following order: firstname, lastname, and invoiceID.

              SELECT Customers.FirstName
                ,Customers.LastName
                ,(Customers.FirstName || Customers.LastName || Invoices.InvoiceId) AS NewInvoiceId
              FROM Customers
              JOIN Invoices ON Customers.CustomerId = Invoices.CustomerId
              WHERE NewInvoiceId LIKE "AstridGruber%"
              ORDER BY FirstName
                ,LastName
                ,InvoiceId;
  
 
