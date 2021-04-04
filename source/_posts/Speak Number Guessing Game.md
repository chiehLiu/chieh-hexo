---
title: 實作練習-Speak Number Guessing Game
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Speak Number Guessing Game- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個用聲音猜數字的遊戲

## 成品:

![](https://i.imgur.com/463ouXb.png)

[成品網址](https://chiehliu.github.io/git-projects/Speak%20Number%20Guessing%20Game/index.html)

## 成品功能:

1.詢問是否可以使用麥克風![](https://i.imgur.com/v7tnOj7.png) 2.判斷數字是否正確 3.顯示離目前數字的位置 - 喊得太高或是太低 4.如果喊得不是數字會顯示相對字樣 5.當遊戲成功會顯示按鈕讓遊戲重來

# HTML

## 上 CSS 之前的 HTML:

## html 程式碼:

```htmlembedded=
<body>

    <img src="img/mic.png" alt="Speak">
    <h1>Guess a Number Between 1 - 100</h1>

    <h3>Speak the number into your microphone</h3>

    <!-- 這個div會填入我們口說的內容透過JS呈現 -->
    <div id="msg" class="msg">
        <div>You said:</div>
        <span class="box">20</span>
        <div>GO HIGHER</div>
    </div>
    <script src="script.js"></script>
</body>
```

# CSS:

## CSS 設置好的樣式

![](https://i.imgur.com/463ouXb.png)

## CSS 完整程式碼

```css=
 * {
    box-sizing: border-box;
}

body {
    background: #2f3542 url('img/bg.jpg') no-repeat left center/cover;
    color: #fff;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    text-align: center;
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
}

h1,
h3 {
    margin-bottom: 0;
}

p {
    line-height: 1.5;
    margin: 0;
}

/* 重新遊玩按鈕會透過JS呈現 */
.play-again {
    padding: 8px 15px;
    border: 0;
    background: #f4f4f4;
    border-radius: 5px;
    margin-top: 10px;
}

.msg {
    font-size: 1.5em;
    margin-top: 40px;
}

/* 挑戰者猜的內容的框框修飾 */
.box {
    border: 1px solid #dedede;
    display: inline-block;
    font-size: 30px;
    margin: 20px;
    padding: 10px;
}
```

# JS:

## 前置作業

後方 webkit 部分是為了瀏覽器相容使用的

```javascript=
window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition
```

## 變數設置

本篇唯一一個變數裡面會放入:

- 猜的數字
- 顯示高於低於
- 顯示內容不符合

`const msgEl = document.getElementById("msg");`

![](https://i.imgur.com/3Hq6pDd.png)

## functions:

### `randomNum()`

產生題目(隨機數字 1-100 內)
抓取聲音產生的值
把抓取到聲音的值推到 DOM 上

### `randomNum()`產生題目(隨機數字 1-100 內)

```javascript=
//這邊+1因為Math.random*100數字只到99不會到100所以必須做這個動作
const randomNum = Math.floor(Math.random() * 100) + 1;

// 檢查隨機數字有無正常生成
//把答案呈現在頁面上以便確認功能
// console.log(randomNum);
```

### `onSpeak()`抓取聲音產生的值

抓取後:

- 把抓取到聲音的值推到 DOM 上 `writeMessage(msg)`
- 辨別使用者聲音答案是否符合題目 `checkNumber(msg)`

```javascript=
function onSpeak(e) {
    const msg = e.results[0][0].transcript;

    //檢查是否有音檔產生的值
    // console.log(msg);

    writeMessage(msg);
    checkNumber(msg);
}
```

### `writeMessage()`把抓取到聲音的值推到 DOM 上

```javascript=
//write what user speaks to DOM
function writeMessage(msg) {
    msgEl.innerHTML = `
    <div>You said:</div>
    <span class="box">${msg}</span>`;
}
```

### `checkNumber()`辨別使用者聲音答案是否符合題目:

- 是否是數字
- 確認範圍有無超過
- 確認有沒有答對

```javascript=
// check msg against number
function checkNumber(msg) {
    const num = +msg;

    //確認是否是數字
    if (Number.isNaN(num)) {

        //這邊使用+=讓這邊的字串不會覆蓋掉wreiteMessage部分的文字
        msgEl.innerHTML += `
       <div>This is not a valid number</div>`;

        return;
    }

    //確認範圍
    if (num > 100 || num < 1) {
        msgEl.innerHTML += `<div>Number must be between 1 - 100</div>`;
        return;
    }

    //確認是否猜對
    if (num === randomNum) {

        //這邊因為已經答對要覆蓋住整個區域了所以不需要使用+=了
        document.body.innerHTML = `<h2>Congrats! You have guessed the number! <br>It was ${num}</h2><button class="play-again" id="play-again">Play Again</button>`
    } else if (num > randomNum) {
        msgEl.innerHTML += '<div>GO LOWER</div>';
    } else {
        msgEl.innerHTML += '<div>GO HIGHER</div>';
    }
}
```

## 事件監聽

使用聲音辨識 API 可以先把它設置為物件並且指派給`recognition`做變數使用比較好操作

SpeechRecognition 專屬的事件

- result- 當 SpeechRecognition 回傳一個值的時候觸發用來抓取使用者輸入的數字
- end- 當 SpeechRecognition 服務停止時觸發，用來繼續遊戲
- start- 開始接收音檔

```javascript=

let recognition = new SpeechRecognition();

//start recogniiton and game
recognition.start();

//speak result取得音檔的值藉由onSpeak函式
recognition.addEventListener('result', onSpeak)

//當猜一次後(沒有答對)讓遊戲繼續
recognition.addEventListener('end', () => recognition.start());

//搭遊戲答對會出現reload按鈕設置事件click並且判斷其id是否為play-again是的話畫面reload
document.body.addEventListener('click', (e) => {

    // 因為這邊的id是只有答對後才出現所以抓取事件在整個body上面所以必須選取其中的target.id才有辦法明確的抓到這個按鈕
    if (e.target.id == 'play-again') {
        window.location.reload();
    }
})
```

小補充:

[SpeechRecognition MDN](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition)

## JS 完整程式碼:

```javascript=
const msgEl = document.getElementById("msg");

//抓取使用者聲音的值capture user speak
function onSpeak(e) {
    const msg = e.results[0][0].transcript;

    //檢查是否有音檔產生的值
    // console.log(msg);

    writeMessage(msg);
    checkNumber(msg);
}

//write what user speaks to DOM
function writeMessage(msg) {
    msgEl.innerHTML = `
    <div>You said:</div>
    <span class="box">${msg}</span>`;
}

// check msg against number
function checkNumber(msg) {
    const num = +msg;

    //確認是否是數字
    if (Number.isNaN(num)) {

        //這邊使用+=讓這邊的字串不會覆蓋掉wreiteMessage部分的文字
        msgEl.innerHTML += `
       <div>This is not a valid number</div>`;
        //使用return是因為
        return;
    }

    //確認範圍
    if (num > 100 || num < 1) {
        msgEl.innerHTML += `<div>Number must be between 1 - 100</div>`;
        return;
    }

    //確認是否猜對
    if (num === randomNum) {
        document.body.innerHTML = `<h2>Congrats! You have guessed the number! <br>It was ${num}</h2><button class="play-again" id="play-again">Play Again</button>`
    } else if (num > randomNum) {
        msgEl.innerHTML += '<div>GO LOWER</div>';
    } else {
        msgEl.innerHTML += '<div>GO HIGHER</div>';
    }
}

//這邊+1因為Math.random*100數字只到99不會到100所以必須做這個動作
const randomNum = Math.floor(Math.random() * 100) + 1;

//把答案呈現在頁面上以便確認功能
console.log(randomNum);

// 檢查隨機數字有無正常生成
// console.log(randomNum);

//引入聲音辨識進來window
window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition

let recognition = new SpeechRecognition();

//start recogniiton and game
recognition.start();


//speak result
recognition.addEventListener('result', onSpeak)

//當猜一次後(沒有答對)讓遊戲繼續
recognition.addEventListener('end', () => recognition.start());

//搭遊戲答對會出現reload按鈕設置事件click並且判斷其id是否為play-again是的話畫面reload
document.body.addEventListener('click', (e) => {

    // 因為這邊的id是只有答對後才出現所以抓取事件在整個body上面所以必須選取其中的target.id才有辦法明確的抓到這個按鈕
    if (e.target.id == 'play-again') {
        window.location.reload();
    }
})
```
