## 第3章 複数のテーブルを扱う

### 17 / 45 p135,136,137,138

0.

まだ販売されていない商品を一覧に出すときの場合。
```
SELECT *
FROM Products
WHERE ProductID NOT IN (
    SELECT ProductID 
    FROM Sales
  )
;
```

1.

```
SELECT EmployeeID, EmployeeName
FROM Employees
WHERE Amount IN (
    SELECT Amount
    FROM Salary
    GROUP BY EmployeeID
    WHERE MAX(Amount) >= 300000
  );
```

2.

```
SELECT SaleID, Quantity,CustomerID,(
    SELECT CustomerName
    FROM Customers
    WHERE CustomerID = Sales.CostomerID
   ) AS '顧客名'
FROM Sales
WHERE Quantity >= 100;
```

3.

```
SELECT ProductID, ProductName
FROM Pruducts 
WHERE ProductID IN
(
  SELECT ProductID
  FROM Sales
  GROUP BY ProductID
  HAVING SUM(Quantity) >= 100
);
```

4.

```
SELECT EmployeeID, EmployeeName ,Amount IN (
    SELECT Amount
    FROM Salary
    GROUP BY EmployeeID
    WHERE MAX(Amount) >= 300000
  ) AS '最高給与額'
FROM Employees
;
```

5.

```
SELECT SaleID, Quantity,CustomerID,(
    SELECT CustomerName
    FROM Customers
    WHERE CustomerID = Sales.CostomerID
   ) AS '顧客名',(
    SELECT ProductName
    FROM Products
    WHERE ProductID = Products.ProductID
   ) AS '商品名'
FROM Sales
WHERE Quantity >= 100;
```

### 18 / 45 p147,148,149,150

1.

```
SELECT e.EmployeeName, s.PayDate,s.Amount
FROM 
    Salary s
  JOIN
    Employees e
  ON
    s.EmployeeID = e.Employees
ORDER BY s.EmployeeID;
```

2.

```
SELECT s.Quantity,c.CustomerName,p.ProductName, e.EmployeeName
FROM 
    Sales s
  JOIN
    Customers c 
  ON
    s.CustomerID = c.CustomerID
  JOIN
    Products p
  ON
    s.ProductID = p.ProductID
  JOIN
    Employees e
  ON
    s.EmployeeID = e.EmployeeID
WHERE s.Quantity >=200
;
```

3.

```
SELECT SUM(s.Quantity) AS '数量合計',s.ProductID,p.ProductName
FROM 
    Sales s
  JOIN
    Products p
  ON
    s.ProductID = p.ProductID
GROUP BY s.ProductID
HAVING SUM(s.Quantity) >= 300
```

4.

```
SELECT 
  s.Quantity,
  CustomerName IN (
    SELECT CustomerName
    FROM Customers
    WHERE 
      Sales.CustomerID = CustomerID
  )
  ,ProductName IN (
    SELECT ProductName
    FROM Products
    WHERE
      Sales.ProductID = ProductID
  )
  ,EmployeeName IN (
    SELECT EmployeeName
    FROM Employees
    WHERE
      Sales.EmployeeID = EmployeeID
  )
FROM 
    Sales
WHERE Quantity >=200;
```

5.

```
SELECT CustomerName,PrefecturalName,CustomerClassName
FROM Customers c,Prefecturals p,CustomerClasses cc
WHERE c.PrefecturalID = p.PrefecturalID, c.CustomerClassID = cc.CustomerClassID
ORDER BY PrefecuturalID;
```

### 19 / 45 p 154,155,156,156.157

1.

```

```

2.

```

```

3.

```

```

4.

```

```

5.

```

```

### 20 / 45 p ,

1.

```

```

2.

```

```

3.

```

```

4.

```

```

5.

```

```
