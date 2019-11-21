# 這裡將會教學建立，操作表單/Table的方法

這裡將會教學一些 `Table` 的建立方法和一些小知識

## 第一步建立 Table

首先我們需要登入到 MariaDB 內，所以有按照前面的教學步驟的話，開啟 Terminal 輸入

```
mysql -u 你的使用者名稱 password
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

可以看到 `MariaDB [(none)]` 裡面已經被改變為 `MariaDB [test]` ，表示已經成功地更改成使用 `test`的
資料庫了

接著我們可以開始使用 `CREATE TABLE` 的指令了，我們可以參考官方的 Knowledge Base 有提供的寫法

```
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    (create_definition,...) [table_options    ]... [partition_options]
```

以中文表示為

```
建立 [或 取代] [作為暫存表] 表單 [如果不存在的話] 表單名稱
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

再來介紹的是表單的設定及選項，我們設定支援的儲存引擎為`InnoDB`，其實還有更多不同的儲存引擎，礙於文章會變得又臭又
長的關系，我們交由其他的大神介紹，然後我們設定編碼方式為`utf8`，這是很常見的編碼方式，要是出來的資料變成亂碼的話
可以試著用`ALERT TABLE`指令將編碼方式變換為`utf8`，說不定就能解決了，當然還有更多的表單設定和不同的自訂選項，有
興趣依然可以藉著官方的文件來知道更多的自訂方法。

儲存引擎介紹連結:https://ssorc.tw/663

`table_options` 連結:https://mariadb.com/kb/en/library/create-table/#table-options

`PARTITION BY RANGE (id)`的意思則是以我們的 `id` 來分區，我們分類出 `less_than_fifty` 的區域，以`id`這個欄位的值來分類
只要`id`的值小於50就會被歸類這個分區，這也只是其中一種分區方法，詳細的可以參考接下來提供的文章，但請注意你如果使用了partition_options的方法，在做表單的 `DELETE` `INSERT` `UPDATE` 等更新資料的方法時語法會有些許的改變，要注意使用。

更詳細關於PARTITION的方法介紹:https://peterli.website/那些在MySQL上的分區方式/

MariaDB 的其他 `PARTITION BY` 寫法:https://mariadb.com/kb/en/library/create-table/#partitions

## 操控表單

### 