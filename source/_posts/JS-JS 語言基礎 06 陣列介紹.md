---
title: JS-語言基礎 06 陣列介紹
date:
tags: Javascript
category: Javascript
---


## JS 語言基礎 06 陣列介紹

陣列是一種資料結構(Array)

* 物件是鍵值對(key-value pairs)
* 陣列是依照索引排序(index)的資料結構
* 不推薦陣列的內容字串跟數字混用不然會比較不好操作

通常長這樣:
![](https://i.imgur.com/s76qbA0.png)




索引的部分(index):

0,1,2的部分

![](https://i.imgur.com/RCsgGVv.png)

擷取其值[]:

![](https://i.imgur.com/2AJBh4f.png)

取陣列的長度大小 length:

![](https://i.imgur.com/OTqScAn.png)


### 陣列基本操作 pop 與 push

pop 把最後一個元素去掉

![](https://i.imgur.com/mK8tWm5.png)


push 把一個值加到最後

![](https://i.imgur.com/ik9vRMy.png)


### 陣列基本操作 替換元素 與 取得最後一個元素


替換元素:

帶入index後直接輸入要替換的值

![](https://i.imgur.com/M6EV9jy.png)

取得最後一個元素的值:

使用length取得陣列長度後減一就是最後一個值的index搂

![](https://i.imgur.com/8SDCdzk.png)

### 陣列操作 indexOf 取得元素的索引

很直接使用(.indexOf)

![](https://i.imgur.com/axNFBsm.png)


### 陣列的基本操作 切片slice 與 方法這麼多到底要怎麼記


切片slice

`陣列.slice(起始點,終點)`

切出來的值會包含起始點不包含終點

![](https://i.imgur.com/4AlzU5O.png)

![](https://i.imgur.com/2xclorT.png)


方法不死背 多巡查詢使用

## JS 語言基礎 06 陣列的進階方法

### 6.1 用 map() 方法來把陣列中的資料，改成你想要的樣子

`Array.prototype.map()`

這邊的意思是每個陣列都會有這方map()方法
他可以針對陣列中的內容做操作並且產生一個新的陣列

* 做數字運算

```javascript=
const a1 = [1, 4, 9, 16];
const result2 = a1.map((a) => {
    return a * a
})

console.log(result2); //
```
![](https://i.imgur.com/7K17cLP.png)


* 做字串串接

```javascript=
 let dogs = ["1", "2", "3", "4"]
 let result = dogs.map((dog) => {
     return dog + "dog is fury"
 })

 console.log(result);
```
![](https://i.imgur.com/rGJrID4.png)

### 6.2 如何使用 for 迴圈實作 map()

比較複雜一些需要用到比較多邏輯的部分不像map簡潔，但可以得到一樣的結果

```javascript=
let dogs = ["1", "2", "3", "4"]

function mapDemo(dogs) {
    let result = [];

    for (let i = 0; i < dogs.length; i++) {
        let str = dogs[i] + "dog is fury";
        result.push(str);
    }
    return result;
}
```
並且作呼叫印出的結果會跟使用map一樣
![](https://i.imgur.com/4Rhsfzg.png)


### 6.3 用 forEach() 讓陣列中的元素一個一個出來面對

逐個印出值並且無法做出return
```javascript=
const a1 = ['a', 'b', 'c', 'd', 'e', 'f']

let forEachResult = a1.forEach(function (el) {
    console.log(el);
})
```
![](https://i.imgur.com/G9oDqoS.png)

#### 跟map做比較

map會返回值可以做return
forEach不會返回值

```javascript=
const a1 = ['a', 'b', 'c', 'd', 'e', 'f']

let forEachResult = a1.forEach(function (el) {
    return el + "is good";
})

let mapResult = a1.map(function (el) {
    return el + "is good";
})
```

![](https://i.imgur.com/nTE6jns.png)

#### 用for來寫forEach

```javascript=
const a1 = ['a', 'b', 'c', 'd', 'e', 'f']


for (let i = 0; i < a1.length; i++) {
    console.log(a1[i] + "is good");
}
```
一樣可以印出結果
![](https://i.imgur.com/ufvZ70H.png)



### 6.4 使用 filter() 找出陣列中符合條件的元素(element)

使用條件做篩選並把選中的內容放進新的陣列

```javascript=
let as = [1, 2, 3, 4, 5, 6, 7, 8, 9];

newa = as.filter(function (a) {
    return a > 5
})
```

![](https://i.imgur.com/wVu73h2.png)


#### 用物件做操作

篩選出大於25歲小於123歲的物件排進新的陣列

```javascript=
let bs = [{
        name: 'tom',
        age: 36
    },
    {
        name: 'hoe',
        age: 123
    },
    {
        name: 'dif',
        age: 43
    },
    {
        name: 'aer',
        age: 25
    }
]
newa = bs.filter(function (b) {
    return b.age > 25 && b.age < 123
})
```

![](https://i.imgur.com/3UNrsks.png)



### 6.5 Array 陣列的 find() 方法，找到第一筆符合條件的資料

* Array 陣列的find()方法，找到第一筆符合條件的資料只印出一個找到的值
* filter()方法則是過濾符合的條件(每一筆)並組成新陣列


#### find()
```javascript=
const a1 = [1, 34, 52, 55, 12, 12, 12, 12, 2345, 55, 44];

let find = a1.find((found) => {
    return found === 12
});

console.log(find);
```
![](https://i.imgur.com/y9gnABv.png)


#### filter()
```javascript=
const a1 = [1, 34, 52, 55, 12, 12, 12, 12, 2345, 55, 44];

let find = a1.filter((found) => {
    return found === 12
});

console.log(find);
```
![](https://i.imgur.com/uxgc2CL.png)

### 6.6 為什麼查詢 Array 的方法時，需要找的是 Array.prototype 的方法

由下圖可以理解，在prototype後面加入的屬性是可以真的使用的

![](https://i.imgur.com/ukGal9q.png)


### 6.7 用 reduce() 加總陣列結果

可以使用forEach達到一樣的效果

```javascript=
let num = [1, 2, 4, 5, 6, 7, 8, 9, 10, 11, 12, ]

let result = 0;
num.forEach(function (n) {
    return result += n
})
console.log(result);

let sum = num.reduce(function (result, current) {
    result += current;
    return result;
}, 0)

console.log(sum);
```

![](https://i.imgur.com/NVlaXr3.png)