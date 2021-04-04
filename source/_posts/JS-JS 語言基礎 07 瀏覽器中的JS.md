---
title: JS-語言基礎 07 瀏覽器中的JS
date:
tags: Javascript
category: Javascript
---


## JS 語言基礎 07 瀏覽器中的JS

### DOM 與樹狀結構

甚麼是DOM

* Document Object Model 文件物件模型
* HTML的格式須遵守W3C的規範
* 而遵守W3C的HTML檔案可以被解成城DOM樹(Tree)

解釋DOM樹(Tree)
![](https://i.imgur.com/UTb1iPm.png)

文件物件模型的意義:
![](https://i.imgur.com/9QAkMzK.png)


### 在瀏覽器觀察 DOM Tree 與 document 物件

在開發者瀏覽器打上document後:

會顯現出上方文件物件模型的意義

![](https://i.imgur.com/9QAkMzK.png)

![](https://i.imgur.com/99I45nJ.png)


### 什麼是 API 


* Application Programming Interface
* 應用程式 編程 介面
* 透過寫程式來跟網頁上的功能(像是email google MAP搜尋等等)溝通



### 瀏覽 document 物件 API 文件

[document Web API](https://developer.mozilla.org/zh-TW/docs/Web/API/document)

[W3Cschool Web API](https://www.w3schools.com/js/js_api_intro.asp)


### BOM 與 window 物件

* Browser Object Model 瀏覽器物件模型
* 就是 window 物件 就是整個瀏覽器所以其實不用打出來也可以有效果

![](https://i.imgur.com/6dViT6V.png)


![](https://i.imgur.com/i6LTlLd.png)

#### Location:

![](https://i.imgur.com/3rsiA8V.png)

#### History back() , go()

back()

可以直接回到上一頁

go()必須加數字在參數的地方

可以去下一頁