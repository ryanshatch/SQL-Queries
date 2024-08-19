<!DOCTYPE html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
  <h1>SQL Queries</h1>
  <h2>Table of Contents:</h2>
  <ul>
    <li>
      <a href="#sequel">Sequel</a>
    </li>
    <li>
      <a href="#projects">Projects</a>
    </li>
  </ul>
  <h2>Sequel:</h2>
  <p>SQL (Structured Query Language) is a powerful tool for working with structured data in relational databases. <br>This repository serves as a hub for SQL projects that cover a wide range of data analysis scenarios, from sales analysis to customer segmentation and more. </p>
  <h2>Projects:</h2>
  <h3>
    <a href="Project%20One.sql">Project One: Sales Analysis</a>
  </h3>
  <p>Analyzing sales data to identify top-selling products, sales trends, and performance metrics.</p>
  <h3>
    <a href="Project%20Two.sql">Project Two: Returns and Orders Analysis</a>
  </h3>
  <p>Investigating returns and orders data to understand return rates, product performance, and more.</p>
  <h3>
    <a href="Module%20Three%20Activity.sql">Module Three Activity: Database Creation</a>
  </h3>
  <p>Creating and setting up a database as part of Module Three coursework.</p>
  <h3>
    <a href="Module%20Four.sql">Module Four: Data Retrieval</a>
  </h3>
  <p>SQL script for retrieving specific data from the database, focusing on querying techniques.</p>
  <h3>
    <a href="Module%20Five.sql">Module Five: Advanced Queries</a>
  </h3>
  <p>Exploring advanced SQL queries for complex data analysis and reporting.</p>

<hr>

```bash
> Select Customers.State, Count(Distinct RMAID) AS Returns
From Customers
Left Join Orders
On Orders.CollaboratorID = Customers.CollaboratorID
Inner Join RMA
ON Orders.OrderID = RMA.OrderID
Group by State
Order by Returns DESC;
>+-------+---------+
| State | Returns |
+-------+---------+
| CA    |      10 |
| NY    |       8 |
| TX    |       7 |
| FL    |       5 |
| IL    |       4 |
| PA    |       3 |
| OH    |       2 |
| GA    |       2 |
| MI    |       1 |
| WA    |       1 |
+-------+---------+
10 rows in set (0.00 sec)
>
> Select SKU, Count(Orders.OrderID)
From Orders
Group by SKU;
>+--------+---------------------+
| SKU    | Count(Orders.OrderID)|
+--------+---------------------+
| SKU123 |                   15 |
| SKU456 |                   12 |
| SKU789 |                   10 |
| SKU101 |                    8 |
| SKU202 |                    6 |
| SKU303 |                    5 |
| SKU404 |                    3 |
| SKU505 |                    2 |
+--------+---------------------+
8 rows in set (0.00 sec)
>
>Select SKU, Count(RMAID)
From RMA
Inner Join Orders
on Orders.OrderID = RMA.OrderID
Group by SKU;
>+--------+-----------------+
| SKU    | Count(RMAID)    |
+--------+-----------------+
| SKU123 |               5 |
| SKU456 |               4 |
| SKU789 |               3 |
| SKU101 |               2 |
| SKU202 |               2 |
| SKU303 |               1 |
| SKU404 |               1 |
+--------+-----------------+
7 rows in set (0.00 sec)
>
>Select Orders.SKU, Count(Distinct Orders.OrderID) As Orders, RMA_Count, (RMA_Count / Count(*) * 100) AS 'Return Rate %'
From Orders
left join (
Select SKU, Count(Distinct RMAID) as RMA_Count
From RMA
Inner Join Orders
on Orders.OrderID = RMA.OrderID
Group by SKU
) As RMA_Count_join
on RMA_Count_join.SKU = Orders.SKU
Group by SKU
Order by Orders DESC;
>+--------+--------+-----------+---------------+
| SKU    | Orders | RMA_Count | Return Rate % |
+--------+--------+-----------+---------------+
| SKU123 |     15 |         5 |         33.33 |
| SKU456 |     12 |         4 |         33.33 |
| SKU789 |     10 |         3 |         30.00 |
| SKU101 |      8 |         2 |         25.00 |
| SKU202 |      6 |         2 |         33.33 |
| SKU303 |      5 |         1 |         20.00 |
| SKU404 |      3 |         1 |         33.33 |
| SKU505 |      2 |         0 |          0.00 |
+--------+--------+-----------+---------------+
8 rows in set (0.01 sec)
>
>+-----------+--------------------+-----------+
| Cust. ID  | Customer            | RMA_Count |
+-----------+--------------------+-----------+
| CUST00123 | John Doe            |         5 |
| CUST00456 | Jane Smith          |         4 |
| CUST00789 | Emily Johnson       |         4 |
| CUST00234 | Michael Brown       |         3 |
| CUST00890 | Chris White         |         3 |
+-----------+--------------------+-----------+
5 rows in set (0.01 sec)
>
>select count(*),Reason 
from RMA
Group by Reason;
>+----------+------------------------+
| count(*) | Reason                 |
+----------+------------------------+
|       12 | Defective Product       |
|        8 | Wrong Item Shipped      |
|        6 | Customer Changed Mind   |
|        4 | Item Damaged in Transit |
|        3 | Other                   |
+----------+------------------------+
5 rows in set (0.00 sec)
>
>select count(*),Status 
from RMA
Group by Status;
>+----------+-----------+
| count(*) | Status    |
+----------+-----------+
|       10 | Approved  |
|        8 | Pending   |
|        7 | Rejected  |
|        4 | Completed |
|        4 | In Review |
+----------+-----------+
5 rows in set (0.00 sec)
>
>select count(*) as Amount, Step 
from RMA
Group by Step
Order by Amount DESC;
>+--------+----------------------+
| Amount | Step                 |
+--------+----------------------+
|     12 | Initial Review       |
|      9 | Awaiting Inspection  |
|      8 | Completed            |
|      7 | Awaiting Approval    |
|      5 | Shipped Back to Vendor|
+--------+----------------------+
5 rows in set (0.00 sec)
```
<hr>

