---
title: 實作練習-10 JS little practice
date:
tags: [HTML, CSS, JavaScript, jQuery]
category: Javascript作品
---

# 10 JS little practice - vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作十個小功能 JS 練習 - 1

## 成品: 漢堡選單功能

![](https://i.imgur.com/INZcJQZ.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/hamburger/index.html)

## 成品功能:

點擊漢堡會開關右側欄位

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <button id="btn">☰</button>
    <nav id="nav">
        <ul>
            <li><a href="">Google</a></li>
            <li><a href="">Youtube</a></li>
            <li><a href="">Twitter</a></li>
        </ul>
    </nav>
</body>
<script src="script.js"></script>
</html>
```

# CSS:

- 當 class .active 加 btn 及 nav 上面時則選單跳出消失則選單消失
- 使用簡單的特效取處在進出時稍慢一點
  ` transition: transform 0.3s ease-in-out;`

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

上方為基礎設定 全置中 margin 0 border-box 字體設定
---

button {
    background-color: gray;
    border: none;
    color: black;
    position: fixed;
    top: 20px;
    right: 20px;
    padding: 1rem;
    transition: transform 0.3s ease-in-out;
}

button.active {
    transform: translateX(-100px);
}

nav {
    background-color: gray;
    position: fixed;
    top: 0;
    right: 0;
    height: 100vh;
    padding: 2rem;
    transform: translateX(100%);
}

nav.active {
    transform: translateX(0)
}

/* 取消三個連結的padding,margin讓它們為0 */
nav ul {
    padding: 0;
    list-style-type: none;
    margin: 0;
}

/* 行間上下的距離 */
nav ul li {
    padding: 1rem 0;
}

nav a {
    color: white;
    text-decoration: none;
}
```

# JS:

- 抓取 btn 以及 nav 後做事件監聽
- 當點擊 btn 的時候 nav,btn 的元素會加上或是移除.active 這個 class
- `toggle()`的使用所以有開關的效果

## JS 完整程式碼:

```javascript=
const btn = document.getElementById('btn');
const nav = document.getElementById('nav');

btn.addEventListener('click', (() => {
    nav.classList.toggle('active');
    btn.classList.toggle('active');
}))
```

# 製作十個小功能 JS 練習 - 2

## 成品: 點擊按鈕後跑出通知

![](https://i.imgur.com/SZ4bNM2.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/toast-notification/index.html)

## 成品功能:

1. 點擊按鈕後跑出通知
1. 三秒後通知消失

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <div id="container"></div>
    <button id="btn">Click me Pretty Please</button>
</body>
```

# CSS:

- CSS 處理.toast 的修飾部分

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

button {
    background-color: gray;
    color: white;
    padding: 1rem;

/*     字體直接繼承body */
    font-family: inherit;
    border-radius: 5px;
    border: none;
}

/* 把notification定位 */
#container {
    position: fixed;
    bottom: 10px;
    right: 10px;
}

/* 針對notification修飾 */
.toast {
    padding: 2rem;
    background-color: gray;
    color: white;
    border-radius: 5px;
    margin: 1rem;
}
```

# JS:

- 抓取 btn 以及 container div
- 做事件監聽當點擊 btn 時會跑`createNotifiction()`
- 設置`setTimeout()`定時三秒消失

`createNotifiction()`
使用`createElement()`做 div 出來，給他加上 class .toast(在 toast 做他的修飾)
並且`appnedChild()` notif 到 container 裡面就完成瞜!

## JS 完整程式碼:

```javascript=
const btn = document.getElementById('btn');
const container = document.getElementById('container');

btn.addEventListener('click', () => {
    createNotifiction();
});

function createNotifiction() {
    const notif = document.createElement('div');

    notif.classList.add('toast');
    container.appendChild(notif);

    notif.innerText = 'this challenge is crazy'
    setTimeout(() => {
        notif.remove();
    }, 3000)
};
```

# 製作十個小功能 JS 練習 - 3

## 成品: 自動輸入文字的跑馬燈

![](https://i.imgur.com/DzgTev4.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/auto-write-text/index.html)

## 成品功能:

- 文字會自動輸入在頁面中間
- 每 0.1 秒會跑下一段文字
- 不會中斷會無限跑下去

# HTML

空白配置

# CSS:

基本上也只修飾顏色跟字體

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    background-color: gray;
    color: white;
    font-size: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}
```

# JS:

- `slice(begin index,end inedex)`
  到 end index "之前"停止提取。
  [slice() MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)

- 使用 index++ 讓 inneText 不斷印出每個 slice 擷取的字
  最後使用判斷式當 index 大於字串長度時歸零從頭開始

- 使用 setInterval 不斷的呼叫 writeText 函式秒 0.1 秒呼叫一次無限循環

## JS 完整程式碼:

```javascript=
const text = 'This string is going to show on the browser automatically using Javascript';
let index = 0;

function writeText() {
    document.body.innerText = text.slice(0, index);

    index++;

    if (index > text.length) {
        index = 0;
    }
};

setInterval(writeText, 100);
```

# 製作十個小功能 JS 練習 - 4

## 成品: 點擊按鈕後跳出視窗並且可以關閉

![](https://i.imgur.com/PfmRNSw.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/popup/index.html)

## 成品功能:

- 點擊按鈕後跳出視窗並且可以關閉
- 改變背景色

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <button id="open">Open</button>
    <div class="popup-container" id="container">
        <div class="popup">
            <button id="close">&times;</button>
            <h1>Popup-btn</h1>
            <p>Using JS to pop this up </p>
        </div>
    </div>
</body>
```

# CSS:

- 這邊的切換讓 popup 區塊出現

```css=
.popup-container.active {
    display: flex;
}
```

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

button {
    background-color: black;
    color: white;
    padding: 1rem;
    border-radius: 4px;
    border: none;
    font-family: inherit;
}

.popup-container {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);

    display: none;
    align-items: center;
    justify-content: center;
}

.popup-container.active {
    display: flex;
}

.popup {
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    padding: 2rem;
    position: relative;
    width: 500px;
}

.popup button {
    padding: .5rem;
    background-color: #fff;
    color: gray;
    position: absolute;
    top: 10px;
    right: 10px;
}
```

# JS:

- 抓取 open,close 按鈕以及 popup 容器
- open, close 設置事件監聽點擊時加上以及移除 class.active

## JS 完整程式碼:

```javascript=
const open = document.getElementById('open');
const close = document.getElementById('close');
const container = document.getElementById('container');

open.addEventListener('click', () => {
    container.classList.add('active');
});

close.addEventListener('click', () => {
    container.classList.remove('active');
});
```

# 製作十個小功能 JS 練習 - 5

## 成品: 下紫色愛心雨的背景

![](https://i.imgur.com/YMmae6Y.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/purple-heart-rain/index.html)

## 成品功能:

- 下紫色愛心雨
- 位置隨機
- 動畫延續時間隨機

# HTML

空白配置

# CSS:

heart 的修飾

- 畫面一開始保持空白所以設置位置固定在螢幕外面
- 這邊把愛心移動到 Y 軸去生出來
- 動畫部分設置 延續 0.3 秒(讓愛心不那麼密集) linear 線性(動畫等速移動) forwards(forwards 代表動畫結束會就停在結束階段不會跑回去)

[animation-fill-mode forwards MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/animation-fill-mode)

[animation-timing-function linear MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/animation-timing-function)

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

.heart {
    position: fixed;
    top: -1vh;
    transform: translateY(0);
    animation: fall 3s linear forwards;
    font-size: 2rem;
}

@keyframes fall {
    to {
        transform: translateY(105vh);
    }
}
```

# JS:

- `createElement('div')`創造愛心並且加上 class .heart
- 把位置做隨機 使用 style.left (其實 right 也可) 使用隨機數串接字串'vw'
- 把下降時間作隨機 使用 style.animationDuration 使用隨機數串接字串's'
- 把出現在`innerText`的部分換成 💜
- 把 💜 貼到 body 上面使用`appendchild()`
- 最後設置 setTimeout 讓愛心消失
- 每個愛心的出現時間 0.3 秒出現一顆`setInterval()`每 0.3 秒呼叫一次`createHeart()`

## JS 完整程式碼:

```javascript=
function createHeart() {
    const heart = document.createElement('div');
    heart.classList.add('heart');

    heart.style.left = Math.random() * 100 + 'vw';
    heart.style.animationDuration = Math.random() * 2 + 5 + 's';
    heart.innerText = '💜';
    document.body.appendChild(heart);

    setTimeout(() => {
        heart.remove();
    }, 5000)
}

setInterval(createHeart, 300);
```

# 製作十個小功能 JS 練習 - 6

## 成品: 點擊按鈕更改背景顏色

![](https://i.imgur.com/w1hsVtY.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/background-changer/index.html)

## 成品功能:

- 點擊按鈕更改被景色

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <button id="btn">Change background</button>
</body>
```

# CSS:

修飾按鈕外觀

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

button {
    background-color: gray;
    color: white;
    padding: 1rem;
    font-family: inherit;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    border-radius: 5px;
    border: none;
    outline: none;
}

button:hover {
    cursor: pointer;
    background-color: black;
}
```

# JS:

- 抓取 btn 後做事件監聽處理當點擊時觸發`randombg()`
- `randombg()`可以使用 rgba 或是 hsl 的方式用 Math.floor(Math.random()\*100)去處理顏色的係數變化並使用樣板字面值（Template literals）`${}`嵌入變數做操作

## JS 完整程式碼:

```javascript=
const btn = document.getElementById('btn');

btn.addEventListener('click', () => {
    document.body.style.background = randomBg();
})

function randomBg() {
    // return `hsl(${Math.floor(Math.random()*360)}, 100%, 50%)`
    return `rgba(${Math.floor(Math.random()*100)}%, ${Math.floor(Math.random()*100)}%, ${Math.floor(Math.random()*100)}%, ${Math.floor(Math.random()*100)}%)`
}
```

# 製作十個小功能 JS 練習 - 7

## 成品:製作一個切換頁面背景的按鈕

![](https://i.imgur.com/3VY3teh.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/dark-mode-toggle/index.html)

## 成品功能:

- 製作一個切換頁面背景的按鈕
- 切換動畫有時間延遲

# HTML

label 處的 for 必須要跟 input 的 id 名稱一樣才能作連動，也就是點擊 label 處 input 的 checkbox 連動，這樣點擊圓圈才有用

## html 程式碼:

```htmlembedded=
<body>
    <div class="toggle-container">
        <input type="checkbox" id="toggle" name="toggle"><label for="toggle"></label>
    </div>
    <h1>using JS to toggle dark mode</h1>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cumque obcaecati sint, libero dignissimos aliquam natus,
        magnam dolorum iure, porro commodi magni repellendus quis quibusdam accusantium culpa iusto! Unde, debitis
        minima.</p>
</body>
```

# CSS:

- transition 處理在 body 並且因為背景以及文字都有改變所以都可以加入持續時間以及速度
- label 的部分也會切換顏色所以一樣使用 transition
- label 需要有 blcok 屬性才有辦法設置 width
- input 做隱藏(把打勾框框藏起來)只出現 label(所以要作連動)

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
    text-align: center;
    padding: 5rem;
    transition: background 0.3s linear, color 0.3s linear;
}

body.dark {
    background-color: #1f1f1f;
    color: #fff;
}

.toggle-container {
    position: fixed;
    top: 10px;
    right: 10px;
}

label {
    background-color: gray;
    border-radius: 50%;
    display: inline-block;
    width: 50px;
    height: 50px;
    cursor: pointer;
    user-select: none;
    transition: background 0.3s linear;
}

body.dark label {
    background-color: #fff;
}

input {
    visibility: hidden;
}
```

# JS:

- `e.target.checked`是 Boolean 會回傳 true/false 也就是狀態 checked 與否，
- 當狀態是 true 則加入 class .dark，flase 的話則移除 class .dark
- `toggle(要被開關的東西, boolean)`

[toggle MDN](https://developer.mozilla.org/en-US/docs/Web/API/DOMTokenList/toggle)

## JS 完整程式碼:

```javascript=
const toggle = document.getElementById('toggle');

toggle.addEventListener('change', (e) => {
    document.body.classList.toggle('dark', e.target.checked)
});
```

# 製作十個小功能 JS 練習 - 8

## 成品: 自己滾動的投影片

![](https://i.imgur.com/LvYg0DB.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/carousel/index.html)

## 成品功能:

- 每兩秒換一張投影片
- 換到最後一張時會回到最開頭
- 有慢進慢出特效

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <div class="carousel">
        <div class="image-container" id="imgs">
            <img src="https://images.unsplash.com/photo-1599394022918-6c2776530abb?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1458&q=80"
                alt="" />
            <img src="https://images.unsplash.com/photo-1593642632559-0c6d3fc62b89?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1500&q=80"
                alt="" />
            <img src="https://images.unsplash.com/photo-1599423300746-b62533397364?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1500&q=80"
                alt="" />
            <img src="https://images.unsplash.com/photo-1599561046251-bfb9465b4c44?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1492&q=80"
                alt="" />
        </div>
    </div>
</body>
```

# CSS:

- 使用 overflow:hidden 來隱藏圖片(不然因為 flex 圖片會並排並且出現卷軸)
- 在 image-container 做水平移動特效
- 使用`object-fit: cover;`讓圖片不失真

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

.carousel {
    box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.3);
    overflow: hidden;
    height: 500px;
    width: 500px;
}

.image-container {
    display: flex;
    transition: transform 0.5s ease-in-out;
    transform: translateX(0);
}

img {
    object-fit: cover;
    height: 500px;
    width: 500px;
}
```

# JS:

- 抓取`translsateX`設定的視窗也就是 image-container
- 為了取得 index 長度抓取所有的 img tag
- 用 style 加上水平移動並且使用 index \* img 寬度 切換投影片位置剛剛好到下一張
- 使用判斷式當 idx 加到超過 img 長度-1 時回到開頭(因為只要跑三次)

## JS 完整程式碼:

```javascript=
const imgs = document.getElementById('imgs');
const img = document.querySelectorAll('#img');
let idx = 0;

function run() {
    idx++;

    if (idx > img.length - 1) {
        idx = 0;
    }

    imgs.style.transform = `translateX(${-idx * 500}px)`;
};

setInterval(run, 2000);
```

# 製作十個小功能 JS 練習 - 9

## 成品: 聲音按鈕

![](https://i.imgur.com/7ZM93DI.png)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/sound-board/index.html)

## 成品功能:

- 點擊按鈕會產生音效
- 當點擊下一個按鈕時上一個的音效會停止
- 下一次點擊同樣的按鈕時音效會歸零從頭開始跑

# HTML

- 設置 audio tag 並且引入檔案

## html 程式碼:

```htmlembedded=
<body>
    <audio id="clapping" src="sound/clapping.mp3"></audio>
    <audio id="boo" src="sound/boo.mp3"></audio>
    <audio id="gasp" src="sound/gasp.mp3"></audio>
</body>
```

# CSS:

- 處理按鈕外觀

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

.btn {
    background-color: gray;
    color: white;
    font-family: inherit;
    font-size: 1.2rem;
    padding: 1.5rem 3rem;
    border-radius: 5px;
    margin: 1rem;
    border: none;
}
```

# JS:

- 建立陣列內容是音檔的 id 名稱
- 使用 forEach 個別印出所有的音檔的名字並且產生按鈕
- 處理點擊事件 1.先引入停止函式 2.開始撥放音效(這個順序讓聲音還是可以正常撥出)
- 停止函式的部分會把音效暫停`song.pause();`並且把撥放時間歸零`song.currentTime = 0;`

## JS 完整程式碼:

```javascript=
const sounds = [
    'clapping',
    'boo',
    'gasp',
]

sounds.forEach((sound) => {
    const btn = document.createElement('button');
    btn.classList.add('btn');

    document.body.appendChild(btn);

    btn.innerText = sound;

    btn.addEventListener('click', () => {
        stopSounds()

        document.getElementById(sound).play();
    })
})

function stopSounds() {
    sounds.forEach((sound) => {
        const song = document.getElementById(sound);

        song.pause();
        song.currentTime = 0;
    })
}
```

# 製作十個小功能 JS 練習 - 10

## 成品: 有 ZOOM 效果的圖片

![](https://i.imgur.com/u2uLBko.gif)

[成品網址](https://chiehliu.github.io/git-projects/10-Project-1-Hour/zoom-effect/index.html)

## 成品功能:

- 隨著滑鼠移動會有放大效果
- 滑鼠離開視窗效果就會解除

# HTML

## html 程式碼:

```htmlembedded=
<body>
    <div id="container">
        <img src="https://images.unsplash.com/photo-1582769923195-c6e60dc1d8dc?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1000&q=80"
            alt="purple kitty" />
    </div>
</body>
```

# CSS:

- `overflow: hidden;`可以限制圖片在原地，非常重要

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css2?family=Poppins:wght@200;400;600&display=swap");

* {
    box-sizing: border-box;
}

body {
    background-color: rebeccapurple;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: "Poppins", sans-serif;
    margin: 0;
    min-height: 100vh;
}

#container {
    box-shadow: 3px 3px 4px rgba(0, 0, 0, 0.3);
    height: 500px;
    width: 500px;
    overflow: hidden;
}

img {
    transform-origin: center center;
    object-fit: cover;
    height: 100%;
    width: 100%;
}
```

# JS:

- 抓取 container, img

- clientX 代表滑鼠在瀏覽器上面的位置

- offsetLeft 距離
  ![](https://i.imgur.com/1AHmrcV.png)

- 故`x = e.clientX - e.target.offsetLeft;`就等於圖片上面的 x 軸的位置，y 軸同理

![](https://i.imgur.com/qGgPrP5.png)

- `scale`以及`transform-origin`的組合技會友針對位置放大的效果
- 透過 mouseleave 事件把組合技還原

[overflow MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow)
[offsetLeft MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/offsetLeft)
[clientX MDN](https://developer.mozilla.org/en-US/docs/Web/API/MouseEvent/clientX)
[transform-origin MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/transform-origin)

## JS 完整程式碼:

```javascript=
const container = document.getElementById('container');
const img = document.querySelector('img');

container.addEventListener('mousemove', (e) => {
    const x = e.clientX - e.target.offsetLeft;
    const y = e.clientY - e.target.offsetTop;

    img.style.transformOrigin = `${x}px ${y}px`;
    img.style.transform = 'scale(2)';
})

container.addEventListener('mouseleave', () => {
    img.style.tranformOrigin = '0 0';
    img.style.transform = 'scale(1)';
})
```
