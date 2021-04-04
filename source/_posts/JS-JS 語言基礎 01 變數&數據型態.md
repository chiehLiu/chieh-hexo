---
title: JS-語言基礎 01 變數&數據型態
date:
tags: Javascript
category: Javascript
---




## JS 語言基礎 01 變數&數據型態


### 變數variable

變數在使用前會被宣告

![](https://i.imgur.com/Jogff3g.png)


如果像一開始的那個只有宣告的變數的話

他會跑出來的結果會是undefined

```javascript=
var x;

console.log(x);
```
當給他value的時候就能正常印出數字摟!

```javascript=
var y = 10;

console.log(y);
```

#### 變數是值的符號名稱，可以透過名稱來獲得值的引用

var x =10 並不是把10丟給X的意思

而是透過變數 var x = 10 名稱來獲得值的引用(reference)

![](https://i.imgur.com/ZRTKQ9S.png)

### 第一種型別 Number

* 整數integer
* 浮點數float

JS中不會區分這兩者都只會顯示"Number"

![](https://i.imgur.com/pwV5N3E.png)

Python中這兩者就有區別瞜!

![](https://i.imgur.com/5NBqH3i.png)


#### 浮點數的陷阱

浮點數可能會造成誤差

![](https://i.imgur.com/R3cvdo1.png)


![](https://i.imgur.com/pnwCyTs.png)


### 第二種資料型別 字串 String

宣告方法:

* 單引號
* 雙引號
* 單雙引號不可以混用
* ES6可以使用`(``)`來宣告

![](https://i.imgur.com/PwREY9M.png)

字串的串接
![](https://i.imgur.com/m6dinYH.png)


### 第三種資料型態 Boolean 布林值

![](https://i.imgur.com/wXpRpPV.png)

使用Boolean來做判斷流程是他很重要的作用

![](https://i.imgur.com/NVksCqE.png)


### 第四、第五種資料型別 null 空值 與 undefined 未定義


* undefined 未定義

宣告變數卻沒有指派時候印出x會得到

undefined因為值還沒有指派

型別也是undefined

![](https://i.imgur.com/9IWUrwW.png)


* null 空值

指派一個空值給變數

![](https://i.imgur.com/oyPNi5x.png)