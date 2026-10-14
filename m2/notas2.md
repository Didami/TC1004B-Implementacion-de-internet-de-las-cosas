# Módulo Software

---

## XAMPP:

### Comandos iniciales:

```sh
/Applications/XAMPP/xamppfiles/bin/mysql -u root
```

```sql
show databases;
```

```sql
use w3schools;
```

Show all tables:

```sql
show tables;
```

Describe the table `employees`:

```sql
desc employees;
```

## Operaciones dentro de BD:

### Select:

Select all columns from table `employees`:

```sql
select * from employees;
```

Select columns `LastName`, `FirstName` and `BirthDate` from table `employees`:

```sql
select LastName, FirstName, BirthDate from employees;
```

Enlists each `Country` from table `customers`:

```sql
select distinct Country from customers;
```

Enumerate the number of distinct `Country` from table `customers`:

```sql
select count(distinct Country) from customers;
```

Select all columns from `customers` where the `Country` is Mexico:

```sql
select * from customers where Country = "Mexico";
```

Select all colums from `customers` where `City` starts with `s`:

```sql
select * from customers where city LIKE 's%';
```

`AND`, `OR` & `NOT` Operators

```sql
select * from customers where Country = "Germany" AND City = "Berlin";
```

```sql
 select * from customers where NOT Country = "Germany";
```

`ORDER BY` `ASC|DESC`:

```sql
select * from customers order by Country;
```

```sql
select * from customers order by Country, CustomerName;
```

### Insert:

```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

```sql
INSERT INTO customers (CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES ("El borrego viudo", "Sr. Borrego Hdez", "Tlalpan 123", "Mexico City", 34348, "Mexico");
```

```sql
INSERT INTO customers (CustomerName, City, Country)
VALUES ("Don Asado", "Mexico City", "Mexico");
```

### Update:

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

```sql
UPDATE customers
SET ContactName = "Sr. Don Gutierrez", Address = "En mi corazón", PostalCode = 67670
WHERE CustomerID = 93;
```

### Delete:

```sql
DELETE FROM table_name WHERE condition;
```

```sql
DELETE FROM customers WHERE CustomerID = 93;
```

**⚠️ Delete database:**

```sql
drop database w3schools;
```

#### Limit & Offset:

```sql
SELECT * from customers limit 3 offset 3;
```

### SQL Aggregate Functions:

```sql
SELECT ProductName, MAX(Price) from Products;
```

```sql
SELECT ProductName, Price from Products order by Price DESC limit 5;
```

```sql
SELECT min(column_name)
```

```sql
SELECT max(column_name)
```

```sql
SELECT count(column_name)
```

```sql
SELECT sum(column_name)
```

```sql
SELECT avg(column_name)
```

```sql
FROM table_name
WHERE condition;
```

```sql
SELECT * from products
WHERE price > (SELECT avg(price) from products);
```

### Big O! notation:

- `O(1)`
- `O(log n)`
- `O(n)`
- `O(n log n)`
- `O(n^2)`
- `O(2^n)`
- `O(n!)`

### LIKE / (WILDCARDS):

- The `%` wildcard represents any number of characters, even zero characters.

```sql
SELECT * from products WHERE city = "s%";
```

```sql
SELECT CustomerName from customers WHERE CustomerName LIKE "%or%";
```

- The `_` wildcard represents one single character.

```sql
SELECT CustomerName from customers WHERE CustomerName LIKE "_r%";
```

```sql
SELECT * FROM Customers WHERE city LIKE 'l_nd__';
```

| Symbol | Description                                                   |
| ------ | ------------------------------------------------------------- |
| `%`    | Represents zero or more characters                            |
| `_`    | Represents a single character                                 |
| `[]`   | Represents any single character within the brackets \*        |
| `^`    | Represents any character not in the brackets \*               |
| `-`    | Represents any single character within the specified range \* |
| `{}`   | Represents any escaped character \*\*                         |

### Alias:

```sql
SELECT CustomerName AS ListaDeClientes from customers ORDER BY ListaDeClientes ASC;
SELECT CustomerName AS "Lista de clientes" from customers ORDER BY "Lista de clientes" ASC;
```

### IN:

```sql
SELECT * FROM Customers
WHERE Country IN ('Germany', 'France', 'UK');
```

```sql
SELECT * FROM customers
WHERE CustomerID IN (SELECT CustomerID FROM orders);
```

- Every client that has made a purchase (does not return how many):

```sql
SELECT * FROM customers
WHERE CustomerID IN (SELECT CustomerID FROM orders);
```

- Every client that has made a purchase (does return how many):

```sql
SELECT orders.OrderID, customers.CustomerName, orders.OrderDate
FROM orders INNER JOIN customers
ON orders.CustomerID = customers.CustomerID;
```

### INNER JOIN:

![Inner Join](./images/sql/inner_join.png)

```sql
SELECT products.ProductName, categories.CategoryName
FROM products INNER JOIN categories
ON products.CategoryID = categories.CategoryID
LIMIT 10;
```

```sql
SELECT orders.OrderID, customers.CustomerName, shippers.ShipperName
FROM
(orders INNER JOIN customers ON orders.CustomerID = customers.CustomerID)
INNER JOIN shippers
ON orders.ShipperID = shippers.ShipperID;
```

### LEFT JOIN:

![Left Join](./images/sql/left_join.png)

```sql
SELECT customers.CustomerName, orders.OrderID
FROM customers
LEFT JOIN orders
ON customers.CustomerID = orders.CustomerID
ORDER BY customers.CustomerName;
```

```sql
SELECT COUNT(*)
FROM customers
LEFT JOIN orders
ON customers.CustomerID = orders.CustomerID
WHERE orders.OrderID IS NULL;
```

### RIGHT JOIN:

![Right Join](./images/sql/right_join.png)

```sql
SELECT orders.OrderID, employees.LastName, employees.FirstName
FROM orders
RIGHT JOIN employees
ON orders.EmployeeID = employees.EmployeeID
ORDER BY orders.OrderID;
```

```sql
SELECT orders.OrderID, employees.LastName, employees.FirstName
FROM employees
RIGHT JOIN orders
ON orders.EmployeeID = employees.EmployeeID
ORDER BY orders.OrderID;
```

### FULL JOIN:

![Full Join](./images/sql/full_outer_join.png)

`FULL JOIN` is **not** available in MARIADB. Use `UNION` instead:

```sql
SELECT c.CustomerID, c.CustomerName, o.OrderID, o.OrderDate
FROM customers AS c
LEFT JOIN orders AS o
ON c.CustomerID = o.CustomerID
UNION
SELECT c.CustomerID, c.CustomerName, o.OrderID, o.OrderDate
FROM customers AS c
RIGHT JOIN orders AS o
ON c.CustomerID = o.CustomerID;
```

### SELF JOIN:

```sql
SELECT
  a.CustomerName AS Cliente1,
  b.CustomerName AS Cliente2,
  a.City
FROM customers a, customers b
WHERE a.CustomerID <> b.CustomerID
AND a.City = b.City
ORDER BY a.City;
```

### GROUP BY:

```sql
SELECT COUNT(CustomerID), Country
FROM customers
GROUP BY Country;
```

```sql
SELECT COUNT(CustomerID), Country
FROM customers
GROUP BY Country
ORDER BY COUNT(CustomerID) DESC;
```

```sql
SELECT shippers.ShipperName, COUNT(orders.OrderID) AS NumeroDePaquetes
FROM orders LEFT JOIN shippers
ON orders.ShipperID = shippers.ShipperID
GROUP BY shippers.ShipperName
ORDER BY NumeroDePaquetes DESC;
```

### HAVING:

```sql
SELECT COUNT(CustomerID), Country
FROM customers
GROUP BY Country
HAVING COUNT(CustomerID) > 5
ORDER BY COUNT(CustomerID) DESC;
```

```sql
SELECT e.LastName, COUNT(o.OrderID) AS NumeroDeOrdenes
FROM orders AS o
INNER JOIN employees AS e
ON o.EmployeeID = e.EmployeeID
GROUP BY LastName
HAVING NumeroDeOrdenes > 10;
```

### ANY:

```sql
SELECT ProductName
FROM products
WHERE ProductID = ANY (
  SELECT ProductID
  FROM order_details
  WHERE Quantity = 10
);
```

### CASE:

```sql
SELECT
  OrderID,
  Quantity,
  CASE
    WHEN Quantity > 30 THEN 'Mas de treinta'
    WHEN Quantity = 30 THEN 'Igual a treinta'
    ELSE 'Menos de treinta'
  END AS TextoCantidad
FROM order_details;
```

```sql
SELECT CustomerName, City, Country
FROM customers
ORDER BY
  CASE
    WHEN City IS NULL THEN Country
    ELSE City
  END;
```
