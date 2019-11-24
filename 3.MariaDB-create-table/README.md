# 這裡將會教學建立，操作表單/Table的方法

這裡將會教學一些 `Table` 的建立方法和一些小知識

## 第一步　建立Table

首先我們需要登入到 MariaDB 內，所以有按照前面的教學步驟的話，開啟 Terminal 輸入

```
mysql -u 你的使用者名稱 -p
Enter password:你的密碼
```

接下來我們使用上個教學所建立的資料庫，在 Terminal 內輸入

```
use 資料庫名稱;

範例:
MariaDB [(none)]> use test
Database changed
MariaDB [test]>
```

可以看到 `MariaDB [(none)]` 裡面已經被改變為 `MariaDB [test]` ，表示已經成功地更改成使用 `test` 的資料庫接著我們可以開始使用 `CREATE TABLE` 的指令了，我們可以參考官方的 Knowledge Base 有提供的寫法

```
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    (create_definition,...) [table_options    ]... [partition_options]
```

以中文表示為

```
建立 [或 取代] [是否作為暫存表] 表單 [如果不存在的話] 表單名稱
    (建立的表單內容)[表單設定]... [分類，分組方式];
Example:

CREATE TABLE IF NOT EXISTS user_id(       #建立名稱為user_id的表單，如果user_id不存在
    #表單內容描述
    id int(11) AUTO_INCREMENT PRIMARY KEY,

) ENGINE=InnoDB CHARSET=utf8           #表單設定，選項
#以什麼方式分類
PARTITION BY RANGE (id)(
    PARTITION less_than_fifty VALUES LESS THAN (50),
);
```

在上述的動作我們輸入的指令為，如果`user_id`不存在就建立名稱為`user_id`的表單。

接著就是描述表單的內容，我們在這設定了字元長度為11個的數字內容，欄位名稱為`id`，並使用`AUTO_INCREMENT`來讓他自動填入數值，在使用
`PRIMARY KEY`來設定 `id`這個欄位為主鍵，有興趣可以藉著官方的文件來知道更多的自訂方法。

連結:https://mariadb.com/kb/en/library/create-table/#column-definitions

再來介紹的是表單的設定及選項，我們設定支援的儲存引擎為`InnoDB`，其實還有更多不同的儲存引擎，礙於文章會變得又臭又長的關系，我交由其他的大神介紹，然後我們設定編碼方式為`utf8`，這是很常見的編碼方式，要是出來的資料變成亂碼的話可以試著用`ALERT TABLE`指令將編碼方式變換為`utf8`，說不定就能解決了，當然還有更多的表單設定和不同的自訂選項，有興趣依然可以藉著官方的文件來知道更多的自訂方法。

儲存引擎介紹連結:https://ssorc.tw/663

`table_options` 連結:https://mariadb.com/kb/en/library/create-table/#table-options

`PARTITION BY RANGE (id)`的意思則是以我們的 `id` 來分區，我們分類出 `less_than_fifty` 的區域，以`id`這個欄位的值來分類
只要`id`的值小於50就會被歸類這個分區，這也只是其中一種分區方法，詳細的可以參考接下來提供的文章，但請注意你如果使用了partition_options的方法，在做表單的 `DELETE` `INSERT` `UPDATE` 等更新資料的方法時語法會有些許的改變，要注意使用。

更詳細關於PARTITION的方法及介紹:https://peterli.website/那些在MySQL上的分區方式/

MariaDB 的其他 `PARTITION BY` 寫法:https://mariadb.com/kb/en/library/create-table/#partitions

## 第二步　操控表單

### 前言

這個部分我們基本上會簡單帶過，因為要一個一個把所有寫法都教完不是個好的方法，有需要再查文件跟著文件使用即可，這裡會教修改，刪除，查詢，以及資料的新增，修改，刪除，查詢

### 其之一　Table的修改，查詢，刪除

首先我們介紹修改以及查詢 `Table` 的語法，你可以使用 `SHOW TABLE STATUS` 先來確認你的表單狀態，在資料庫的世界中要知道狀態基本上都是 `show` 開頭的語法，這裡只先示範 `SHOW TABLE STATUS`，我們以上個教學所建立的表單為例子。

Example:

```
#丟出test資料庫內的表單狀態
MariaDB [test]> show table status\G
*************************** 1. row ***************************
            Name: user_id
          Engine: InnoDB
         Version: 10
      Row_format: Dynamic
            Rows: 2
  Avg_row_length: 16384
     Data_length: 32768
 Max_data_length: 0
    Index_length: 0
       Data_free: 0
  Auto_increment: 1
     Create_time: 2019-11-15 21:34:55
     Update_time: NULL
      Check_time: NULL
       Collation: utf8mb4_general_ci
        Checksum: NULL
  Create_options: partitioned
         Comment:
Max_index_length: 0
       Temporary: N
1 row in set (0.001 sec)
```

我們可以看到表單的名稱為 `user_id` 我們將把這個表單加入 `email` 欄位，順便將表單名稱改為 `user_profile` 我們在需要修改表單時需要用到 `ALTER TABLE` 的指令。

Example:

```
#重新命名user_id
MariaDB [test]>alter table user_id rename to user_profile;
Query OK, 0 rows affected (0.016 sec)
#使用show table status再次確認
MariaDB [test]> show table status\G
*************************** 1. row ***************************
            Name: user_profile
          Engine: InnoDB
         Version: 10
      Row_format: Dynamic
            Rows: 2
  Avg_row_length: 16384
     Data_length: 32768
 Max_data_length: 0
    Index_length: 0
       Data_free: 0
  Auto_increment: 1
     Create_time: 2019-11-24 12:32:57
     Update_time: NULL
      Check_time: NULL
       Collation: utf8mb4_general_ci
        Checksum: NULL
  Create_options: partitioned
         Comment:
Max_index_length: 0
       Temporary: N
1 row in set (0.001 sec)
#新增email的欄位在user_profile內
MariaDB [test]> alter table user_profile ADD COLUMN IF NOT EXISTS  (email varchar(254));
Query OK, 0 rows affected (0.010 sec)
Records: 0  Duplicates: 0  Warnings: 0
#使用SHOW COLUMNS來確認新增的欄位
MariaDB [test]> SHOW COLUMNS from user_profile;
+----------+--------------+------+-----+---------+----------------+
| Field    | Type         | Null | Key | Default | Extra          |
+----------+--------------+------+-----+---------+----------------+
| id       | int(11)      | NO   | PRI | NULL    | auto_increment |
| username | varchar(254) | YES  |     | NULL    |                |
| email    | varchar(254) | YES  |     | NULL    |                |
+----------+--------------+------+-----+---------+----------------+
3 rows in set (0.004 sec)
```

那為什麼 `SHOW COLUMNS` 跟 `show table status` 的表示方式不同呢? 原因就在於 `\G` 如果將 `SHOW COLUMNS from user_profile` 改為 `SHOW COLUMNS from user_profile\G`，那輸出方式將會如下

Example:

```
#使用\G的輸出結果
MariaDB [test]> SHOW COLUMNS from user_profile\G
*************************** 1. row ***************************
  Field: id
   Type: int(11)
   Null: NO
    Key: PRI
Default: NULL
  Extra: auto_increment
*************************** 2. row ***************************
  Field: username
   Type: varchar(254)
   Null: YES
    Key:
Default: NULL
  Extra:
*************************** 3. row ***************************
  Field: email
   Type: varchar(254)
   Null: YES
    Key:
Default: NULL
  Extra:
3 rows in set (0.003 sec)
```

兩種輸出方式會顯示的東西幾乎都相同，只差於格式的不同而已，可以依照自己喜歡的格式來選擇表示方式。

更多的Alter Table:https://mariadb.com/kb/en/library/alter-table/

更多可以SHOW的東西:https://mariadb.com/kb/en/library/show/

### 其之二　刪除

