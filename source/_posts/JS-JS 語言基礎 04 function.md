---
title: JS-語言基礎 04 function
date:
tags: Javascript
category: Javascript
---


## JS 語言基礎 04 function


DRY = don't repeat yourself

盡量避免重複讓他工具化就是function的目的瞜!

![](https://i.imgur.com/nHJ7rDY.png)


### 了解表達式(Expression)與陳述句(Statement)的差異


* 陳述句(Statement)

不會有值

如　if else,switch


* 表達式(Expression)

一定會有值

如 1 + 1

### 使用函式陳述式(Function Statement)與函式表達式(Function Expression)


* 函式陳述式(Function Statement)

```javascript=
function helloFunctionStatement(){
console.log('hello function statement !!!')
}

helloFunctionStatement()
```
* 函式表達式(Function Expression)

```javascript=
var helloFunctionExpression = function(){
console.log('hello function Expression !!!')
}

helloFunctionExpression()
```


* Hoisting 變數提升

它讓函式陳述式可以先呼叫函式在執行他的身體

![](https://i.imgur.com/qMf63CS.png)



函式表達式則不行呼叫函式一定要寫在身體下方

![](https://i.imgur.com/CJzxbrr.png)


### 變數能夠影響的範圍作用域( Scope )


![](https://i.imgur.com/9HZOB1r.png)

印出的結果是 

150
100

代表funciton裏面的變數不會影響到外面的

但是如果function裡面的關鍵字var 或是 let const 忘記寫了就會影響到外面的變數瞜!

![](https://i.imgur.com/ElbwThz.png)

印出的結果是 

150
150


### 全域變數與區域變數


在function內宣告的變數就是區域變數
![](https://i.imgur.com/r55q1PP.png)

不再function內的話就是全域變數可以被當作property被window使用
![](https://i.imgur.com/kXFHVro.png)

不是變數 (會被存取成屬性(property))

![](https://i.imgur.com/KJ3S0XN.png)

當包含不是變數的function被呼叫執行後這個不是變數的部分也可以被當作property被window使用瞜!

![](https://i.imgur.com/GosNh9F.png)


### 回呼函數 Callback Function - 把函數做為參數傳遞


這樣寫就可以把把函數做為參數傳遞:

當中的alert就可以改成各種方法去執行這個函式瞜
![](https://i.imgur.com/GBM4gEb.png)


### 匿名函式

下方的函式沒有名稱的部分就是匿名函式並且它只能放在回乎函式之中等待被呼叫的時候才使用

匿名的因為是因為它是預計要被傳進去的函式

![](https://i.imgur.com/ztMucl2.png)


### IIFE 立即函式

使用的理由是避免一些不必要的汙染(變數的部分)

![](https://i.imgur.com/8AbEP3T.png)


* 全名: Immediately Invoked Functions Expression
* 可以立即呼叫的函式表達式
* 表達式: expression 它會回傳值
* 使用立即函式 會立刻執行函式

![](https://i.imgur.com/x18fhcO.png)



### hoisting 變數提升

不管在哪一行做的變數都視為在第一行做宣告

```javascript=

//一開始的樣子

console.log(x);// 結果是undefined因為它實際上長這樣

----------

var x;

console.log(x);

//實際上內建提升上去變數

```


看四個console.log()的印出結果:

第一個紅色框是undefined

第二個是10

第三個是undefined

第四個是20

原樣:
![](https://i.imgur.com/kP0yVPP.png)

提升後的樣子:
![](https://i.imgur.com/zRGav1B.png)