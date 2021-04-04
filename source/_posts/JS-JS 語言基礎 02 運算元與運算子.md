---
title: JS-語言基礎 02 運算元與運算子
date:
tags: Javascript
category: Javascript
---


## JS 語言基礎 02 運算元與運算子

下圖中 1, 2 的部分是運算元，(+)就是運算子，整段式子為運算式

![](https://i.imgur.com/F9oedTH.png)

### 比較運算子介紹 大於小於.與等於screenflow

這邊的觀念比較直覺只要內容是正確的就顯示true反之則顯示false

![](https://i.imgur.com/EwkmXyu.png)


### 比較運算子第二部分 三個等於與兩個等於 有什麼不一樣

* 一個等於是指派賦值運算子

![](https://i.imgur.com/4rFvd13.png)


* 兩個等於不是嚴格的比較

所以下圖就算是型別不同還是會判斷成這樣

![](https://i.imgur.com/qx46t5f.png)

* 三個等於是嚴格的比較

實務中也比較常使用

![](https://i.imgur.com/wkiL9kW.png)


### 算數運算子 加減乘除

這邊觀念比較簡單
![](https://i.imgur.com/8tsDdJx.png)

### 算數運算子 餘數與被除數

這邊觀念比較簡單

(%)這個運算子可以計算出餘數
![](https://i.imgur.com/uZ2rxFD.png)


### 邏輯運算子 AND (&&) 與 OR(||)

(||)

只要有一個是true就是true

![](https://i.imgur.com/0x5Fr9b.png)

(&&)

兩邊必須一樣才是true

![](https://i.imgur.com/q92vvGV.png)
![](https://i.imgur.com/IaaX9lR.png)


進階的例子:

就算前面是false但是因為是(||)

```javascript=
(3==2) || true

=>true
```
因為&&這個運算符必須兩個都跑過所以會跑到第二個

```javascript=
x = 5
y =2

(x-y) && (y-1)

=> 1
```
左邊如果是false會直接返回false
![](https://i.imgur.com/SN7fByu.png)


如果是(||)就會左邊的跑完就出結果

```javascript=
x = 5
y =2

(x-y) || (y-1)

=> 1
```

這邊卻會繼續執行是比較不一樣的地方

![](https://i.imgur.com/nRZaUGG.png)

或等於 (||=)

![](https://i.imgur.com/X6EedzQ.png)

如果有預設值則跑預設值的結果

![](https://i.imgur.com/AqAlpQS.png)


### 邏輯運算子 NOT (!)

不等於!!

![](https://i.imgur.com/gWqzZXN.png)


### 三元運算子 

這句話很好的解釋了三元運算子的運算式
![](https://i.imgur.com/I1Tg8LV.png)

如果1>=3 我就印出a 不然我就印出b

明顯問句是1不大於等於3錯得所以印出b

![](https://i.imgur.com/YEOuI5J.png)

其實三元運算子實際上長這樣:
![](https://i.imgur.com/3irInfK.png)

賦值運算子與次方(+= 系列)

### 賦值運算子與次方(+= 系列)


這邊解釋各種加減乘除=的用法



![](https://i.imgur.com/YXFU62o.png)
![](https://i.imgur.com/tYtlRg0.png)