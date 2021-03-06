# 如你所見，這是一個 MariaDB 的安裝教學

我將會在這裡示範 MariaDB 的安裝方法

## 第一步，下載你的 MariaDB


~~打開你的瀏覽器搜尋如何安裝 MariaDB~~

放下你手中的掃把，我會認真教的

首先到 https://downloads.mariadb.org/mariadb/ 下載

基本上都是用新的 Series

按進去往下看會發現 mariadb-版本號-winx64.msi 按連結載下來

如果連 Dowload 都看不懂那還是放棄ㄅ，這個東西太難了

等到下載完成就可以開始安裝 MariaDB 了


## 第二步，安裝你的 MariaDB


相信到這個地方，聰明的你不用看這邊都可以解決了。

但為了讓更嚴謹的人看懂到底是發生了什摸是。

我決定在這裡一步一步的教學怎麼安裝


### 其之一　打勾


就是字面上的意思，同意公司的規定之類的，基本上不用管他

沒用 MariaDB 賺錢就不用理了，也不會有人想看 ~~被告了才會知道(́◉◞౪◟◉‵)~~

~~ 我是不知道裡面有沒有賣身契拉~~

![image](That-picture/pic1.jpg)


### 其之二　選擇你要安裝啥


請注意!!

當你覺得你跟我一樣菜鼻八的時候請不要亂動這裡面的東西(´_ゝ`)

![image](That-picture/pic2.jpg)


### 其之三　設定最高的? 最上端的? 使用者密碼


第一格為輸入密碼

再來為確認輸入的密碼

我本人是沒多在勾額外的東西，有興趣可以密我來討論下面那兩個是幹啥的

![image](That-picture/pic3.jpg)


### 其之四　設定 ServerName Port BufferPool PageSize

![image](That-picture/pic4.jpg)

第一個會關於你的 Server 會是啥名子，基本上我們在安裝時都會維持預設，也不會隨意去改動

再來是 `Port` 

要設定這個就要先了解什麼是 `Port` https://zh.wikipedia.org/wiki/%E9%80%9A%E8%A8%8A%E5%9F%A0

維基百科基本上不講人話


以承濬語來解釋就是你要播這個電話才可以跟這個人溝通

我們要設定這個電話 `port` 讓寫的程式能跟 MariaDB 溝通

基本上基底吃 MySQL Server 的 `MariaDB` 跟 `MySQL` 預設值就如同圖片內的 `3306`


`BufferPool`基本上就是大了沒差，小了有問題，會直接影響到資料庫讀取進出的速度

但本肥宅玩算不少應用預設值都還沒問題，有興趣的話可以看官方文件的解釋

https://mariadb.com/kb/en/library/innodb-buffer-pool/


最後就是 `PageSize` 基本上不是很重要

我也沒很在意這個東，詳細可以參考這個來源

https://mariadb.com/kb/en/library/innodb-limitations/


### 其之五　按按按


最後這個有勾沒勾都沒關係，基本上就是想要你分享你的電腦環境，如果出了種種問題

錯誤訊息會傳給 MariaDB 那邊

![image](That-picture/pic5.jpg)


### 其之六 加入Path


如果你在啥都沒動的情況下按 是是是是是 的結束了你的安裝流程

那你就將你的 MariaDB 在 PC Windows 的預設路徑大概會類似

```
C:\Program Files\MariaDB 10.4\bin
```

然後對著本機按右鍵

![image](That-picture/pic6.jpg)

接著按內容->進階設定->進階->環境變數->在系統變數欄中找到`Path`

![image](That-picture/pic7.jpg)

再點個兩下進入，找空白的地方貼上 `MariaDB` 裏頭含有 `mysql.exe` 的資料夾路徑

![image](That-picture/pic8.jpg)

這樣就可以用 Terminal 來確認 MariaDB 有沒有安裝成功了

用 `Win+S` 開啟查詢，輸入 `cmd` 會跳出命令提示字元的方框，也就是 Terminal

`Win` 就是 `Ctrl` 跟 `Alt` 夾起來的那個按鍵，筆電鍵盤可能是 `fn` 跟 `Alt` 夾起來的

或者輸入 `powershell` 也可以，但我沒印象是要自己加入path還是原生會加入

本魯覺得 `powershell` 我比較愛用

接著輸入

```mysql -V```

出現了安裝版本就代表整個安裝成功了(灑花

#### 可撥肥宅的踩坑筆記


如果你跟我一樣是個三心二意的全婆俠，左擁瑪麗亞，右抱買西擴，中間 Xampp 建伺服器

那你應該要看到這裡的可撥肥宅踩坑記

基本上 MySQL 跟 MariaDB 的預設值 `Port` 會是一樣的，都是 `3306` 的 `Port`

所以呢 你只要改其中一個改成 `3307` 的 `Port` 就可以完成了

如果你用的是 Xampp 呢

你就不要開 MySQL 那行就解決了

##### 阿不是阿　我就很基掰很想用Xampp裡面的MySQL阿

改掉 `my.ini` 裏頭的 `Port` 別跟 MariaDB 的 `port` 互相衝突就好了

也要將 `Apache` -> `config.inc.php` 裏頭的 `Port` 改成跟 `my.ini` 相同就行惹

