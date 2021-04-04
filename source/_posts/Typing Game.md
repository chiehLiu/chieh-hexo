---
title: 實作練習-Typing Game
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Typing Game- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個挑戰打字速度遊戲

## 成品:

![](https://i.imgur.com/VY0QxRT.png)

[成品網址](https://chiehliu.github.io/git-projects/Typing-Game/)

## 成品功能:

1.可以在中間的空格打字比對題目是否正確 2.中間空格左上角有倒數計時右邊會顯示分數(都是即時反應) 3.當遊戲失敗會顯示不一定的圖示，顯示得到幾分並且有一個 Reload 按鈕重啟遊戲 4.瀏覽器中間上方有一個選取難度的下拉式選單 5.左下角有個設定按鈕可以決定"設定"是否出現(決定難度的地方)

# HTML

## 上 CSS 之前的 HTML:

![](https://i.imgur.com/bZacXa7.png)

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.11.2/css/all.min.css"
      integrity="sha256-+N4/V/SbAFiW1MPBCXnfnP9QSN3+Keu+NlB+0ev/YKQ="
      crossorigin="anonymous"
    />
    <link rel="stylesheet" href="style.css">
    <title>Speed Typer</title>
</head>
<body>
    <button id="settings-btn" class="setting_btn">
        <i class="fas fa-cog"></i>
    </button>
    <div id="settings" class="settings">
        <form id="settings-form">
            <div>
                <label for="difficulty">Difficulty</label>
                <select id="difficulty">
                    <option value="easy"></option>
                    <option value="medium"></option>
                    <option value="hard"></option>
                </select>
            </div>
        </form>
    </div>

    <div class="container">
        <h2>👩‍💻 Speed Typer 👨‍💻</h2>
        <small>Type the following:</small>

        <h1 id="word"></h1>

        <input type="text" id="text" autocomplete="off" placeholder="Type the word here...">

        <!-- 這邊的內容會由JS操作 -->
        <p class="time-container">
            Time left: <span id="time">10s</span>
        </p>

        <!-- 這邊的內容會由JS操作 -->
        <p class="score-container">
            Score: <span id="score">0</span>
        </p>

        <!-- 這邊的內容會由JS操作 -->
        <div id="end-game-container" class="end-game-container"></div>
    </div>

    <script src="script.js"></script>
</body>
</html>
```

# CSS:

## CSS 設置好的樣式

![](https://i.imgur.com/VY0QxRT.png)

## CSS 完整程式碼

```css=
 * {
    box-sizing: border-box;
}

body {
    background-color: #2c3e50;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: Verdana, Geneva, Tahoma, sans-serif;

}

/* 全部btn的設定 */
button {
    cursor: pointer;
    font-size: 14px;
    border-radius: 4px;
    padding: 5px 15px;
}

select {
    width: 200px;
    padding: 5px;
    border-radius: 0;
    background-color: #a7c5e3;
}


select:focus,
button:focus {
    outline: 0;
}


/* 設定按鈕定位 */
.settings-btn {
    position: absolute;
    bottom: 30px;
    left: 30px;
}

/* 最上方的難度選擇區 */
.settings {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.3);
    height: 70px;
    color: #fff;
    display: flex;
    justify-content: center;
    align-items: center;

    /* 這邊要做往上移動的特效 */
    transform: translateY(0%);
    transition: transform 0.3s ease-in-out;
}

/* 這邊使用JS操作點擊左下設定按鈕後才會加入這個class */
.settings.hide {
    transform: translateY(-100%);
}


/* 遊戲區域 */

.container {
    background-color: #34495e;
    padding: 20px;
    border-radius: 4px;
    box-shadow: 0 3px 5px rgba(0, 0, 0, 0.3);
    color: #fff;

    /* 這邊設置relative是因為等下要設置分數以及時間的定位在上面 */
    position: relative;
    text-align: center;
    width: 500px;

}


h2 {
    background-color: rgba(0, 0, 0, 0.3);
    padding: 8px;
    border-radius: 4px;
    margin: 0 0 40px;
}


/* 同步顯示文字區域 */
h1 {
    margin: 0;
}

/* 輸入文字區 */
input {
    border: 0;
    border-radius: 4px;
    font-size: 14px;
    width: 300px;
    padding: 12px 20px;
    margin-top: 10px;
}

/* 這邊的內容會由JS操作來顯示分數 */
.score-container {
    position: absolute;
    top: 60px;
    right: 20px;
}

/* 這邊的內容會由JS操作來顯示時間 */
.time-container {
    position: absolute;
    top: 60px;
    left: 20px;
}

/* 遊戲結束時才會轉到這邊 */
.end-game-container {
    background-color: inherit;
    display: none;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    z-index: 1;
}
```

小補充:

無

# JS:

## 變數設置

### word

抓取顯示題目的區域
![](https://i.imgur.com/MVts9WW.png)

### text

抓取輸入答案的區域
![](https://i.imgur.com/DjkxewL.png)

### socreEl

抓取顯示分數的區域
![](https://i.imgur.com/uJNwdSL.png)

### timeEl

抓取顯示時間的區域
![](https://i.imgur.com/8nIaOW3.png)

### endgameEl

遊戲結束時覆蓋整個區域的`<div>`
![](https://i.imgur.com/fD0IpMh.png)

### settingBtn

抓取設定按鈕的區域- 當點擊時會讓難易度下拉式選單顯示或是消失
![](https://i.imgur.com/AbXanUJ.png)

### settings

抓取整個上方區塊- 用來對應點擊設定按鈕後難易度視窗的顯示或是消失
![](https://i.imgur.com/OJ53bQb.png)

### settingsForm

抓取難易度區塊- 使用 change 事件把 difficulty 存取到 localStorage 裡面
![](https://i.imgur.com/xfUBqgN.png)

### difficultySelect

抓取內部的下拉式選單內容- 被 localStorage 重新賦值或是如果為空的話則預設 medium
![](https://i.imgur.com/RjeaHBD.png)

## functions:

- 初始化題目
- 初始化分數
- 初始化時間
- 初始化難易度 - 這邊使用三元邏輯判斷如果 LS 內容不為空則顯示內容不然就預設 medium
- 把 LS 的紀錄重新賦值給 difficultySelect
- 設定進入頁面的 Focus
- 設定更新時間(倒數時間)的間隔為一秒

```javascript=
//init word
let randomWord;

//init score
let score = 0;

//init time
let time = 10;

//LS資料當不為空的時候存取剛剛存取的下拉式選單的值不然就顯示medium當作初始值
// init difficulty and set difficulty to value in LS or medium
let difiiculty = localStorage.getItem('difficulty') !== null ? localStorage.getItem('difficulty') : 'medium';

//把LS的紀錄的值放進去選單裡面直接重新賦值
// set difficulty select value
difficultySelect.value = difiiculty;


//當進入頁面就直接可以focous在input區域不需要移動鼠標過去(focous on text on start)
text.focus();

//每秒數一次(start counting down)
// 使用setInterval來每秒使用一次updateTime也就是更新時間
const timeInterval = setInterval(updateTime, 1000);
```

- `getRandomWord()` - 使用數學方法來隨機的抽取題目
- `addWordToDOM()` - 把抽取到的題目呈現到 DOM 上
- `updateScore()` - 更新分數蠻值觀的就直接 socre++
- `updateTime()`- 更新時間也是使用 time++不過重點是要避免超過 0 秒所以要加入判斷式終止倒數並且使用`gameOver()`
- `gameOver()`- 做出遊戲結束時的頁面並且修改 class 為 flex 讓頁面可以呈現

```javascript=
//隨機取陣列中物件的方法
function getRandomWord() {

    // 用random會隨機給1~0之間的數字乘上words的長度也就是個數再取整數就可以用來找words裡面的內容
    return words[Math.floor(Math.random() * words.length)];
}

//把剛剛抓出來的word的內容貼到DOM上面去(add word to DOM)
function addWordToDOM() {

    randomWord = getRandomWord();
    word.innerHTML = randomWord;
}

//直接把數字加一因為函式放在判斷式中並且已經判斷答對了(update score)
function updateScore() {
    score++;
    scoreEl.innerHTML = score;
}

//update time
function updateTime() {
    time--;
    timeEl.innerHTML = time + "s";

    if (time === 0) {
        // 當time===0時，把timeinterval消除就不會數到負數去了
        clearInterval(timeInterval);

        //結束遊戲(end game)
        gameOver();
    }
}

//做出遊戲結束時的頁面並且修改class為flex讓頁面可以呈現(game over show end screen)
function gameOver() {
    endgameEl.innerHTML = `
    <h1>Time ran out</h1>
    <p>Your final score is ${score}</p>
    <button onclick = "location.reload()">Reload</button>`;

    endgameEl.style.display = "flex";
}
```

## 事件監聽

### text

也就是 input 區域，當輸入的文字符合題目時:

- 顯示下一題答案
- 更新加分的分數
- 清空上一題的內容
- 判斷當下的難度後選擇要加多少秒數
- 更新時間

```javascript=
//typing
text.addEventListener('input', e => {
    const insertedText = e.target.value;

    if (insertedText === randomWord) {

        //當答案符合則顯示下一題題目
        addWordToDOM()

        //答對加分更新分數上去
        updateScore();

        //當答案符合則清空內容(clear)
        e.target.value = '';

        //對應當下的難度加時間
        if (difiiculty === 'hard') {
            time += 2;
        } else if (difiiculty === 'medium') {
            time += 3;
        } else {
            time += 5;
        }

        // 最後更新時間
        updateTime();
    }
})
```

### settingBtn

當點擊設定按鈕![](https://i.imgur.com/gj6CgmZ.png)
讓難易度選擇區塊顯示或隱藏
![](https://i.imgur.com/jvgdMHi.gif)

```javascript=
//讓難易度選擇區塊顯示或隱藏(settings btn click)
settingBtn.addEventListener('click', () => settings.classList.toggle('hide'));
```

### settingForm

當下拉式選單的值改變時存進去 localStorage 當下的 diffuculty 的值

```javascript=
//當下拉式選單的值改變時存進去LS當下的diffuculty
// setting select
settingsForm.addEventListener('change', e => {
    difficulty = e.target.value;
    localStorage.setItem('difficulty', difficulty);
})
```

## JS 完整程式碼:

```javascript=
const word = document.getElementById('word');
const text = document.getElementById('text');
const scoreEl = document.getElementById('score');
const timeEl = document.getElementById('time');
const endgameEl = document.getElementById('end-game-container');
const settingBtn = document.getElementById('settings-btn');
const settings = document.getElementById('settings');
const settingsForm = document.getElementById('settings-form');
const difficultySelect = document.getElementById('difficulty')

const words = [
    'sigh',
    'tense',
    'airplane',
    'ball',
    'pies',
    'juice',
    'warlike',
    'bad',
    'north',
    'dependent',
    'steer',
    'silver',
    'highfalutin',
    'superficial',
    'quince',
    'eight',
    'feeble',
    'admit',
    'drag',
    'loving'
];

//init word
let randomWord;

//init score
let score = 0;

//init time
let time = 10;

//LS資料當不為空的時候存取剛剛存取的下拉式選單的值不然就顯示medium當作初始值
// init difficulty and set difficulty to value in LS or medium
let difiiculty = localStorage.getItem('difficulty') !== null ? localStorage.getItem('difficulty') : 'medium';

//把LS的紀錄的值放進去選單裡面直接重新賦值
// set difficulty select value
difficultySelect.value = difiiculty;


//當進入頁面就直接可以focous在input區域不需要移動鼠標過去(focous on text on start)
text.focus();

//每秒數一次(start counting down)
// 使用setInterval來每秒使用一次updateTime也就是更新時間
const timeInterval = setInterval(updateTime, 1000);

//隨機取陣列中物件的方法
function getRandomWord() {

    // 用random會隨機給1~0之間的數字乘上words的長度也就是個數再取整數就可以用來找words裡面的內容
    return words[Math.floor(Math.random() * words.length)];
}

//把剛剛抓出來的word的內容貼到DOM上面去(add word to DOM)
function addWordToDOM() {

    randomWord = getRandomWord();
    word.innerHTML = randomWord;
}

//直接把數字加一因為函式放在判斷式中並且已經判斷答對了(update score)
function updateScore() {
    score++;
    scoreEl.innerHTML = score;
}

//update time
function updateTime() {
    time--;
    timeEl.innerHTML = time + "s";

    if (time === 0) {
        // 當time===0時，把timeinterval消除就不會數到負數去了
        clearInterval(timeInterval);

        //結束遊戲(end game)
        gameOver();
    }
}

//做出遊戲結束時的頁面並且修改class為flex讓頁面可以呈現(game over show end screen)
function gameOver() {
    endgameEl.innerHTML = `
    <h1>Time ran out</h1>
    <p>Your final score is ${score}</p>
    <button onclick = "location.reload()">Reload</button>`;

    endgameEl.style.display = "flex";
}

//這裡必須寫在外面呼叫第一次當作預設值
addWordToDOM();


//event lisenter

//typing
text.addEventListener('input', e => {
    const insertedText = e.target.value;

    if (insertedText === randomWord) {

        //當答案符合則顯示下一題題目
        addWordToDOM()

        //答對加分更新分數上去
        updateScore();

        //當答案符合則清空內容(clear)
        e.target.value = '';

        //對應當下的難度加時間
        if (difiiculty === 'hard') {
            time += 2;
        } else if (difiiculty === 'medium') {
            time += 3;
        } else {
            time += 5;
        }

        // 最後更新時間
        updateTime();
    }
})

//讓難易度選擇區塊顯示或隱藏(settings btn click)
settingBtn.addEventListener('click', () => settings.classList.toggle('hide'));

//當下拉式選單的值改變時存進去LS當下的diffuculty
// setting select
settingsForm.addEventListener('change', e => {
    difficulty = e.target.value;
    localStorage.setItem('difficulty', difficulty);
})
```
