# SQL Server joins

Use a join to combine rows from two tables based on a matching column.

## Sample data

```sql
DECLARE @Customers TABLE (CustomerID int, CustomerName varchar(30));
DECLARE @Orders TABLE (OrderID int, CustomerID int);

INSERT INTO @Customers VALUES (1, 'Asha'), (2, 'Nila');
INSERT INTO @Orders VALUES (101, 1), (102, 1);
```

Run the setup and the queries below in the same batch.

## INNER JOIN

Returns one row for each matching customer and order.

```sql
SELECT c.CustomerName, o.OrderID
FROM @Customers AS c
INNER JOIN @Orders AS o ON o.CustomerID = c.CustomerID
ORDER BY c.CustomerID, o.OrderID;
```

| CustomerName | OrderID |
| --- | ---: |
| Asha | 101 |
| Asha | 102 |

## LEFT JOIN

Keeps every customer. Customers without an order have a NULL OrderID.

```sql
SELECT c.CustomerName, o.OrderID
FROM @Customers AS c
LEFT JOIN @Orders AS o ON o.CustomerID = c.CustomerID
ORDER BY c.CustomerID, o.OrderID;
```

| CustomerName | OrderID |
| --- | ---: |
| Asha | 101 |
| Asha | 102 |
| Nila | NULL |

## Practice

Use a LEFT JOIN and COUNT(o.OrderID) to show the number of orders for each customer. The expected counts are 2 for Asha and 0 for Nila.
