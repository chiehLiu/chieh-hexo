---
title: 實作練習-Javascript 30 02 - CSS + JS Clock
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Javascript 30 02 - CSS + JS Clock

---

## tags: Javascript relate

###### tags: `Javascript`

跟著做 js 30 第二個作品 CSS + JS Clock

[跟著做出來的範例](https://chiehLiu.github.io/git-projects/02%20-%20JS%20and%20CSS%20Clock/index-START.html)

![](https://i.imgur.com/n1YSCqe.png)

想法示意:

基本上這篇 JS 的概念比較簡單，就是使用 getSeconds/getMinutes/getHours 這三個 property 來取的現在的秒分時指向何方通過計算取的當下這一秒的時間中的角度，之後取得 style 裡面的 transform 去做旋轉，然後這邊都是只有一次的操作所以這邊計時器就必須介入讓他在多少的時間內再觸發一次設定成一秒時間的功能就完成摟!

這邊舉個例子如何取的角度:

我們的起始點使用 CSS 設定是 12:00:00

假設現在時間是 12 點 10 分 15 秒好了，

所以 12 點: 12*30 也就是繞了一圈 360 度也就是它在原地
10 分: 10*6 也就是 60 度
15 秒: 15\*6 也就是 90 度

可是在小時跟分鐘他們是會有比例的，跟隨著分鐘的前進時針也會等比例前進所以
12 點再 10 分的時候會往 1 點的方向動一點點: 12*30+12*30/60 也就是往前動了一點點六 6 度
以此類推

HTML:

這部分很直觀就是時間的各個部件

```htmlembedded=
<div class="clock">
    <div class="clock-face">
      <div class="hand second-hand"></div>
      <div class="hand min-hand"></div>
      <div class="hand hour-hand"></div>
```

CSS:

CSS 部分再比較特別的地方做解釋:

首先第一個部分圓心以及錶針的部分都是使用 after 來做裝飾

範例是秒針的部分，使用了定位定位在鐘面上待會比較好旋轉

```css=
.second-hand:after {
      position: absolute;
      content: '';
      display: block;
      width: 5px;
      height: 50%;
      background-color: red;
      left: 50%;
      bottom: 50%;
      transform: translate(-50%, 0%);
    }
```

## JS:

重點一取得現在時間

```javascript=
let data = new Date()
```

重點二
角度計算上面解釋了

重點三 旋轉

![](https://i.imgur.com/6GIr8UZ.png)

重點四 呼叫函式重設鐘面

`setClock(); //初始化畫面`

重點五

`setInterval`設定跑一次 function 的時間間隔

```javascript=
<script>
    ;
    (function () {
      const second = document.querySelector('.second-hand');
      const min = document.querySelector('.min-hand');
      const hour = document.querySelector('.hour-hand');

      //做時鐘

      function setClock() {
        let data = new Date()

        //這邊乘法出來的數字都是為了取得旋轉的度數

        let secondDeg = data.getSeconds() * 6 //(360/60) 一格跑六度
        let minDeg = data.getMinutes() * 6 + data.getSeconds() * 6 / 60 //(360/60) 一格跑六度
        let hourDeg = data.getHours() * 30 + data.getMinutes() * 30 / 60 //(360/12) 一格跑三十度

        second.style.transform = `rotate(${secondDeg}deg)`
        min.style.transform = `rotate(${minDeg}deg)`
        hour.style.transform = `rotate(${hourDeg}deg)`
        //transform是CSS的一種，直接用上面取的值去改變旋轉角度

      }
      setClock(); //初始化畫面

      //計時器 setInterval setTimeout requestAnimationFrame這三種可以選用

      setInterval(setClock, 1000);

    })()
  </script>
```

## 小補充的地方

取得時間

![](https://i.imgur.com/f4EpQEi.png)

CSS3 Transform 屬性

- 左右的偏移:在圓心的部分使用
  ![](https://i.imgur.com/Mt4X4fL.png)
- 旋轉的偏移:在錶針的部分使用
  ![](https://i.imgur.com/oZDMpWU.png)

setInterval()方法

`setInterval(要觸發的函式,多久觸發一次(毫秒))`
