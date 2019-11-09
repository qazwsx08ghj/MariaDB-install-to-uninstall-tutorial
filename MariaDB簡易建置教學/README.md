# 這裡是 MariaDB 的簡易建置教學

如你所見這裡是個教你怎麼建置一個簡單的資料庫

+ [第一步　開啟你的 Terminal 登入](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%B8%80%E6%AD%A5%E9%96%8B%E5%95%9F-terminal-%E7%99%BB%E5%85%A5)

+ [第二步　建立使用者](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%BA%8C%E6%AD%A5%E5%BB%BA%E7%AB%8B%E4%BD%BF%E7%94%A8%E8%80%85)

+ [第三步　讓使用者有權限](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%B8%89%E6%AD%A5%E8%AE%93%E4%BD%BF%E7%94%A8%E8%80%85%E6%9C%89%E6%AC%8A%E9%99%90)

+ [第四步　建立資料庫，使用資料庫](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E5%9B%9B%E6%AD%A5%E5%BB%BA%E7%AB%8B%E8%B3%87%E6%96%99%E5%BA%AB%E4%BD%BF%E7%94%A8%E8%B3%87%E6%96%99%E5%BA%AB)

+ [第五步　Terminal 的及簡易教學區](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%BA%94%E6%AD%A5terminal-%E7%9A%84%E5%8F%8A%E7%B0%A1%E6%98%93%E6%95%99%E5%AD%B8%E5%8D%80)

## 第一步　開啟 Terminal 登入

我會在最下面教學一下 `Terminal` 的極簡介紹

如果沒興趣的人可以完全的跳過沒差
~~個人覺得不會用 `Terminal` 不能叫會寫程式就是了~~

如果是依照上個安裝教學的人，且成功的使用了
```mysql -V```
的這條指令

### 哈哈　壞小孩出現這種錯誤了吧

```'mysql' is not recognized as an internal or external command,operable program or batch file.```

### 給不從頭開始看的壞小孩連結

https://ppt.cc/fKXecx

那你現在可以在任何的地方按下 `Win` + `R`

`Win` 是 `Ctrl` 跟 `Alt` 夾起來的辣個按鍵，筆電鍵盤可能是 `fn` 跟 `Alt` 夾起來的辣個按鍵

`cmd` 開啟 `Terminal` 或者使用 `powershell` ，輸入

```
mysql -uroot -p你的密碼 
或者
_______________________
mysql -u root -p
Enter password:你的密碼
```

兩者皆可，那為什麼兩者皆可呢? 可以輸入`--help`指令來找到為什麼

```
mysql --help
```

如下可以找到

```
-p, --password[=name]
    Password to use when connecting to server. If password is 
    not given it's asked from the tty.
    
-u, --user=name     User for login if not current user.
```
所以指令也可以寫成
```
 mysql --user=root --password=你的密碼
```

那這時候就有疑問了 `我每次都要這樣打 --help 來找我要什麼嗎?`

本魯教你們一個小秘訣 https://www.google.com/

本魯知道不是每個人的英文都嚇嚇叫，所以只能推薦 Google 大神教了**我的能力很有限TAT**

輸入完成後，基本上可以看到

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

恭喜成功的登入囉ヽ(✿ﾟ▽ﾟ)ノ

### 妳不想看到的兩種例外狀況處理法

#### 其之一　帳號密碼錯了

若出現了

```ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)```

會有很多種問題，但最基本的問題都是打錯帳號密碼，如果沒有的話請參考

http://mustgeorge.blogspot.com/2011/11/mysql-error-1045-28000-using-password.html

#### 其之二　Server不知為啥沒開

若出現了

```ERROR 2002 (HY000): Can't connect to MySQL server on 'localhost' (10061)```

有可能是妳的 MariaDB `Service` 不知道為啥關掉了，這時候就要啟用他

使用 `Administration` 的權限去開啟 Terminal

按下 `Win` + `R`，輸入 cmd 或者 powershell
並且按下 `Ctrl` + `Shift` + `Enter` 會獲得使用 `Administration` 權限的 Terminal 輸入

```
net start 你的 Service 名子
```

`Service` 名子就是基於上個教學提到的，例如:

![image](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/pic1.jpg
)

那指令就會像這樣:

![image](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/pic2.jpg
)

可以按下 `Ctrl` + `Alt` + `Delete` ，選擇工作管理員可以看到如下:

![image](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/Pic3.jpg
)

再重新登入一次或許就能成功囉!

## 第二步　建立使用者

使用 資料庫管理系統當然要學會怎麼增加使用者R

### 其之一　以 Root 權限登入到 MariaDB 內

如同上面的教學，開啟 Terminal 輸入

```
mysql -u root -p你的密碼
或者
mysql -u root -p
Enter Password:你的密碼
```
會看到登入的畫面，接著輸入建立使用者的指令 `CREATE USER`
例如:

```
MariaDB [(none)]>CREATE USER '文香醬老公'@'localhost' IDENTIFIED BY '123';
Query OK, 0 rows affected (0.007 sec)
```

``` CREATE USER '文香醬老公'@'localhost' IDENTIFIED BY '123' ```

應該會有問題的是這個部分的指令`'localhost' IDENTIFIED BY '123'`

`localhost` 這個位置意思是他可以從何處來進入 Maria醬的服務

當然也可以不從 `localhost` 從其他的地方登入，詳細就交由 Maria醬的官網講解了

https://mariadb.com/kb/en/library/create-user/#host-name-component

再來是 ` IDENTIFIED BY '123'`

這句就是， Maria醬該怎麼知道這個人不是陌生人呢?

所以就以123這個密碼來識別這個人是不是文香醬的老公喔

綜合上述這句的意思就是 

```建立 使用者 '文香醬老公'@可以自'localhost'登入 怎麼分辨是不是文香醬的老公呢 由 123 這個密碼```

這時候聰明的你會想提問:這是怎麼來的，和這些參數有什麼意義?

### **這部分完完全全可以跳過，但是我會恨你(X**

+ [我要當壞小孩的第三步連結](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/MariaDB%E7%B0%A1%E6%98%93%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%B8%89%E6%AD%A5%E8%AE%93%E4%BD%BF%E7%94%A8%E8%80%85%E6%9C%89%E6%AC%8A%E9%99%90)

### 其之二　我要怎麼知道我可以用啥

我們來看登入的時候 Maria醬告訴了我們什麼呢?

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 8
Server version: 10.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```

`Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.`

沒錯 又是看文件的時間了，幾乎所有的指令都可以由這種方式找到更多的自訂方法。
所以我就在這教如何得到更多相關的寫法信息

首先在 Terminal 輸入 `\h`例如:

```MariaDB [(none)]>\h``` 

會得到跟 Maria醬溝通的方法，但是你不會看到 `CREATE USER` 類似的寫法或者他該含有什麼參數，什麼指令的寫法
看到最後一句會發現

```For server side help, type 'help contents'```

因為輸入 `\h` 只會得到跟 Maria醬溝通的方法，如果要獲得使用 Maria醬服務的方法，必須輸入 Maria醬提供的 `help contents`
例如:

```
MariaDB [(none)]> help contents
You asked for help about help category: "Contents"
For more information, type 'help <item>', where <item> is one of the following
categories:
   Account Management
   Administration
   Compound Statements
   Data Definition
   Data Manipulation
   Data Types
   Functions
   Functions and Modifiers for Use with GROUP BY
   Geographic Features
   Help Metadata
   Language Structure
   Optimization and Indexes
   Plugins
   Procedures
   Sequences
   Storage Engines
   Table Maintenance
   Transactions
   User-Defined Functions
   Utility
```

這時候 Maria醬提供的服務就會顯示出來啦
因為我們要使用的是建立使用者，建立使用者跟使用帳戶的管理相關，所以我們要用到的是 `Account Management`

Maria醬也貼心的說了這句 `For more information, type 'help <item>', where <item> is one of the following`

我們就可以知道，要知道更多這個服務的資訊我們可以輸入 `help 我想查詢的服務`
例如:

```MariaDB [(none)]> help Account Management```

```
MariaDB [(none)]> help Account Management
You asked for help about help category: "Account Management"
For more information, type 'help <item>', where <item> is one of the following
topics:
   ALTER USER
   Account Locking
   Authentication from MariaDB 10.4
   CREATE ROLE
   CREATE USER
   DROP ROLE
   DROP USER
   GRANT
   RENAME USER
   REVOKE
   Roles Overview
   SET DEFAULT ROLE
   SET PASSWORD
   SET ROLE
   User Password Expiry
```

然後以上面所提過的邏輯，我們可以知道我們要使用的是建立使用者 `CREATE USER`
所以就可以輸入 `help CREATE USER`
例如:

```
MariaDB [(none)]> help CREATE USER
More imformations
```

就可以得到更多的相關於 `CREATE USER`的信息囉 (*´▽`*)，上述的方法都是在完完全全Google不到的情況下可以自救的辦法
~~如同本魯這可撥小孩~~

## 第三步　讓使用者有權限

好的，使用者有了，那我們來開始建立使用者的權限吧!

### 其之一　GRANT 指令

在 Terminal 裡面輸入 `GRANT`，我們要讓這個使用者有所有的權限在所有的DB裡面
那我們就這樣子寫我們的指令
例如:

```
GRANT ALL PRIVILEGES ON *.* TO '文香醬老公'@'localhost' ;
```

我們接著解釋這行指令發生了什麼事情

`GRANT ALL PRIVILEGES ON *.* TO '文香醬老公'@'localhost' ;`

`ALL PRIVILEGES ON *.*`

所謂的 `*` 就如同在SQL裡面 `Select *` 一般，選擇所有的資料庫。

`.` 則可以翻譯為這個資料庫的哪一些 `Table` ，我這個例子也是使用 `*` ，表示選擇所有的 `Table`
所以這行指令的白話意思就是指

```給予 所有可行使的權限(例如:新增，修改等權限) 在 所有的資料庫中 裡的 所有的表單 將這個權限給予 '文香醬老公'@'localhost'```

如果對 `ALL PRIVILEGES` 還可以改成別的東西有興趣，想知道更多的內容都在
https://mariadb.com/kb/en/library/grant/#global-privileges

就可以知道更多可以分別給予的權限了(*´▽`*)

接著就輸入離開 `\q`
在使用新的登入帳戶，也就是剛剛 `CREATE USER` 的帳戶

```
mysql -u 設立的帳戶名稱 -p
Enter Password:剛剛所設立的密碼
```
例如:

```
C:\Users\default_user>mysql -u 文香醬老公 -p
Enter password: ***
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

## 第四步　建立資料庫，使用資料庫

現在使用者有了，使用者也有權限了，那我們就來建立和使用資料庫吧

### 其之一　建立，找尋，刪除，修改(CRUD)資料庫

接下來就是大家口中的建立資料庫了，在這裡只會介紹很簡易的寫法，細節或者要特別設定的寫法都可以用Google找到

#### **一小節　建立**

在 Terminal 內輸入

```CREATE DATABASE DATABASE_NAME;```

這是最基礎的語法，也是最基本的語法，在 MariaDB 內也可以寫

```CREATE DATABASE IF NOT EXISTS DATABASE_NAME;```

他會先判斷有沒有存在這個名子的資料庫，再來創建
詳細 https://mariadb.com/kb/en/library/create-database/

#### **二小節　找尋**

找尋的語言也很直覺，只需要

```SHOW DATABASES;```

當然也可以

```SHOW DATABASES LIKE 'm%';```

來找到開頭為字母 `m` 的資料庫
詳細 https://mariadb.com/kb/en/library/show-databases/

#### **三小節　刪除**

刪除資料庫也只需要簡單的

```DROP DATABAS DATABASE_NAME;```

依照上面的邏輯一定也可以寫成

```DROP DATABASE IF EXISTS DATABASE_NAME;```

詳細 https://mariadb.com/kb/en/library/drop-database/

#### **四小節　修改**

可以修改資料庫的編碼方式，名稱，排序方式等等功能
例如:

```ALTER DATABASE DATABASE_NAME CHARACTER SET = 'utf8';```

詳細 https://mariadb.com/kb/en/library/alter-database/

## **注意!!　由於 Terminal 實在有太多的應用以及方法，所以只教觀念跟簡易用法**
## 第五步　Terminal 的及簡易教學區

這邊會教到 windows 中 `CMD` 及 `powershell` 的簡單範例及差別，以及簡單的語法範例

### 第一步　什麼是 CMD 什麼是 powershell

#### 一小節　CMD

`cmd` 為 windows 中可以使用文字介面來操控作業系統的工具，基本上可以使用 `Win` + `R` 輸入 `cmd` 來開啟
接著透過 `cmd` 來操作電腦中的檔案

例如:
在 `Python` 有寫入 `Path` 的情況下使用 `Win` + `R` 輸入 `cmd` 來開啟 Terminal
是可以使用 `cmd` 做到簡單撰寫 `Python` 檔案的
windows 的例子基本上預設在

```C:\Users\user name\Desktop```
在 Terminal 中輸入

```
C:\Users\bbb65>cd Desktop #開啟desktop的資料夾

C:\Users\bbb65\Desktop>mkdir Test_dir #建立一個名為 "Test_dir" 資料夾

C:\Users\bbb65\Desktop>cd Test_dir #開啟 Test_dir 的資料夾

C:\Users\bbb65\Desktop\Test_dir>copy con TestFile.py #複製一個你打出的指令輸出成你指定的檔案名稱及檔案型態
print("hello word")
        1 file(s) copied.

C:\Users\bbb65\Desktop\Test_dir>DIR #輸入DIR來確認檔案的型態及確認位置
 Volume in drive C has no label.
 Volume Serial Number is 6ECF-195F

 Directory of C:\Users\bbb65\Desktop\Test_dir

2019/11/10  上午 01:51    <DIR>          .
2019/11/10  上午 01:51    <DIR>          ..
2019/11/10  上午 01:51                21 TestFile.py
               1 File(s)             21 bytes
               2 Dir(s)  13,173,456,896 bytes free

C:\Users\bbb65\Desktop\Test_dir>python TestFile.py #呼叫 Python.exe 來執行你建立的TestFile.py
hello word
```

還有更多的玩法，但本魯實在是沒有辦法在這裡一一的介紹~~這要教到會都可以開一個禮拜兩節的選修了~~
所以就在這放上教學文章讓有興趣的人去學習了
https://lnpcd.blogspot.com/2012/09/00.html

#### 二小節　PowerShell

`PowerShell` 可以當作是功能相當之強大的 `CMD`

你甚至可以用它來寫 script(腳本) 直接執行都不是問題

例如:
```
$Excel = New-Object -comobject Excel.Application #建立一個變數使用Excel
$Excel.Visible = $True #讓這個Excel是可見的
$Workbook = $Excel.Workbooks.Add() #開啟一個Excell 
```

在電腦中有Excell的情況下是真的可以如此開啟一個Excell來繼續執行其他的步驟的
有很多東西都可以使用 PowerShell 來達成，本魯自己也是偏向喜歡使用 Powershell的
更多詳細的東西都在 Microsoft 的 Powershell 裡可以找到
對這兩個都有興趣的話可以先試著看看 Powershell 功能強大也可以玩很多東西

https://docs.microsoft.com/zh-tw/powershell/

### 本魯的採坑日記

基本上這個章節不會有什麼太嚴重的問題，在不同的 `RDBMS` 也就是關聯性資料庫管理系統
語法會稍微的不同，只有這點需要稍微注意
 `cmd` 及 `powershell` 基本上都是走寫程式這條路都會碰到的，如果有要走這條路鼓勵大家多學一些 d(`･∀･)b
本魯就是在邊學邊會的 ~~邊踩坑邊會的~~
希望大家看了我的教學多少會了一些東西 ㄅ噗

(*´∀`)~♥
