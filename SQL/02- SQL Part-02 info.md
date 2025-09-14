**JOINS**

In a DBMS, a join is an operation that combines rows from two or more tables based on a related column between them.
Joins are used to retrieve data from multiple tables by linking them together using a common key or column.

Types of Joins:

1. Inner Join
2. Outer Join
3. Cross Join
4. Self Join

**1) Inner Join:**

An inner join combines data from two or more tables based on a specified condition, known as the join condition.

The result of an inner join includes only the rows where the join condition is met in all participating tables.

It essentially filters out non-matching rows and returns only the rows that have matching values in both tables.

Syntax:

SELECT columns FROM table1 INNER JOIN table2 ON table1.column = table2.column;

● columns refers to the specific columns you want to retrieve from the tables.

● table1 and table2 are the names of the tables you are joining.

● column is the common column used to match rows between the tables.

● The ON clause specifies the join condition, where you define how the tables are related.

| CustomerID | CustomerName |
| ---------- | ------------ |
| 1          | Alice        |
| 2          | Bob          |
| 3          | Carol        |

Orders Table:

| OrderID | CustomerID | Product    |
| ------- | ---------- | ---------- |
| 101     | 1          | Laptop     |
| 102     | 3          | Smartphone |
| 103     | 2          | Headphones |

**Inner Join Query:**


SELECT Customers.CustomerName, Orders.Product FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

Result:

| CustomerName | Product    |
| ------------ | ---------- |
| Alice        | Laptop     |
| Bob          | Headphones |
| Carol        | Smartphone |

**2) Outer Join**
   
Outer joins combine data from two or more tables based on a specified condition, just like inner joins. However, unlike inner joins, outer joins also include rows that do not have matching values in both tables.
Outer joins are particularly useful when you want to include data from one table even if there is no corresponding match in the other table.

**Types:**

There are three types of outer joins: left outer join, right outer join, and full outer join.

1. Left Outer Join (Left Join):
   
A left outer join returns all the rows from the left table and the matching rows from the right table.

If there is no match in the right table, the result will still include the left table's row with NULL values in the right table's columns.

Example:

SELECT Customers.CustomerName, Orders.Product FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

Result:

| CustomerName | Product    |
| ------------ | ---------- |
| Alice        | Laptop     |
| Bob          | Headphones |
| Carol        | Smartphone |
| **NULL**     | Monitor    |

In this example, the left outer join includes all rows from the Customers table.

Since there is no matching customer for the order with OrderID 103 (Monitor), the result includes a row with NULL values in the CustomerName column.

**2. Right Outer Join (Right Join):**
   
A right outer join is similar to a left outer join, but it returns all rows from the right table and the matching rows from the left table.

If there is no match in the left table, the result will still include the right table's row with NULL values in the left table's columns.

Example: Using the same Customers and Orders tables.

SELECT Customers.CustomerName, Orders.Product FROM Customers RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

Result:

| CustomerName | Product    |
| ------------ | ---------- |
| Alice        | Laptop     |
| Carol        | Smartphone |
| Bob          | Headphones |
| **NULL**     | Keyboard   |

Here, the right outer join includes all rows from the Orders table. Since there is no matching
order for the customer with CustomerID 4, the result includes a row with NULL values in the
CustomerName column.

**3. Full Outer Join (Full Join)**:
   
A full outer join returns all rows from both the left and right tables, including matches and non-matches.

If there's no match, NULL values appear in columns from the table where there's no corresponding value.

Example: Using the same Customers and Orders tables.

SELECT Customers.CustomerName, Orders.Product FROM Customers FULL OUTER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

Result:

| CustomerName | Product    |
| ------------ | ---------- |
| Alice        | Laptop     |
| Bob          | Headphones |
| Carol        | Smartphone |
| NULL         | Monitor    |
| NULL         | Keyboard   |

In this full outer join example, all rows from both tables are included in the result. Both
non-matching rows from the Customers and Orders tables are represented with NULL
values.

**3) Cross Join**
   
A cross join, also known as a Cartesian product, is a type of join operation in a Database
Management System (DBMS) that combines every row from one table with every row from
another table.

Unlike other join types, a cross join does not require a specific condition to match rows
between the tables. Instead, it generates a result set that contains all possible combinations
of rows from both tables.

Cross joins can lead to a large result set, especially when the participating tables have many
rows.

Syntax:

SELECT columns FROM table1 CROSS JOIN table2;

In this syntax:

● columns refers to the specific columns you want to retrieve from the cross-joined
tables.

● table1 and table2 are the names of the tables you want to combine using a cross
join.

Example: Consider two tables: Students and Courses.

Student Table:

| StudentID | StudentName |
| --------- | ----------- |
| 1         | Alice       |
| 2         | Bob         |

Courses Table:

| CourseID | CourseName |
| -------- | ---------- |
| 101      | Maths      |
| 102      | Science    |

Cross Join Query:
SELECT Students.StudentName, Courses.CourseName
FROM Students CROSS JOIN Courses;

Result:

| StudentName | CourseName |
| ----------- | ---------- |
| Alice       | Maths      |
| Alice       | Science    |
| Bob         | Maths      |
| Bob         | Science    |

In this example, the cross join between the Students and Courses tables generates all
possible combinations of rows from both tables. As a result, each student is paired with each
course, leading to a total of four rows in the result set.

**4) Self Join**
   
A self join involves joining a table with itself.

This technique is useful when a table contains hierarchical or related data and you need to compare or analyse rows within the same table.

Self joins are commonly used to find relationships, hierarchies, or patterns within a single table.

In a self join, you treat the table as if it were two separate tables, referring to them with different aliases.

Syntax:

The syntax for performing a self join in SQL is as follows:

SELECT columns FROM table1 AS alias1 JOIN table1 AS alias2 ON alias1.column = alias2.column;

In this syntax:

● columns refers to the specific columns you want to retrieve from the self-joined table.
● table1 is the name of the table you're joining with itself.
● alias1 and alias2 are aliases you assign to the table instances for differentiation.
● column is the column you use as the join condition to link rows from the same table.

Example: Consider an Employees table that contains information about employees and their managers.

Employees Table:

| EmployeeID | EmployeeName | ManagerID |
| ---------- | ------------ | --------- |
| 1          | Alice        | 3         |
| 2          | Bob          | 3         |
| 3          | Carol        | NULL      |
| 4          | David        | 1         |

**Self Join Query:**

SELECT e1.EmployeeName AS Employee, e2.EmployeeName AS Manager

FROM Employees AS e1 JOIN Employees AS e2 ON e1.ManagerID = e2.EmployeeID;

Result:

| Employee | Manager |
| -------- | ------- |
| Alice    | Carol   |
| Bob      | Carol   |
| David    | Alice   |

In this example, the self join is performed on the Employees table to find the relationship
between employees and their managers. The join condition connects the ManagerID column
in the e1 alias (representing employees) with the EmployeeID column in the e2 alias
(representing managers).


**SET OPERATIONS:**

Set operations in SQL are used to combine or manipulate the result sets of multiple SELECT queries.

They allow you to perform operations similar to those in set theory, such as union,
intersection, and difference, on the data retrieved from different tables or queries.

Set operations provide powerful tools for managing and manipulating data, enabling you to
analyse and combine information in various ways.

There are four primary set operations in SQL:

● UNION
● INTERSECT
● EXCEPT (or MINUS)
● UNION ALL

1. UNION:
   
The UNION operator combines the result sets of two or more SELECT queries into a single
result set.

It removes duplicates by default, meaning that if there are identical rows in the result sets,
only one instance of each row will appear in the final result.

Example:

Assume we have two tables: Customers and Suppliers.

Customers Table:

| CustomerID | CustomerName |
| ---------- | ------------ |
| 1          | Alice        |
| 2          | Bob          |

Suppliers Table:

| SupplierID | SupplierName |
| ---------- | ------------ |
| 101        | SupplierA    |
| 102        | SupplierB    |

**UNION Query:**

SELECT CustomerName FROM Customers

UNION

SELECT SupplierName FROM Suppliers;

Result:

| Name      |
| --------- |
| Alice     |
| Bob       |
| SupplierA |
| SupplierB |

**2. INTERSECT:**

The INTERSECT operator returns the common rows that exist in the result sets of two or more SELECT queries.

It only returns distinct rows that appear in all result sets.

Example: Using the same tables as before.

SELECT CustomerName FROM Customers INTERSECT SELECT SupplierName FROM Suppliers;

Result:

| CustomerName |

In this example, there are no common names between customers and suppliers, so the result is an empty set.

**3. EXCEPT (or MINUS):**
 
The EXCEPT operator (also known as MINUS in some databases) returns the distinct rows
that are present in the result set of the first SELECT query but not in the result set of the
second SELECT query.

Example: Using the same tables as before.

SELECT CustomerName FROM Customers
EXCEPT SELECT SupplierName FROM Suppliers;

| CustomerName |
| ------------ |
| Alice        |
| Bob          |

In this example, the names "Alice" and "Bob" are customers but not suppliers, so they appear in the result set.

**4. UNION ALL:**

The UNION ALL operator performs the same function as the UNION operator but does not
remove duplicates from the result set. It simply concatenates all rows from the different
result sets.

Example: Using the same tables as before.

SELECT CustomerName FROM Customers UNION ALL SELECT SupplierName FROM Suppliers;

Result:

| CustomerName |
| ------------ |
| Alice        |
| Bob          |
| SupplierA    |
| SupplierB    |

**Difference between Set Operations and Joins:**

| Aspect                         | Set Operations                                                                                  | Joins                                                                                  |
| ------------------------------ | ----------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| **Purpose**                    | Manipulate result sets based on set theory principles.                                          | Combine data from related tables based on specified conditions.                        |
| **Data Source**                | Result sets of SELECT queries.                                                                  | Tables that are related by common columns.                                             |
| **Combining Rows**             | Combine rows from different result sets. May remove duplicates.                                 | Combine rows from different tables based on specified conditions.                      |
| **Output Columns**             | Require the SELECT queries to have the same number of output columns and compatible data types. | Can combine columns from different tables, regardless of data types or column numbers. |
| **Common Operations**          | UNION, INTERSECT, EXCEPT (MINUS).                                                               | INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL JOIN.                                          |
| **Conditional Requirements**   | No specific join conditions are required.                                                       | Require specified join conditions for combining data.                                  |
| **Handling Duplicates**        | UNION removes duplicates by default.                                                            | Joins do not inherently handle duplicates; it depends on the join type and data.       |
| **Usage Scenarios**            | Useful for combining and analysing related data from different queries or tables.               | Used to retrieve and relate data from different tables based on their relationships.   |
| **Result Set Structure**       | Result sets may have different column names, but data types and counts must match.              | Result sets can have different column names, data types, and counts.                   |
| **Performance Considerations** | Generally faster and less complex than joins.                                                   | Joins can be more complex and resource-intensive, especially for larger datasets.      |



**SUB QUERIES**

Subqueries, also known as nested queries or inner queries, allow you to use the result of
one query (the inner query) as the input for another query (the outer query).

Subqueries are often used to retrieve data that will be used for filtering, comparison, or
calculation within the context of a larger query.

They are a way to break down complex tasks into smaller, manageable steps.

Syntax:

SELECT columns FROM table WHERE column OPERATOR (SELECT column FROM table WHERE condition);

In this syntax:

● columns refers to the specific columns you want to retrieve from the outer query.

● table is the name of the table you're querying.

● column is the column you're applying the operator to in the outer query.

● OPERATOR is a comparison operator such as =, >, <, IN, NOT IN, etc.

● (SELECT column FROM table WHERE condition) is the subquery that provides the

input for the comparison.

Example: Consider two tables: Products and Orders.

Products Table:

| ProductID | ProductName | Price |
| --------- | ----------- | ----- |
| 1         | Laptop      | 1000  |
| 2         | Smartphone  | 500   |
| 3         | Headphones  | 50    |

Orders Table:

| OrderID | ProductID | Quantity |
| ------- | --------- | -------- |
| 101     | 1         | 2        |
| 102     | 3         | 1        |


For Example: Retrieve the product names and quantities for orders with a total cost greater
than the average price of all products.

SELECT ProductName, Quantity FROM Products WHERE Price * Quantity > (SELECT AVG(Price) FROM Products);

Result:

| ProductName | Quantity |
| ----------- | -------- |
| Laptop      | 2        |

**Differences Between Subqueries and Joins:**

| Aspect                         | Subqueries                                                                     | Joins                                                                      |
| ------------------------------ | ------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| **Purpose**                    | Retrieve data for filtering, comparison, or calculation within a larger query. | Combine data from related tables based on specified conditions.            |
| **Data Source**                | Result of one query used as input for another query.                           | Data from multiple related tables.                                         |
| **Combining Rows**             | Not used for combining rows; used to filter or evaluate data.                  | Combines rows from different tables based on specified join conditions.    |
| **Result Set Structure**       | Subqueries return scalar values, single-column results, or small result sets.  | Joins return multi-column result sets.                                     |
| **Performance Considerations** | Subqueries can be slower and less efficient, especially for large datasets.    | Joins can be more efficient for combining data from multiple tables.       |
| **Complexity**                 | Easier to understand for simple tasks or smaller datasets.                     | Can become complex, but suited for large-scale data retrieval/combination. |
| **Versatility**                | Can be used in various clauses: WHERE, FROM, HAVING, etc.                      | Primarily used in the FROM clause for combining tables.                    |








