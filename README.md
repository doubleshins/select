# select

- 瀏覽目前圖書館內有哪些藏書，SQL 命令如下：
```bash
Select * from books;
```

- 查詢作者粘添壽有哪些書的書名與出版公司，SQL 命令如下：
```bash
Select  title, publisher

From books

Where auther = “粘添壽”;
```

- 查詢東南圖書公司有那些書，請列印出書名作者名稱，SQL 命令如下：
```bash
select title, Author

from books

where publisher = "東南圖書公司";
```


select * from messages where cust_ID = (SELECT cust_ID from customers where name = "郭大豪")
