## この書留は問題を解いた形跡に使用する。

ドリルを書き込むことができないので、この場を借りて実践を積むことを第一としてここで進めていく。
加えて、手書きよりタイピングした方が僕は速いのでこの方法をとる。

## 第2章

### 1/45 p27,28

1.

```
SELECT Address
FROM Customers;
```

2.

```
SELECT ProductName
FROM Products;
```

3.

```
SELECT Price
FROM Products;
```

4.

```
SELECT EmployeeName
FROM Employees;
```

5.

```
SELECT Email
FROM Employees;
```

### 2/45 p32,33

1.

```
SELECT CustomerName,Address
FROM Customers;
```

2.

```
SELECT ProuctID,ProductName,Price
FROM Products;
```

3.

```
SELECT EmployeeName, Email,Height
FROM Employees;
```

4.

```
SELECT CustomerCode,CustomerName,CustomerCode
FROM Customers;
```

5.

```
SELECT ProductCode,Price,ProductName,ProductCode
FROM Products;
```

### 3/45 p37,38

別名は別の用途で使用する際に区別できて便利なんやって。

1.

```
SELECT EmployeeName AS '社員名'
FROM Employees;
```

2.

```
SELECT CustormerCode AS '顧客コード',CustomerName AS '顧客名'
FROM Customers;
```

3.

```
SELECT ProductCode AS '商品コード',ProductName AS '商品名',Price AS '価格'
FROM Products;
```

4.

```
SELECT CustomerName AS '顧客名',Customer AS '得意先名'
FROM Customer;
```

5.

```
SELECT EmployeeName AS '社員名',Email AS 'メールアドレス',Email AS '連絡先'
FROM Employees;
```

### 4/45 p42,43

SQLの予約語を別名にしたいときは"(ダブルクォーテーション)で挟むこと。

1.

```
SELECT Amount *0.15 AS "給与の15%"
FROM Salary;
```

2.

```
SELECT Height / 2 AS '身長の半分'
FROM Employees;
```

3.

```
SELECT Weight * 3 - 50 AS '体重の3倍引く50'
FROM Rmployees;
```

4.

```
SELECT (Price + 100)*0.3 AS "(価格+100)の30%"
FROM Products;
```

5.

```
SELECT (Quantity + 200) /3 AS "(数量＋２００)÷3"
FROM Sales;
```

### 5/45 p48,49
SQL文で計算処理させるのおすすめじゃないんだよなぁ。。。。

1.

```
SELECT (Height *3) - (Weight*2.5) AS '結果'
FROM Employees;
```

2.

```
SELECT (HireFiscalYear / Weight) + Height AS '結果'
FROM Employees;
```

3.

```
SELECT Quantity + (CustomerID *ProductID*EmployeeID) AS '結果'
FROM Sales;
```

4.

```
SELECT Price - (ProductCode*CategoryID) AS '結果'
FROM Products;
```

5.

```
SELECT CudtomerID +(CustomerClassID ^3) AS '結果'
FROM Customers;
```

## 6/45 p53,54

SQLだけで名刺を作りたい！！！！！！！(無理じゃね？)

1.

```
SELECT EmployeeName || 'さん' AS '社員名'
FROM Employees;
```

2.

```
SELECT 'E-mail' || Email AS 'メールアドレス'
FROM Employees;
```

3.

```
SELECT EmployeeName || 'さんの' || 'E-MAIL' || Email AS '連絡先'
FROM Employees;
```

4.

```
SELECT CustomerName || '様のお住まいは' || Address AS 'お得意様連絡先'
FROM Customers;
```

5.

```
SELECT '社員' || EmployeeName || 'さんの血液型は' || BloodType || '型' AS '社員血液型'
FROM Employees;
```


## 7/45 p58,59

1.

```
SELECT SUM(CustomersID) AS 'お得意様'
FROM Customers;
```

2.

```
SELECT SUM(Weight) AS '社員体重合計'
FROM Employees;
```

3.

```
SELECT MAX(Price) AS '最高額価格'
FROM Products;
```

4.

```
SELECT MIN(Weight) AS '最軽量体重'
FROM Employees;
```

5.

```
SELECT AVG(Height) AS '平均身長',AVG(Weight) AS '平均体重'
FROM Employees;
```

## 8/45 p64,65
|x <> y |
|---|
|xとyが等しくないとき、T|

|x IN y |
|---|
|xがyの中のいずれかのとき、T|

|x EXISTS y |
|---|
|y(副問合せ)に存在する場合,T|

↑
だいたいJOINでできる。

1.

```
SELECT ProductName
FROM Products
WHERE Price >= 2500;
```

2.

```
SELECT EmployeeName,Weight
FROM Employees
WHERE Weight >= 70;
```

3.

```
SELECT EmployeeName,Height
FROM Employees
WHERE Height BETWEEN 160 AND 180;
```

4.

```
SELECT SaleID,
FROM Sales
WHERE SalesDate > '2007-06-01';
```

5.

```
SELECT EmployeeName,Height,Weight
FROM Employees
WHERE Height >= 170 AND Weight >= 60;
```

## 9/45 p70,71

1.

```
SELECT CustomerName AS '会社名'
FROM Customers
WHERE CustomerName LIKE '%株式会社%';
```

2.

```
SELECT AVG(Height) AS '平均身長'
FROM Employees
WHERE EmployeeName LIKE '%ー%';
```

3.

```
SELECT count(CustomerName) AS '顧客数'
FROM Customers
WHERE CustomerName LIKE '%株式会社%';
```

4.

```
SELECT EmployeeName,Height
FROM Employees
WHERE EmployeeName LIKE '%リ%' AND Height <=160;
```

5.

```
SELECT *
FROM Customers
WHERE CustomerName NOT LIKE '%株式会社%' AND Address LIKE '%江戸川区%';
```

## 10/45 p77,78
初見のため、0問目も解く。

0.

```
SELECT ProductName AS '商品名'
  ,CASE 
    WHEN Price < 1000 THEN 'C'
    WHEN Price < 2000 THEN 'B'
    ELSE 'A'
FROM Product;
```

1.

```
SELECT EmployeeName
  ,CASE 
    WHEN Height < 160 THEN 'A'
    WHEN Height >= 160 AND Height < 170 THEN 'B'
    WHEN Height >= 170 AND Height < 180 THEN 'C'
    ELSE 'D'
  END AS 'ランク'
FROM Employees;
```

2.

```
SELECT Salary AS '給与ID'
  ,CASE
    WHEN Amount < 150000 THEN 'D'
    WHEN Amount < 300000 AND Amount >= 150000 THEN 'C'
    WHEN Amount < 500000 AND Amount >= 300000 THEN 'B'
    ELSE 'A'
  END AS 'ランク'
FROM Salary;
```

3.

```
SELECT EmployeeName AS '社員名'
  ,CASE
    WHEN Weight <60 THEN 'A'
    WHEN Weight <70 AND Weight >=60 THEN 'B'
    WHEN Weight <80 AND Weight >=70 THEN 'C'
    ELSE 'D'
   END AS 'ランク'
FROM Employees;
```

4.

```
SELECT SaleID AS '販売ID'
  ,CASE 
    WHEN Quantity >=10 THEN 'A'
    WHEN Quantity <10 THEN 'B'
   END AS 'ランク'
FROM Sales;
```

5.

```
SELECT EmployeeName AS '社員名',Height AS '身長'
  ,CASE 
    WHEN Height < 160 THEN 'A'
    WHEN Height < 170 AND Height >=160 THEN 'B'
    WHEN Height < 180 AND Height >=170 THEN 'C'
    ELSE 'D'
  END AS 'ランク'
FROM Employees;
```

## 11/45 p85,86

1.

```
SELECT CustomerID AS '顧客ID',
       count(CustomerID) AS '件数'
FROM Sales
GROUP BY CustomerID;
```

2.

```
SELECT EmployeeID AS '社員ID',
       count(EmployeeID) AS '合計'
FROM Salary
GROUP BY EmployeeID;
```

3.

```
SELECT CustomerID AS '顧客ID',
       ProductID AS '商品ID'
       sum(Quantity) AS '数量'
FROM Sales
GROUP BY CustomerID,
         ProductID;   
```

4.

```
SELECT BloodType AS '血液型',AVG(Height) AS '平均身長', AVG(Weight) AS '平均体重' 
FROM Employees
GROUP BY BloodType;
```

5.

```
SELECT EmployeeID AS '社員ID', count(＊) AS '支給回数', AVG(Amount) AS '平均支給額'
FROM Salary
GROUP BY EmployeeID;
```

## 12/45 p92,93,94

0.

```
SELECT PrefecturalID, count(＊)
FROM Customers
GROUP BY PrefecturalID
HAVING count(＊) >= 3;
```

1.

```
SELECT EmployeeID AS '社員ID', count(＊) AS '社員ID'
FROM Salary
GROUP BY EmployeeID
HAVING count(＊) < 12;
```

2.

```
SELECT PrefecturID AS '県ID',count(＊) AS '顧客数'
FROM Customers
GROUP BY PrefecturalID 
HAVING PrefecturalID > 1;
```

3.

```
SELECT ProductID AS '商品ID',count(＊) AS '売上レコード数'
FROM Sales
GROUP BY ProductID
HAVING count(＊) BETWEEN 10 AND 50;
```

4.

```
SELECT BloodType AS '血液型', count(＊)
FROM Employees
GROUP BY BlooType
HAVING BlooType >=10;
```

5.

```
SELECT ProductID AS '商品ID', count(Quantity) AS '数量合計' 
FROM Sales
GROUP BY ProductID
HAVING count(Quantity) BETWEEN 100 AND 200;
```

## 13/45 p99,100,101

0.

```
SELECT PrefecturaID, count(＊)
FROM Customers
WHERE CustomerClassID = 1
GROUP BY PrefecturalID
HAVING count(＊) >= 2;
```

1.

```
SELECT PrefecturalID AS '県ID', count(＊) AS '顧客数'
FROM Customers
WHERE PrefecturalID >= 10
GROUP BY PrefecturalID
HAVING count(＊) > 1;
```

2.

```
SELECT EmployeeID AS '社員ID', count(＊) AS '支給回数'
FROM Salary
WHERE EmployeeID >= 20
GROUP BY EmployeeID
HAVING count(＊) >= 12;
```

3.

```
SELECT ProductID AS '商品ID', count(＊) AS '売上レコード数'
FROM Sales
WHERE ProductID BETWEEN 20 AND 30
GROUP BY ProductID 
HAVING count(＊) >= 30;
```

4.

```
SELECT BloodType AS '血液型', count(＊) AS 'データ件数'
FROM Employees
WHERE Height >= 165
GROUP BY BloodType
HAVING count(＊) >= 5;
```

5.

```
SELECT ProductID AS '商品ID', SUM(Quantity) AS '数量合計'
FROM Sales
WHERE SaleDate >= '2007-06-01'
GROUP BY ProductID
HAVING SUM(Quantity) >= 200;
```

## 14/45 p106,107,108,109,110,110,111,112

0.

```
SELECT HireFiscalYear AS '入社年度',
    SUM(
      CASE
        WHEN BloodType = 'A' THEN 1
        ELSE 0
      END
    ) AS 'A型',
    SUM(
      CASE
        WHEN BloodType = 'B' THEN 1
        ELSE 0
      END
    ) AS 'B型',
    SUM(
      CASE
        WHEN BloodType = 'O' THEN 1
        ELSE 0
      END
    ) AS 'O型',
    SUM(
      CASE
        WHEN BloodType = 'AB' THEN 1
        ELSE 0
      END
    ) AS 'AB型'
FROM Employees
GROUP BY HireFiscalYear;
```

1. 

```
SELECT HireFiscalYear AS '入社年度',
    SUM(
      CASE
        WHEN Height <= 160 THEN 1
        ELSE 0
      END
    ) AS '160cm以下',
    SUM(
      CASE 
        WHEN Height <= 170 THEN 1
        ELSE 0
      END
    ) AS '170cm以下',
    SUM(
      CASE
        WHEN Height <= 180 THEN 1
        ELSE 0 
      END
    ) AS '180cm以下',
    SUM(
      CASE
        WHEN Height > 180 THEN 1
        ELSE 0 
      END
    ) AS '180cm超'
FROM Employees
GROUP BY HireFiscalYear;
```

2.

```
SELECT CategoryID AS '商品カテゴリID', 
    SUM(
      CASE
        WHEN Price < 100 THEN 1
        ELSE 0
      END
    ) AS '100円未満',
    SUM(
      CASE
        WHEN Price <400 THEN 1
        ELSE 0
      END
    ) AS '400円未満',
    SUM(
      CASE
        WHEN Price <1000 THEN 1
        ELSE 0
      END
    ) AS '1000円未満',
    SUM(
      CASE
        WHEN Price >= 1000 THEN 1
        ELSE 0
      END
    ) AS '1000円以上'
FROM Products
GROUP BY CategoryID;
```

3.

```
SELECT CustomerID,
    SUM(
      CASE 
        WHEN MONTH( SaleDate ) = 9 THEN 1
        ELSE 0
      END 
    ) AS '9月',
    SUM(
      CASE 
        WHEN MONTH( SaleDate ) = 10 THEN 1
        ELSE 0 
      END 
    ) AS '10月',
    SUM(
      CASE 
        WHEN MONTH( SaleDate ) = 11 THEN 1
        ELSE 0 
      END 
    ) AS '11月'
FROM Sales
WHERE YEAR( SaleDate ) = 2006 
GROUP BY CustomerID;
```


4.

```
SELECT PrefecturalID AS '都道府県ID',
    COUNT(
      CASE
        WHEN CustomerClassID = 1 THEN 1
        ELSE 0
      END
    ) AS '法人',
    COUNT(
      CASE
        WHEN CustomerClassID = 2 THEN 1
        ELSE 0
      END
    ) AS '個人'
FROM Customers
GROUP BY PrefecturalID
```

5.

```
SELECT HireFiscalYear AS '入社年度',
    COUNT(
      CASE
        WHEN Weight <=50 THEN 1
        ELSE 0
      END
    ) AS '50kg以下',
    COUNT(
      CASE Weight <= 60 THEN 1
      END 0
    ) AS '60kg以下',
    COUNT(
      CASE Weight <=80 THEN 1
      END 0
    ) AS '80kg以下',
    COUNT(
      CASE Weight >80 THEN 1
      END 0
    ) AS '80kg超'
FROM Employees
GROUP BY HireFiscalYear;
```

## 15/45 p118,119,120

昇順(ASC)とは小さい順に並べること。降順(DESC)とは大きい順に並べること。

1.

```
SELECT EmployeeID, EmployeeName, BirthDay
FROM Employees
ORDER BY BirthDay ASC
```

2.

```
SELECT SaleID, Quantity, CustomerID, ProductID, SaleDate
FROM Sales
ORDER BY ProductID,CustomerID, SaleDate DESC;
```

3.

```
SELECT CategoryID, count(＊) AS '商品数'
FROM Products
WHERE Price <= 1000
GROUP BY CategoryID
HAVING count(＊) < 5
ORDER BY CategoryID;
```

4.

```
SELECT EmployeeID AS '社員ID', SUM(Amount) AS '給与合計'
FROM Salary
GROUP BY EmpoloyeeID
ORDER BY SUM(Amount) DESC;
```

5.

```
SELECT DepartmentID AS '部署ID',count(Employee)
FROM BelongTo
WHERE EndDate IS NULL
GROUP BY DepartmentID
ORDER BY count(Employee) DESC;
```

## 16/45 p123,124,125

0.

```
SELECT DISTINCT
    Address AS '住所'
FROM Customers;
```

1.

```
SELECT DISTINCT
   HireFiscalYear
FROM Employee;
```

2.

```
SELECT DISTINCT 
    CustomerID, ProductID
FROM Sales;
```

3.

```
SELECT DISTINCT
    CustomerClassID, PrefecturalID
FROM Customers;
```

4.

```
SELECT DISTINCT
    CustomerID,ProductID,EmployeeID
FROM Sales;
```

5.

```
SELECT DISTINCT 
    Price,CategoryID
FROM Products;    
```
