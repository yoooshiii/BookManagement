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

0.

```
SELECT Customers.PrefectturalID, Prefectturals.PrefecturalName AS '都道府県', count(＊) AS '顧客数'
FROM Customers
    JOIN
        Prefecturals
    ON 
        Customers.PrefecturalID = Prefecturals.PrefecturalID
GROUP BY
    Customers.PrefecturalID
    ,Prefecturals.PrefecturalName;
```

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

0.

```
SELECT d.DepartmentName AS '部門名', AVG(s.Amount) AS '部門別平均給与額'
FROM Salary s
    JOIN BelongTo b
    ON s.EmployeeID = b.EmployeeID
    JOIN Departments d
    ON b.DepartmentID = d,DepartmentID
    JOIN Employees e
    ON b.EmployeeID = e.EmployeeID
GROUP BY d.DepartmentName;
```

1.

```
SELECT s.CategoryID, c.CategoryName AS 'カテゴリ名', p.Quantity AS '数量合計'
FROM Sales s
    JOIN Products p
    ON s.ProductID = p.ProductID
    JOIN Categories c
    ON s.CategoryID = c.Cattegory
GROUP BY PrefecturalID;
```

2.

```
SELECT SUM(c.Quantity) AS '合計数量',s.PrefectturalID,p.PrefecturalName AS '県名'
FROM Sales s
    JOIN Customers c
    ON s.CustomerID = c.CustomerID
    JOIN Prefecturals p
    ON p.PrefecturalID = s.PrefecturalID
GROUP BY PrefecturalID    
```

3.

```
SELECT MAX(c.Quantity) AS '最大数量',s.CustomerClassID,cc.CustomerClassName AS '顧客クラス名'
FROM Sales s
    JOIN Customers c
    ON s.CustomerID = s.CustomerID
    JOIN CustomerClasses cc
    ON c.CustomerClassID = cc.CustomerClassID
GROUP BY cc.CustomerID    
```

4.

```
SELECT PrefecturalID
    ,SUM(Quantity IN (
        SELECT c.Quantity
        FROM Customers c
        WHERE c.CustomerID = CustomerID
    )) AS '合計数量'
    ,PrefecturalName IN (
        SELECT p.PrefecturalName
        FROM Prefecturals p
        WHERE p.PrefecturalID = PrefecturalID
    ) AS '県名'
FROM Sales
GROUP BY PrefecturalID 
```

5.

```
SELECT CustomerClassID
    ,MAX(Quantity IN (
        SELECT Quantity
        FROM Customers c
        WHERE c.CustomerID = CustomerID
    )) AS '最大数量'
    ,CustomerClassName IN(
        SELECT CustomerClassName
        FROM CustomerClasses cc
        WHERE cc.CustomerClassesID = CustomerClasses
    ) AS '顧客クラス名'
FROM Sales
GROUP BY CustomerID    
```

### 20 / 45 p 163,164,165,166,167 (その4)

0.

```
SELECT p.ProducttName
    ,AVG(
        p.Price *
        CASE
            WHEN s.Quantity IS NULL THEN 0
            ELSE s.Quantity
        END
    ) AS '平均販売価格'
FROM 
        Product AS p
    LEFT OUTER JOIN 
            Sales AS s
    ON
            s.ProductID = p.ProductID
GROUP BY p.ProductName;
```


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
