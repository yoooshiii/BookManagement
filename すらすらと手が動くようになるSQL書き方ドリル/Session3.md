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

1.答え合わせ　未

```
SELECT s.CategoryID, c.CategoryName AS 'カテゴリ名', SUM(p.Quantity) AS '数量合計'
FROM Sales s
    JOIN 
        Products p
    ON
        s.ProductID = p.ProductID
    JOIN
        Categories c
    ON
        s.CategorieID = c.CategorieID
GROUP BY s.CategoryID;
```

2.答え合わせ　未

```
SELECT s.PrefecturalID, p.PrefecturalName AS '県名', SUM(c.Quantity) AS '合計数量'
FROM Sales s
    JOIN Customers c
    ON s.CustomerID = c.CustomerID
    JOIN Prefectural p
    ON s.PrefecturalID = p.PrefecturalID
GROUP BY s.PrefecturalID    
```

3.答え合わせ　未

```
SELECT s.CustomerClass ,cc.CustomerClassName AS '顧客クラス名',MAX(c.Quantity) AS '最大数量'
FROM Sales s
    JOIN Customers c
    ON s.CustomerID = c.CustomerID
    JOIN CustomerClasses cc
    ON s.CustomerClassID = cc.CustomerClassID
GROUP BY s.CustomerClassID
```

4.

```
SELECT s.PrefecturalID
     ,PrefecturalName IN (
        SELECT PrefecturalName
        FROM Prefectural
        WHERE s.PrefecturalID = PrefecturalID
    ) AS '県名'
    ,Quantity IN(
        SELECT SUM(Quantity)
        FROM Customers
        WHERE s.CustomerID = CustomerID
    ) AS '合計数量'
FROM Sales s
GROUP BY s.PrefecturalID;
```

5.

```
SELECT s.CustomerClass
    ,CustomerClassName IN(
        SELECT CustomerClassName
        FROM CustomerClasses
        WHERE CustomerClassID = s.CustomerClassID
    ) AS '顧客クラス名'
    ,Quantity IN(
        SELECT MAX(Quantity)
        FROM Customers
        WHERE s.CustomerID = CutomerID
    ) AS '最大数量'
FROM Sales s
GROUP BY s.CustomerClassID
```

### 20 / 45 p 163,164,165,166

0.

```
SELECT p.ProductName
    ,AVG(
        p.Price *
        CASE
            WHEN s.Quantity IS NULL THEN 0
            ELSE s.Quantity 
        END
    ) AS '平均販売価格'
FROM Products AS p
LEFT OUTER JOIN Sales AS s
ON s.ProductID = p.ProductID
GROUP BY p.ProductName;
```

1.

```
SELECT CustomerName 
    , SUM(s.Quantity *
        CASE
            WHEN c.CustomerID IS NULL THEN 0
            ELSE c.CustomerID
        END
    ) AS '合計'
FROM Customers c
LEFT JOIN Sales s
ON s.CustomerID = c.CustomerID
GROUP BY CustomerID;
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
