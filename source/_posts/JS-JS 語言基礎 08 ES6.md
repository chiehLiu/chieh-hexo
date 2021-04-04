---
title: JS-語言基礎 08 ES6
date:
tags: Javascript
category: Javascript
---

## JS 語言基礎 08 ES6

### 01 let 與 const 作用域改變成大括號會怎麼樣


let與const 對比舊時代的var


1.作用域的改變
* var=> function
* let,const =>{}


#### Example1:

```javascript=
var i = 0;

for (var i = 0; i < 10; i++) {
    console.log(`迴圈跑第${i}次`);
}

console.log(i);
```
很明顯的地方是外面的var i = 0被裡面的迴圈汙染到所以傳回來的結果是10
![](https://i.imgur.com/wexESY7.png)

所以改成let做操作時因為其作用域是{}因此沒有汙染到外面來

```javascript=
let i = 0;

for (let i = 0; i < 10; i++) {
    console.log(`迴圈跑第${i}次`);
}

console.log(i);
```
![](https://i.imgur.com/za2DaSb.png)

#### Example2:

用在判斷式上面更明顯使用var來操作的話這邊的結果是會直接跑進判斷式中

```javascript=
var x = 1;
if (x === 1) {
    var x = 5;
} else {
    var x = 10
}

console.log(x);
```
印出結果為5
![](https://i.imgur.com/ocAUxF2.png)

全面改成使用let

```javascript=
let x = 1;
if (x === 1) {
    let x = 5;
} else {
    let x = 10
}

console.log(x);
```

印出結果就沒有被汙染瞜

![](https://i.imgur.com/BCKG9mX.png)


#### Example3:

使用大括號的效果跟IFEE一樣

```javascript=
//IIFE立即函式
(function($){
var x = 1;
})(jQuery);


{let x =1;}
```


#### 支援度

* chrome已經全面支援使用
* 但是IE部分還沒，所以舊的寫法還是需要了解
* 使用babel 做編譯 ES6 =>ES5


### 02 const 常數與注意事項

const 定義了之後不可以改變的變數


![](https://i.imgur.com/V3Z9eDz.png)


#### 重要例外

當常數定義物件的時候裡面的值是可以改變的並不會報錯


![](https://i.imgur.com/PkrU1Ti.png)


但是如果你在複寫一次物件就會出問題摟!
![](https://i.imgur.com/B4TwpLl.png)


### 03 解構賦值陣列與物件為什麼可以這樣寫

#### 陣列的解構賦值

![](https://i.imgur.com/gKme5TF.png)

解構賦值的其中一種用法:讓賦值變簡潔
![](https://i.imgur.com/FdPG2N1.png)


#### 物件的的解構賦值

前面let的部分其實是縮寫

`let{a:a,b:a}`是原本的樣子


```javascript=
let {a,b} = {a: 111,b: 222}

console.log("a:" + a, "b:" + b);
```


### 04 for in, for of 的區別


#### for of 用來迭代可以迭代的物件

> 可以迭代的對象包含:
> Array，Map，Set，String，TypedArray，arguments

![](https://i.imgur.com/A1qG3Jv.png)

[for of -MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...of)

#### for in

> 迭代可以列舉的屬性

```javascript=
var object = {
    a: 1,
    b: 2,
    c: 3
};

function show_props(obj, objName) {
    var result = "";

    for (var prop in obj) {
        result += objName + "." + prop + " = " + obj[prop] + "\n";
    }

    return result;
}

// 前方的參數是要引入的object 後方是物件的名字
alert(show_props(object, "物件"));
```

![](https://i.imgur.com/2jQmrqW.png)


### 05 Iterator 迭代器是什麼? 如何使用


#### 可迭代協議（iterable protocol）


一個物件如果要被迭代他必須有這個屬性`[Symbol.iterator]`

而當這個物件需要被迭代的時候這個屬性的不需要引入參數的函式(下方圖片)就會被呼叫來獲得被迭代的值


```javascript=
let myStings = "123";

myStings[Symbol.iterator]();

console.log(myStings[Symbol.iterator]());
```

String Iterator
![](https://i.imgur.com/Ofzt0LW.png)


#### 迭代器協議（iterator protocol）

迭代器協議定義了一個標準的方式來產生迭代的有限或是無限的值並且都會回傳一個值，而next()就是一個迭代器

```javascript=
let myStings = "hello";

let iterator = myStings[Symbol.iterator]();
```
之後在chrome呼叫方法next()就可以迭代出字串摟

![](https://i.imgur.com/7gelfsm.png)

#### 迭代array

```javascript=
let myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9];

let arrayIterator = myArray[Symbol.iterator]();
```

![](https://i.imgur.com/x24qipJ.png)


### 06 for of 的使用方法

從上面解釋過迭代的原理後下方這邊的用法就清楚多了


#### for of:字串的迭代

```javascript=
let myStings = "hello";

for (let str of myStings) {
    console.log(str);
}
```

![](https://i.imgur.com/JhVcBmq.png)

#### for of 陣列的迭代

```javascript=

let myArray = [1, 2, 3, 4, 5, 6, 7, 8, 9];

for (let i of myArray) {
    console.log(i);
}
```


![](https://i.imgur.com/zm9dNdj.png)


### 07 樣板字面值Template Iterator與字串字面值String Iterator

* 使用的符號不一樣使用(\`\`\)來包裹住文字

```javascript=
let str = "123";
let str2 = `123`;
```

* 斷行

Template Iterator可以直接空格下去不需要使用跳脫字元\n

```javascript=
let str = "123 \n 123";

let str2 = `123
123`;
```

* 嵌入變數

可以直接在字串串接中放入變數

```javascript=
let name = "john";

let str2 = `my name is ${name}`;
```
ES5的寫法

```javascript=
let name = "john";

let str2 = "my name is " + name;
```

### 08 展開運算子 Spread Operator

#### 印出其值

```javascript=
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(...arr1);

```

![](https://i.imgur.com/zaP2dyN.png)


例子

數學方法Math.min()取最小值參數不能放入陣列這個時候就可以使用展開運算子

```javascript=
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(Math.min(arr1));
```

![](https://i.imgur.com/QRqoJvl.png)

這樣就可以正常使用搂!

```javascript=
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];

console.log(Math.min(...arr1)); // 印出最小值為 1 
```

#### 陣列串接

把內容物有重疊的兩個陣列構成新的陣列

```javascript=
let arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9];

let arr2 = [7, 8, 9, 10, 11, 12, 13, 14, 15];

let arr3 = [...arr1, ...arr2];
```

這樣的寫法會等於`arr1.concat(arr2)`

![](https://i.imgur.com/TPTXpLY.png)

#### 物件的串接

把內容物有重疊的屬性直接用o2取代掉，後方的新屬性會取代掉舊的屬性

```javascript=
let o1 = { a: 1, b: 2, c: 3 };
let o2 = { c: 100, d: 4 };

let o3 = { ...o1, ...o2 };
```

![](https://i.imgur.com/4UgB52N.png)


### 09 箭頭函式(1) 

怎麼樣寫會有回傳值, 怎麼樣寫不會有回傳值

有回傳值
```javascript=
const function1 = x => x+1
``` 


無回傳值
```javascript=
const function1 = x => {x+1} 
```

### 箭頭函式(2) 

call 與 this

這邊this的指向是window

```javascript=
function greet() {
  let reply = `Hi, ${this.person}`;
  console.log(this);
};
greet();
```

![](https://i.imgur.com/PeZfz24.png)


如果我們想要改變this的指向可以使用`call()`這個方法讓this去呼叫到obj裡面的屬性

```javascript=
function greet() {
  let reply = `Hi, ${this.person}`;
  console.log(reply);
}

let obj = { person: "BIll" };

greet.call(obj);
```

![](https://i.imgur.com/UWNoqdP.png)




### 箭頭函式(3) 


this 綁定的對象不再是function本身


#### 使用ES5的函式寫法

```javascript=
let obj = { person: "BIll" };

function greet() {
  let reply = `Hi, ${this.person}`;
  console.log(reply);

  setTimeout(function () {
    console.log("Hi,", this.perosn);
  },1000);
}

greet.call(obj);
```

因為function 內部的作用域會是隔開地所以是未定義(undefined)
![](https://i.imgur.com/Dl7tOZ1.png)

#### 使用ES6箭頭函式

```javascript=
let obj = { person: "BIll" };

function greet() {
  let reply = `Hi, ${this.person}`;
  console.log(reply);

  setTimeout(() => {
    console.log("Hi,", this.person);
  }, 1000);
}

greet.call(obj);
```
箭頭函式不會有作用域的隔閡所以不會影響到this，所以它是一樣吃到外面的obj
![](https://i.imgur.com/4iyrpM9.png)