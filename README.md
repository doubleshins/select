# MySQL 教學範本

## 連線
- 指令一：mysql –h Host – u User -pPassword
- 指令二：mysql –h Host – u User –p
Enter password: ********
- 指令三：mysql

"-h" 代表指定連線主機參數， Host 代表主機名稱，可用數字碼，或是網域名稱。
"-u" 代表帳號參數，User 為使用者帳號。
"-p"表示密碼參數，Password 為使用者自己設定之密碼，"-p"和密碼間不能有空格。
指令一之密碼直接在"-p"之後輸入，輸入之密碼將直接顯示在螢幕上。
指令二之密碼在輸入"-p"之後，按 Enter 鍵，然後輸入密碼

## 離線

離線指令有下列兩種型式：
指令一： QUIT
指令二： \q 

![](https://i.imgur.com/6rQNoKl.png)


## 建立資料庫
語法：Create Database資料庫名稱;

新增資料庫
CREATE DATABASE `my_db`;

新增使用者，設定密碼
CREATE USER 'my_user'@'localhost' IDENTIFIED BY '輸入自訂密碼';

設定使用者權限
GRANT ALL PRIVILEGES ON my_db.* TO 'my_user'@'localhost';

use my_db;



## 備份資料庫

指令 1:
    mysqldump 目標資料庫 -u 帳號 -p > 備份檔案名稱
指令 2 (不備份資料)
    mysqldump 目標資料庫 -d -u 帳號 -p > 備份檔案名稱
指令 3 (不加註解):
    mysqldump 目標資料庫 --comment=0 -u 帳號 -p > 備份檔案名稱
指令 4 (包含資料庫建檔指令):
    mysqldump 目標資料庫 -d -u 帳號 --databases -p > 備份檔案名稱
    

## 建立暫時性資料表
語法：Create Temporary Table資料庫名稱（欄位定義）;
說明：資料表將建立在記憶體內，資料處理完後可予以刪除，離線後該表
將自動被刪除。暫存表可用於整理過渡資料。

## 刪除資料表
語法：Drop Table資料表名稱 ; 


## 顯示資料表明細
語法：Show Tables;

![](https://i.imgur.com/LIwPvHH.png)


## 顯示資料表結構
語法：Describe 資料表名稱;
範例：Describe cuinfo; 

![](https://i.imgur.com/Vd0Wp42.png)



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

說明：
Count：計算筆數，
Sum：計算總和，
AVG：計算平均，
Std：計算母體標準差，
StdDev_Samp：計算樣本標準差，
Max：計算最大值，
Min：計算最小值。


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

http://web.nuu.edu.tw/~carlu/html/eBook/EasydoMySQL/CH2.pdf
