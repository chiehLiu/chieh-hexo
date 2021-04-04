---
title: 實作練習-New Year Countdown
date:
tags: [HTML, CSS, JavaScript, jQuery]
category: Javascript作品
---

# New Year Countdown- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個新年倒數器

## 成品:

![](https://i.imgur.com/2hgb9LC.png)

[成品網址](https://chiehliu.github.io/git-projects/new-year-countdown/index.html)

## 成品功能:

1.倒數距離下一個新年還有幾天幾小時幾分鐘幾秒 2.顯示下一年在背景 3.當重整畫面時會顯示 loading
![](https://i.imgur.com/29PLXLA.png)
讓顯示時間的區域隱藏變成 loading 的樣式
![](https://i.imgur.com/Zbdkh8b.png)

# HTML

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta http-equiv="X-UA-Compatible" content="ie=edge" />
  <link rel="stylesheet" href="style.css" />
  <title>New Year Countdown</title>
</head>

<body>
  <div id="year" class="year"></div>

  <h1>New Year Countdown</h1>

  <!-- 在JS作互動 -->
  <div id="countdown" class="countdown">
    <div class="time">
      <h2 id="days">00</h2>
      <small>days</small>
    </div>
    <div class="time">
      <h2 id="hours">00</h2>
      <small>hours</small>
    </div>
    <div class="time">
      <h2 id="minutes">00</h2>
      <small>minutes</small>
    </div>
    <div class="time">
      <h2 id="seconds">00</h2>
      <small>seconds</small>
    </div>
  </div>

  <!-- 這部分在處理JS的時候才會打開 -->
  <img src="./img/spinner.gif" alt="Loading..." id="loading" class="loading" />

  <script src="script.js"></script>
</body>

</html>
```

# CSS:

## CSS 設置好的樣式

![](https://i.imgur.com/2hgb9LC.png)

## CSS 完整程式碼

```css=
@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');

* {
  box-sizing: border-box;
}

body {
  background-image: url('https://images.unsplash.com/photo-1467810563316-b5476525c0f9?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit-crop&w=1349&q=80');

  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  height: 100vh;
  color: #fff;
  font-family: 'Lato', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  margin: 0;

  /* 讓卷軸不出現 */
  overflow: hidden;
}

/* 製作一個黑色的罩子讓白字更顯眼 */
body::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
}

/* 把body內部的東西全部蓋在最上層 */
body * {
  z-index: 1;
}

h1 {
  font-size: 60px;
  margin: -80px 0 40px;
}

/* 會隨著JS做動態變化每年更新一次 */
.year {
  font-size: 200px;
  z-index: -1;
  opacity: 0.2;
  position: absolute;
  bottom: 20px;
  left: 50%;
  transform: translateX(-50%);
}

.countdown {
  /* flex讓他們成橫排列 */
  display: none;

  /* 放大或是縮小的倍率 */
  transform: scale(2);
}

.time {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 15px;
}

.time h2 {
  margin: 0 0 5px;
}

/* 縮小字體跟一些margin讓小螢幕裝置也可以使用 */
@media(max-width:500px) {
  h1 {
    font-size: 45px;
  }

  .time {
    margin: 5px;
  }

  .time h2 {
    font-size: 12px;
    margin: 0;
  }

  .time small {
    font-size: 10;
  }
}
```

小補充:

無

# JS:

## 變數設置

- 抓取四個框框呈現數字

```javascript=
const days = document.getElementById('days');
const hours = document.getElementById('hours');
const minutes = document.getElementById('minutes');
const seconds = document.getElementById('seconds');
```

![](https://i.imgur.com/zVCiC5u.png)

- 抓取整個 countdown 區塊

為了呈現 loading 時可以把框框移除掉

```javascript=
const countdown = document.getElementById('countdown');
```

![](https://i.imgur.com/EXU1dk2.png)

- 在背景顯示新的一年年分

```javascript=
const year = document.getElementById('year');
```

![](https://i.imgur.com/L90apbx.png)

- loading 圖示

```javascript=
const loading = document.getElementById('loading');
```

![](https://i.imgur.com/YnAAo6V.png)

- 現在年分以及新的一年的時間

currentYear 用來取得新的一年的時間(在程式碼中需要+1)
newYearTime 用來減去現在時間得倒數

```javascript=
const currentYear = new Date().getFullYear();
const newYearTime = new Date(`January 01 ${currentYear + 1} 00:00:00`);
```

## functions:

- updateCountdown() -用扣的方式得到倒數 diff = newYearTime - currentTime
  -diff 得出來的值是以毫秒呈現必須先除以 1000 得到秒數
  -%60 是因為要看剩下幾秒而不是過了幾秒其他部分以此類推 -使用 innerHTML,innerText 貼倒 DOM 上面 -數字呈現部分採用三元邏輯運算子? 來呈現小於 10 的數字要左邊加個 0 大於 10 就直接呈現

```javascript=
// 讓倒數時間可以更新
function updateCountdown() {
  const currentTime = new Date();
  const diff = newYearTime - currentTime;

  const d = Math.floor(diff / 1000 / 60 / 60 / 24);
  const h = Math.floor(diff / 1000 / 60 / 60) % 24;
  const m = Math.floor(diff / 1000 / 60) % 60;
  const s = Math.floor(diff / 1000) % 60;

  // 把數字推到DOM上面
  days.innerHTML = d;
  hours.innerHTML = h < 10 ? '0' + h : h;
  minutes.innerHTML = m < 10 ? '0' + m : m;
  seconds.innerHTML = s < 10 ? '0' + s : s;
  year.innerText = currentYear + 1;
}
```

- setTimeout() 把 loading 畫面 show 出來並且設定在一秒內移除 loading 畫面以及把 flex 屬性加回去 countdown
- setInterval() 每秒更新一次

```javascript=
// 把loading畫面show出來
// 設定在一秒內移除loading畫面以及把flex屬性加回去countdown
setTimeout(() => {
  loading.remove();
  countdown.style.display = 'flex';
}, 1000);

// 每秒更新一次
setInterval(updateCountdown, 1000);
```

## 事件監聽

無

## JS 完整程式碼:

```javascript=
const days = document.getElementById('days');
const hours = document.getElementById('hours');
const minutes = document.getElementById('minutes');
const seconds = document.getElementById('seconds');
const countdown = document.getElementById('countdown');
const year = document.getElementById('year');
const loading = document.getElementById('loading');

const currentYear = new Date().getFullYear();
const newYearTime = new Date(`January 01 ${currentYear + 1} 00:00:00`);



// 讓倒數時間可以更新
function updateCountdown() {
  const currentTime = new Date();
  const diff = newYearTime - currentTime;

  const d = Math.floor(diff / 1000 / 60 / 60 / 24);
  const h = Math.floor(diff / 1000 / 60 / 60) % 24;
  const m = Math.floor(diff / 1000 / 60) % 60;
  const s = Math.floor(diff / 1000) % 60;

  // 把數字推到DOM上面
  days.innerHTML = d;
  hours.innerHTML = h < 10 ? '0' + h : h;
  minutes.innerHTML = m < 10 ? '0' + m : m;
  seconds.innerHTML = s < 10 ? '0' + s : s;
  year.innerText = currentYear + 1;
}

// 把loading畫面show出來
// 設定在一秒內移除loading畫面以及把flex屬性加回去countdown
setTimeout(() => {
  loading.remove();
  countdown.style.display = 'flex';
}, 1000);

// 每秒更新一次
setInterval(updateCountdown, 1000);
```

# jQuery

本篇改寫成 jQuery 的地方:

## updateTimeToDOM()

主要是抓取日月年分秒的部分

## setTimeout()

抓取 loading 圖片部份一秒後移除掉

抓取 countdown 部分來一秒後移除`display:none`

```javascript=
//這邊會得到2021主要處理每個新的一年的更新
const currentYear = new Date().getFullYear();
const nextYear = new Date(`January 01 ${currentYear + 1} 00:00:00`);

//把數字黏到DOM上面
//這邊數字部分最後 取餘數是因為這邊計算的是倒數也就是得扣掉經過的時間
function updateTimeToDOM() {

  //這邊處理倒數的時間有多少秒
  //currentTime,conuntDownNum,totalSeconds這三個變數必須放在updateTimeToDOM內部，時間才會更新!
  const currentTime = new Date()
  const conuntDownNum = nextYear - currentTime;
  const totalSeconds = Math.floor(conuntDownNum / 1000)
  const s = Math.floor(totalSeconds % 60);
  const m = Math.floor(totalSeconds / 60 % 60);
  const d = Math.floor(totalSeconds / 60 / 60 / 24);
  const h = Math.floor(totalSeconds / 60 / 60 % 24)

  $('#days').text(d < 10 ? '0' + d : d);
  $('#hours').text(h < 10 ? '0' + h : h);
  $('#minutes').text(m < 10 ? '0' + m : m);
  $('#seconds').text(s < 10 ? '0' + s : s);
  $('#year').text(currentYear);
}

setInterval(updateTimeToDOM, 1000);


//這邊處理點擊重新整理後一秒鐘移除loading整個圖片
//以及處理點擊重新整理後一秒鐘讓整個畫面顯示flex也就是重新顯示倒數框框回來(這邊我預設處理css部分為display:none轉圈一秒後改成flex)
setTimeout(function () {
  $('#loading').remove();
  $('.countdown').css('display', 'flex')
}, 1000);
```
