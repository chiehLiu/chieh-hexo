---
title: HTML-簡介
date:
tags: HTML
category: HTML
---

#  HTML簡介

---
tags: HTML CSS relate
---

###### tags: `HTML, CSS`


## 他的程式架構

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hello Pages!!</title>
</head>
<body>
    <h1>Hello pages!!</h1>
</body>
</html>

```


## !DOCTYPE html 

這個表示它們的類型

是HTML5，也是現行的大多數的瀏覽器都相容的格式


## html 

被稱為根元素，基本上會把整個網站的內容包在裡面

## head 

網頁的描述 EX.字元集、標題、縮圖

## title 

網頁的標題

## charset 

一個資料格式

## body 

網頁瀏覽器的眼前的內容，文字、圖片、影片都是


---

## headings 

像是h1~h2~h3(數字越小字體越大)這些東西都是，有著各種粗體跟大小的字體會讓文字顯示在網頁上

`<h1></h1>`

![](https://i.imgur.com/XeigVbl.png)


## paragarph(block元素) 

段落，每個段落都會有個空間存在，他的文字不會都黏在一起

`<P> </P>`

![](https://i.imgur.com/pUvlW87.png)




--------------




## img  

這是代表圖片的標籤 
如果中間也沒有文字的話可以為了節省時間變成這樣寫


`<img src="裡面可以放入圖片的位置/>`

```
這個是正常寫法
<img src="裡面可以放入圖片的位置></img>
```

## ul、li 

代表列表 

```
<UL>
    <li>中間輸入內容</li>
    <li>中間輸入內容</li>
</UL>
```

## a 

這個標籤可以代表網頁的超連結

`<a href=放入超連結的網址>名稱如.GOOGLE</a>`


## table 
代表表格 tr 裡面是那列的內容，td表示那一欄的內容


border="1" 這個屬性會讓格線出現
width="400" 這個屬性表示表格寬度
cellpadding="5" 這個屬性代表表格框框內容的填塞(可以讓內容不那麼擁擠)

```
<table border="1" width="400" cellpadding="5">
    <tr>這裡代表表格的第一列
        <td>這邊是第一欄</td>
    </tr>
    
    <tr>這裡代表表格的第二列
        <td>這邊是第一欄</td>
    </tr>
    
```

--------

## b 

這個標籤的功能是讓文字變成粗體字

`<b>中間放入要變粗體字的內容</b>`

u 這個標籤的功能是給文字加入底線

`<u>中間放入要加入底線的內容</u>`

兩個功能合併的話可以又粗體又底線

`<u><b>中間放入要加入又粗體又底線的內容</b></u>`

-------


## hr 

這個標籤的功能是加入斜線區格

因為這個功能常常中間是沒有文字的，就可以把後面那個`</hr>`整個去掉變成`<hr/>`
這樣可以代替並節省時間

`<hr></hr>`



