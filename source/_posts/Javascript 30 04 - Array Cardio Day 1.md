---
title: 實作練習-Javascript 30 04 - Array Cardio Day 1
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Javascript 30 04 - Array Cardio Day 1

---

## tags: Javascript relate

###### tags: `Javascript`

跟著做 JS 30 第四個作品，不過這集比較多在介紹 array 裡面的內容，像是一些功能介紹等等

![](https://i.imgur.com/V70zMHQ.png)

上圖是 12 筆資料待會要開跑 array 的 methods

## 1. `Filter` -the list of inventors for those who were born in the 1500's

使用 filter 印出出生約在 1500~1600 左右的人

`Array.prototype.filter() `

`filter` 對內容作過濾後抽出幾個符合條件的然後做為一個"新陣列"產生，且不會影響原始的資料

```javascript=
let ans = inventors.filter(inventor => inventor.year >= 1500 && inventor.year < 1600)
//箭頭函式在箭頭後面的就是return的內容
console.table(ans) //這邊使用table可以印出表格
```

結果:
![](https://i.imgur.com/ZGYzXUv.png)

## 2. `map`-Give us an array of the inventors first and last names

給出一個 inventors 的新陣列包含了它們的 first 跟 last names

`Array.prototype.map()`

`map`產生"新陣列"列出符合條件的內容並且其內容可以針對 return 的東西

```javascript=
 let ans = inventors.map(inventor => inventor.first + ' ' + inventor.last);
 console.table(ans);
```

### 補充 forEach 的部分做一樣的題目

`Array.prototype.forEach()`

`forEach` 是對某些數量的東西各做一件甚麼事，如果沒有要產生新陣列時可以使用，有點像是加東西上去的概念

```javascript=
let ans = [];
inventors.forEach(inventor => ans.push(inventor.first + ' ' + inventor.last));
console.table(ans);
```

map 跟 forEach 產出的結果:

![](https://i.imgur.com/GuBBKDS.png)

## 3. `Sort` - the inventors by birthdate, oldest to youngest

`Array.prototype.sort()`

- 若 sort(a, b) 的回傳值小於 0，則會把 a 排在小於 b 之索引的位置，即 a 排在 b 前面。
- 若 sort(a, b) 的回傳值大於 0，則會把 b 排在小於 a 之索引的位置，即 b 排在 a 前面。
  如果我們是為了比較簡單的數字，可以利用 a 減 b。（由小到大）

let ary =[3,2,8,6,4,9] 這個使用 sort 之後會產生 由小排到大的預設[2,3,4,6,8,9]]

```javascript=
let ans = inventors.sort((a, b) => a.year - b.year)
//< 0 會往後排 == 0 保持原位 > 0 會往前排
console.table(ans)
```

根據生日前後排出來的結果:
![](https://i.imgur.com/eWG6x69.png)

## 4. `reduce` - How many years did all the inventors live all together?

`Array.prototype.reduce()`

> 我們會有一個暫存值，進入陣列去跟每個值做運算，最後回傳這個暫存值。

簡單來說就是使用加法做加總

```javascript=
let total = 0;
    inventors.forEach((inventor) => {
    total += inventor.passed - inventor.year
}) //傳統作法會使用forEach
```

`reduce`作法

```javascript=
let total = inventors.reduce((total, inventor) => {
   return total + inventor.passed - inventor.year
 }, 0)
 //參數 前面是function 後面0是初始起始值

```

---

以下是練習題

## 5. `Sort` - the inventors by years lived

照活的歲數排序

跟上面的操作差不多

```javascript=
let ans = inventors.sort((a, b) => {
    return (a.passed - a.year) - (b.passed - b.year)
});

console.table(ans);
```

印出結果:

![](https://i.imgur.com/8K35h14.png)

## 6. create a list of Boulevards in Paris that contain 'de' anywhere in the name

從下面這個頁面找出有多少個字包含了'de'這兩個字母在裡面

https://en.wikipedia.org/wiki/Category:Boulevards_in_Paris

首先創造一個先陣列 ary

選取所有的 Boulevards 會發現我們要的文字內容 text 會在`.mw-category-group li a`這邊找到

接下來`forEach`每一個[]並且 push 進去選取到的文字組合這邊會得到 38 個項目

下一步來做`filte`r 篩選出要得'de'在 text 裡面尋找完全不一樣是-1 完全一樣是 1 不相關是 0

![](https://i.imgur.com/rJk7kkx.png)

```javascript=
let ary = [];
      document.querySelectorAll('.mw-category-group li a').forEach((a) => {
      ary.push(a.text);
    });
    let ans = ary.filter(text => text.indexOf('de') !== -1);
```

得出結果:

![](https://i.imgur.com/BUUUqEf.png)

## 7. `sort` - Exercise-Sort the people alphabetically by last name

照 abcd 順序排列所有人的 last name

```javascript=
let ans = people.sort((a, b) => {
      let [aFirst, aLast] = a.split(', ')
      let [bFirst, bLast] = b.split(', ')

      return aLast > bLast ? 1 : bLast > aLast ? -1 : 0//判斷整個單字
      return aLast[0] > bLast[0] ? 1 : bLast > aLast[0] ? -1 : 0//只判斷第一個字

      //如果a>b則 1 如果不是則繼續 b>a 如果"是"則反應 -1 否則為 0
    })
```

印出結果(片段...後面太長卡掉)

![](https://i.imgur.com/7Lu3UhN.png)

## 8. `Reduce` - Exercise -Sum up the instances of each of these

加總 data 內部的字串數量有多少

得到的結果應該會長這樣:
{
car: ...
truck:...
bike:...

}

```javascript=
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car',
      'truck'
    ];
let ans = data.reduce((obj, content) => {
        if (!obj[content]) obj[content] = 1 //當obj內容不等於物件內容的時候回覆1 ， 除此之外回覆 obj[content]++ ，之後再跑回迴圈return obj
        else obj[content] += 1

        return obj
}, {})

console.table(ans)
```

結果如下

![](https://i.imgur.com/RzMkuvZ.png)
