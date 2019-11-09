# 這裡是 MariaDB 的簡易建置教學

如你所見這裡是個教你怎麼建置一個簡單的資料庫

+ ![第一步　開啟你的 Terminal 登入](https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/tree/master/%E6%91%B8%E5%93%A9%E9%9B%85%E4%BD%8E%E9%80%BC%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8#%E7%AC%AC%E4%B8%80%E6%AD%A5%E9%96%8B%E5%95%9F%E4%BD%A0%E7%9A%84-terminal-%E7%99%BB%E5%85%A5)

+ ![第二步　建立使用者]

## 第一步　開啟你的 Terminal 登入

我會在最下面教學一下 `Command Line` 的極簡運作方式

如果沒興趣的人可以完全的跳過沒差
~~個人覺得不會用 `Command Line` 不能叫會寫程式就是了~~

如果是依照上個安裝教學的人，且成功的使用了
```mysql -V```
的這條指令

### 哈哈　壞小孩出現

```'mysql' is not recognized as an internal or external command,operable program or batch file.```

這種錯誤了吧

### 給不從頭開始看的壞小孩連結

https://ppt.cc/fKXecx

那你現在可以在任何的地方按下你的 `Win+R`

`Win` 是 `Ctrl` 跟 `Alt` 夾起來的辣個按鍵，筆電鍵盤可能是 `fn` 跟 `Alt` 夾起來的辣個按鍵

輸入 `cmd` 開啟 `Terminal` 或者使用 `powershell` 也可以

輸入

```
mysql -uroot -p你的密碼 
或者
_______________________
mysql -u root -p
Enter password:你的密碼
```

兩者皆可，那為什麼兩者皆可呢?

你可以輸入`--help`指令來找到為什麼

```
mysql --help
```

你可以看到

```
-p, --password[=name]
    Password to use when connecting to server. If password is 
    not given it's asked from the tty.
再往下拉
-u, --user=name     User for login if not current user.
```
所以你的指令也可以寫成
```
 mysql --user=root --password=你的密碼
```

那這時候就有疑問了

`我每次都要這樣打 --help 來找我要什麼嗎?`

本魯教你們一個小秘訣 https://www.google.com/

本魯知道不是每個人的英文都嚇嚇叫

所以只能推薦 Google 大神教你們了**我的能力很有限TAT**

再輸入完成後，基本上可以看到

```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 10
Server version: 10.4.8-MariaDB mariadb.org binary distribution

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

MariaDB [(none)]>
```

恭喜你/妳成功的登入囉ヽ(✿ﾟ▽ﾟ)ノ

### 妳不想看到的兩種例外狀況處理法

#### 其之一　帳號密碼錯了

若出現了

```ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: YES)```

會有很多種問題，但最基本的問題都是打錯帳號密碼

如果沒有的話請參考
http://mustgeorge.blogspot.com/2011/11/mysql-error-1045-28000-using-password.html

#### 其之二　Server不知為啥沒開

若出現了

```ERROR 2002 (HY000): Can't connect to MySQL server on 'localhost' (10061)```

有可能是妳的 MariaDB `Service` 不知道為啥關掉了

這時候你就要啟用他

使用 `Administration` 的權限去開啟 Terminal

按下你的 `Win` + `R`

輸入 cmd 或者 powershell 

並且按下 `Ctrl` + `Shift` + `Enter` 會獲得使用 `Administration` 權限的 Terminal

輸入

```
net start 你的 Service 名子
```

`Service` 名子就是基於上個教學提到的

例如:
![image](
    https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/%E6%91%B8%E5%93%A9%E9%9B%85%E4%BD%8E%E9%80%BC%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/pic1.jpg
)

那你的指令就會像這樣:
![image](
    https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/%E6%91%B8%E5%93%A9%E9%9B%85%E4%BD%8E%E9%80%BC%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/pic2.jpg
)

可以按下 `Ctrl` + `Alt` + `Delete` ，選擇工作管理員可以看到如下:
![image](
    https://github.com/qazwsx08ghj/MariaDB-install-to-uninstall-tutorial/blob/master/%E6%91%B8%E5%93%A9%E9%9B%85%E4%BD%8E%E9%80%BC%E5%BB%BA%E7%BD%AE%E6%95%99%E5%AD%B8/%E6%88%91%E6%89%8D%E6%B2%92%E6%94%BE%E5%9C%96%E7%89%87%E5%9C%A8%E9%80%99%E5%91%A2/Pic3.jpg
)

再重新登入一次或許就能成功囉!

## 第二步　建立使用者