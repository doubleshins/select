# 常用SQL語法

## SQL Select：
```bash
SELECT "欄位名" FROM "表格名";
Select * from books;
```

## SQL Distinct
我們會經常碰到需要找出表格內的不同 資料值的情況。
我們需要知道這個表格/欄位內有哪些不同的值，而每個值出現的次數並不重要。 
```bash
SELECT DISTINCT "欄位名"
FROM "表格名";
SELECT DISTINCT Store_Name FROM Store_Information;
```


## SQL WHERE
```bash
SELECT "欄位名"
FROM "表格名"
WHERE "條件";

Select  title, publisher
From books
Where auther = "ABC";
```


## SQL And Or
```bash
SELECT "欄位名"
FROM "表格名"
WHERE "簡單條件"
{[AND|OR] "簡單條件"}+;

SELECT Store_Name
FROM Store_Information
WHERE Sales > 1000
OR (Sales < 500 AND Sales > 275);
```


## SQL In
```bash
SELECT "欄位名"
FROM "表格名"
WHERE "欄位名" IN ('值一', '值二', ...);

SELECT *
FROM Store_Information
WHERE Store_Name IN ('Los Angeles', 'San Diego');
```



## SQL Between
```bash
SELECT "欄位名"
FROM "表格名"
WHERE "欄位名" BETWEEN '值一' AND '值二';

SELECT *
FROM Store_Information
WHERE Txn_Date BETWEEN 'Jan-06-1999' AND 'Jan-10-1999';
```

## 萬用字元  LIKE

- 'A_Z': 所有以 'A' 起頭，另一個任何值的字原，且以 'Z' 為結尾的字串。 'ABZ' 和 'A2Z' 都符合這一個模式，而 'AKKZ' 並不符合 (因為在 A 和 Z 之間有兩個字元，而不是一個字元)。
- 'ABC%': 所有以 'ABC' 起頭的字串。舉例來說，'ABCD' 和 'ABCABC' 都符合這個模式。
- '%XYZ': 所有以 'XYZ' 結尾的字串。舉例來說，'WXYZ' 和 'ZZXYZ' 都符合這個模式。
- '%AN%': 所有含有 'AN'這個模式的字串。舉例來說， 'LOS ANGELES' 和 'SAN FRANCISCO' 都符合這個模式。
- '_AN%'： 所有第二個字母為 'A' 和第三個字母為 'N' 的字串。舉例來說，'SAN FRANCISCO' 符合這個模式，而 'LOS ANGELES' 則不符合這個模式。



## SQL Like
```bash
SELECT "欄位名"
FROM "表格名"
WHERE "欄位名" LIKE {模式};

SELECT *
FROM Store_Information
WHERE store_name LIKE '%AN%';
```


## SQL Order By
ASC 代表結果會以由小往大的順序列出，而 DESC 代表結果會以由大往小的順序列出。
```bash
SELECT "欄位名"
FROM "表格名"
[WHERE "條件"]
ORDER BY "欄位名" [ASC, DESC];


SELECT Store_Name, Sales, Txn_Date
FROM Store_Information
ORDER BY Sales DESC;
```



## SQL Order By
- AVG (平均)
- COUNT (計數)
- MAX (最大值)
- MIN (最小值)
- SUM (總合)
- COUNT(個數)
```bash
SELECT "函數名"("欄位名")
FROM "表格名";
```

## SQL Group By
需求變成是要算出每一間店 (Store_Name) 的營業額 (Sales)
```bash
SELECT "欄位1", SUM("欄位2")
FROM "表格名"
GROUP BY "欄位1";

SELECT Store_Name, SUM(Sales)
FROM Store_Information
GROUP BY Store_Name;
```

## SQL Having
知道哪些店的營業額有超過 $1,500
```bash
SELECT "欄位1", SUM("欄位2")
FROM "表格名"
GROUP BY "欄位1"
HAVING (函數條件);

SELECT Store_Name, SUM(Sales)
FROM Store_Information
GROUP BY Store_Name
HAVING SUM(Sales) > 1500;
```


## SQL Alias
欄位別名 及 表格別名。
```bash
SELECT "表格別名"."欄位1" "欄位別名"
FROM "表格名" "表格別名";

SELECT A1.Store_Name Store, SUM(A1.Sales) "Total Sales"
FROM Store_Information A1
GROUP BY A1.Store_Name;

結果
Store	Total Sales
Los Angeles	1800
San Diego	250
Boston	700

```


## SQL AS

```bash
SELECT "表格別名"."欄位1" "欄位別名"
FROM "表格名" "表格別名";

SELECT A1.Store_Name AS Store, SUM(A1.Sales) AS 'Total Sales'
FROM Store_Information AS A1
GROUP BY A1.Store_Name;
```



## SQL SUBSTRING 函數
```bash
SUBSTR (str, pos)
以上語法的意思是，由 <str> 中，選出所有從第 <pos> 位置開始的字元。請注意，這個語法不適用於SQL Server上。
SUBSTR (str, pos, len)
以上語法的意思是，由 <str> 中的第 <pos> 位置開始，選出接下去的 <len> 個字元。


SELECT SUBSTR(Store_Name, 3)
FROM Geography
WHERE Store_Name = 'Los Angeles';
```




## SQL Trim 函數
用來移除掉一個字串中的字頭或字尾
```bash
TRIM ( [ [位置] [要移除的字串] FROM ] 字串): 

LTRIM (字串): 將所有字串起頭的空白移除。

RTRIM (字串): 將所有字串結尾的空白移除。

SELECT TRIM ('   Sample   ');

SELECT LTRIM ('   Sample   ');

SELECT RTRIM ('   Sample   ');
```





## SQL Length 函數
- MySQL: LENGTH( )
- Oracle: LENGTH( )
- SQL Server: LEN( )
```bash
Length (str)

SELECT Length (Store_Name)
FROM Geography
WHERE Store_Name = 'Los Angeles';


結果:

11
```




## SQL Replace 函數
Replace函數是用來改變一個字串的內容。
```bash
Replace (str1, str2, str3)


SELECT REPLACE (Region_Name, 'ast', 'astern')
FROM Geography;
```



## 參考網址

[SQL語法教學](https://www.1keydata.com/tw/sql)
