---
title: 實作練習-Music Player
date: 2019-07-0521:27:59
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Music Player- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個音樂撥放器 使用 html CSS 以及 audio API

## 成品:

![](https://i.imgur.com/Ngco0dU.png)

[成品網址](https://chiehliu.github.io/git-projects/Music-Player/index.html)

## 成品功能:

1.點擊中間的撥放後左邊的唱盤會開始旋轉 2.並且上方會跳出視窗顯示歌名 3.點擊上一首下一首會直接跳轉 4.在暫停狀態下點擊上一首或是下一首會直接撥放並且跳出視窗顯示歌名

---

# HTML:

## 上 CSS 之前的 HTML:

![](https://i.imgur.com/DJNwyLu.png)

## html 程式碼:

```htmlembedded=
<body>
    <h1>Music Player</h1>

    <!-- 專輯名稱、進度條(progress bar)包裹住它們的是music-info -->
    <div class="music-container" id="music-container">
      <div class="music-info">

        <!-- 專輯名稱 -->
        <h4 id="title"></h4>

        <!-- 進度條 -->
        <div class="progress-container" id="progress-container">
          <div class="progress" id="progress"></div>
        </div>

      </div>

      <!-- 專輯音檔 -->
      <!-- 這邊的來源先放著待會要修飾CSS之後會變成動態的操作JS(可以切換歌曲) -->
      <audio src="music/ukulele.mp3" id="audio"></audio>

      <!-- 專輯封面 -->
      <div class="img-container">
        <!-- 這邊的來源先放著待會要修飾CSS之後會變成動態的操作JS(切換歌曲時cover也會改) -->
        <img src="images/ukulele.jpg" alt="music-cover" id="cover" />
      </div>

      <!-- 按鍵區域 -->
      <div class="navigation">

        <button id="prev" class="action-btn">
          <i class="fas fa-backward"></i>
        </button>
        <button id="play" class="action-btn action-btn-big">
          <i class="fas fa-play"></i>
        </button>
        <button id="next" class="action-btn">
          <i class="fas fa-forward"></i>
        </button>
      </div>
    </div>

    <script src="script.js"></script>
  </body>
```

小補充:

[audio-MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/audio)

---

# CSS:

## 相關 CSS 設定:

- 背景使用漸層色處理
- 讓封面(cover)旋轉使用 animation
- 使用偽元素做出封面圓點
- 包含專輯名稱、進度條的跳出視窗做 transition 處理
- 進度條的 CSS 設置

### 背景使用漸層色處理

linear-gradient(產生位置角度,顏色 1 顏色 2) 後面%數代表梯度(顏色漸變的層度)

[linear-gradient -w3cschool](https://www.w3schools.com/css/css3_gradients.asp)

```css
background-image: linear-gradient(
  0deg,
  rgba(247, 247, 247, 1) 23.8%,
  rgba(252, 221, 221, 1) 92%
);
```

### CSS animation

![](https://i.imgur.com/3IFpISV.png)

CSS animaiton 縮寫順序:
animation: name | duration | timing-function | delay | iteration-count | direction | fill-mode | play-state;

### keyframes

animation 的動作是來自於 CSS style 逐步的改變有兩種做法

- 0~100%的時間甚麼樣的 style 做甚麼事情
- from to 擺入不同的 css style 去做動畫(本專案使用這個)
- ![](https://i.imgur.com/cdDkfcv.png)

![](https://i.imgur.com/4cclgm8.png)

```css=
.img-container img {
  border-radius: 50%;
  object-fit: cover;
  height: 110px;
  width: inherit;
  position: absolute;
  bottom: 0;
  left: 0;

  /* 動畫設置縮寫: 動畫名稱:rotate 延續3s轉一整圈  線性的加速度 無限重複*/
  animation: rotate 3s linear infinite;

  /* 控制動畫的播放狀態其實也可以放進縮寫裡面 : 先設定暫停待會用JS開啟*/
  animation-play-state: paused;
}

/* 必須使用JS才會切換到這個play狀態 預設設定上面cover是不會跑的 */
.music-container.play .img-container img {
  animation-play-state: running;
}
/* animation裡面的動畫設定可以寫在這邊from到to是一整段動畫過程中使用的元素 */
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

### 偽元素製作圓心

唱盤指針 使用 CSS 偽元素做出子元素圓點當作指針並且做定位

[偽元素 -MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/::after)

```css
.img-container {
  position: relative;
  width: 110px;
}

/* 唱盤指針 使用CSS 偽元素做出子元素圓點當作指針*/
.img-container::after {
  content: "";
  background-color: #fff;
  border-radius: 50%;
  position: absolute;
  bottom: 100%;
  left: 50%;
  width: 10px;
  height: 10px;
  transform: translate(-50%, 50%);
}
```

### CSS transition

CSS Transition 縮寫順序: property | duration | timing-function | delay

```css=
/* 包含專輯名稱、進度條的跳出視窗 */
.music-info {
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 15px 15px 0 0;
  position: absolute;
  top: 0;
  left: 20px;
  /* 這邊calc是指100%的width減去40px寬度就是取得的width */
  width: calc(100% - 40px);
  padding: 10px 10px 10px 150px;

  /*JS控制出場前顯示透明 */
  opacity: 0;

  transform: translateY(0%);
  /* 使用transform特效時觸發transition 的修飾秒數以及加速度特效*/
  /* 這邊後半部的opacity是另外的不算在transition的縮寫裡面喔! */
  /* transition 後方的0.3s 以及ease-in修飾transform特效 */
  transition: transform 0.3s ease-in, opacity 0.3s ease-in;

  /* JS控制出廠前先壓在最底層 */
  z-index: 0;
}

  /* JS控制出場後顯示1 */
.music-container.play .music-info {
  opacity: 1;
  transform: translateY(-100%);
}
```

### 專輯進度條 CSS 處理

使用 transition: width 0.1s linear

改變 width 讓寬度改變就會像一般撥放軟體再跑進度條一樣顯示了

```css=
.progress {
  background-color: #fe8daa;
  border-radius: 5px;
  height: 100%;
  /* 這邊的width要用JS控制因為它是音樂進行的進度條 */
  width: 0%;
  transition: width 0.1s linear;
}
```

## CSS 設置好的樣式

![](https://i.imgur.com/P6WNHbo.png)

## CSS 完整程式碼

```css=
 @import url("https://fonts.googleapis.com/css?family=Lato&display=swap");

/* 全域設定 */
* {
  box-sizing: border-box;
}

body {
  /* linear-gradient(位置,顏色1顏色2) 後面%數代表梯度(顏色漸變的層度) */
  background-image: linear-gradient(
    0deg,
    rgba(247, 247, 247, 1) 23.8%,
    rgba(252, 221, 221, 1) 92%
  );
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  font-family: "Lato", sans-serif;
  margin: 0;
}

.music-container {
  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0 20px 20px rgba(252, 169, 169, 0.6);
  display: flex;
  padding: 20px 30px;
  position: relative;
  margin: 100px 0;
  /* z-index較大數值的元素會覆蓋其他的較小的數值的z-index */
  z-index: 10;
}

.img-container {
  position: relative;
  width: 110px;
}

/* 唱盤指針 使用CSS 偽元素做出子元素圓點當作指針*/
.img-container::after {
  content: "";
  background-color: #fff;
  border-radius: 50%;
  position: absolute;
  bottom: 100%;
  left: 50%;
  width: 10px;
  height: 10px;
  transform: translate(-50%, 50%);
}

.img-container img {
  border-radius: 50%;
  object-fit: cover;
  height: 110px;
  /* 使用inherit會繼承到他parent的width也就是img-container width:110 */
  width: inherit;
  position: absolute;
  bottom: 0;
  left: 0;

  /* 動畫設置縮寫: 動畫名稱:rotate 延續3s轉一整圈  線性的加速度 無限重複*/
  animation: rotate 3s linear infinite;

  /* 控制動畫的播放狀態其實也可以放進縮寫裡面 : 先設定暫停待會用JS開啟*/
  animation-play-state: paused;
}

/* 必須使用JS才會切換到這個play狀態 預設設定上面cover是不會跑的 */
.music-container.play .img-container img {
  animation-play-state: running;
}

/* animation裡面的動畫設定可以寫在這邊from到to是一整段動畫過程中使用的元素 */
@keyframes rotate {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}

.navigation {
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
}

.action-btn {
  background-color: #fff;
  border: 0;
  color: #dfdbdf;
  font-size: 20px;
  cursor: pointer;
  padding: 10px;
  margin: 0 20px;
}

.action-btn.action-btn-big {
  color: #cdc2d0;
  font-size: 30px;
}

/* 當點擊取得焦點後移除邊框 */
.action-btn:focus {
  outline: 0;
}

.music-info {
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 15px 15px 0 0;
  position: absolute;
  top: 0;
  left: 20px;
  /* 這邊calc是指100%的width減去40px寬度就是取得的width */
  width: calc(100% - 40px);
  padding: 10px 10px 10px 150px;
  opacity: 0;
  transform: translateY(0%);
  transition: transform 0.3s ease-in, opacity 0.3s ease-in;
  z-index: 0;
}

.music-container.play .music-info {
  opacity: 1;
  transform: translateY(-100%);
}

.music-info h4 {
  margin: 0;
}

.progress-container {
  background-color: #fff;
  border-radius: 5px;
  cursor: pointer;
  margin: 10px 0;
  height: 4px;
  width: 100%;
}

.progress {
  background-color: #fe8daa;
  border-radius: 5px;
  height: 100%;
  /* 這邊的width要用JS控制因為它是音樂進行的進度條 */
  width: 0%;
  transition: width 0.1s linear;
}

```

小補充:

`inherit`會繼承到他 parent 的 width 也就是 img-container width:110
width: inherit;

`calc`是指 100%的 width 減去 40px 寬度就是取得的 width
width: calc(100% - 40px);

---

# JS:

## 變數設置

- musicContainer 區域
  ![](https://i.imgur.com/DtbV5Ad.png)

- playBtn,prevBtn,nextBtn 區域
  ![](https://i.imgur.com/rQ8HNKo.png)

- audio 區域
  這部分是音檔嵌入在 html 裡面

- progressContainer 區域
  ![](https://i.imgur.com/PLWVawP.png)

- progress 區域
  裡面的進度條
  ![](https://i.imgur.com/7F6O9D8.png)

- title
  目前藏在 music-container 下方
  ![](https://i.imgur.com/fBUeRLy.png)

- cover
  專輯封面
  ![](https://i.imgur.com/JM4vTK5.png)

- songs
  `['hey', 'summer', 'ukulele']`
  這邊設置歌曲名稱給下面做抓取

- songIndex
  一開始的畫面初始值的 index

```javascript=
const musicContainer = document.getElementById('music-container');

const playBtn = document.getElementById('play');
const prevBtn = document.getElementById('prev');
const nextBtn = document.getElementById('next');

const audio = document.getElementById('audio');
const progress = document.getElementById('progress');
const progressContainer = document.getElementById('progress-container');
const title = document.getElementById('title');
const cover = document.getElementById('cover');


const songs = ['hey', 'summer', 'ukulele'];
let songIndex = 2;

```

## functions:

- 更新專輯名稱
  loadSong

雖然做了更新但是這邊專輯資訊還沒有跳出來

- 撥放暫停相關:
  playSong
  pauseSong

在撥放後才會跳出專輯視窗

- 上一首下一首相關:
  prevSong
  nextSong

這邊也會跳出視窗因為也會撥放歌曲

- 進度條相關
  updatePorgress
  setProgress

```javascript=

//設置好歌名給下面的src作抓取(song title)
const songs = ['hey', 'summer', 'ukulele'];

//設置檢索抓取選到的歌曲對應其images以及音檔
// keep track of song
let songIndex = 2;

//呼叫loadSong重置歌曲的名稱、images以及音檔
//Initiallly load song details into DOM
loadSong(songs[songIndex]);


//重置歌曲的名稱、images以及音檔(update song details)
function loadSong(song) {
    title.innerText = song;
    audio.src = `music/${song}.mp3`;
    cover.src = `images/${song}.jpg`;
}

//play song
function playSong() {

    // 增加play詞墜到musicContainer裡面就可以觸發css animation的動畫
    //讓cover旋轉以及專輯名稱進度條跳上來
    musicContainer.classList.add('play');

    //並且按下play後圖案會改成pause
    playBtn.querySelector('i.fas').classList.remove('fa-play');
    playBtn.querySelector('i.fas').classList.add('fa-pause');

    // 這是audio的方法play可以直接撥放音檔
    audio.play();
}

//pause song
function pauseSong() {

    //去除play詞墜從musicContainer裡面就可以消除css animation的動畫
    //讓cover旋轉以及專輯名稱進度條 關閉
    musicContainer.classList.remove('play');

    //並且按下pause後圖案會改成play
    playBtn.querySelector('i.fas').classList.add('fa-play');
    playBtn.querySelector('i.fas').classList.remove('fa-pause');

    // 這是audio的方法pause可以直接停止音檔
    audio.pause();
}

//上一首點擊之後要撥放上一首歌曲(Previous song)
function prevSong() {

    //每次按上一首songIndex要減一才會跑到上一首
    songIndex--;

    //這邊要判斷當songIndex減到0以下的時候
    // 要回到index2使用length-1也就是3-1=2
    if (songIndex < 0) {
        songIndex = songs.length - 1;
    }

    // 當歌曲轉換自然要更改重置歌曲的名字音檔以及歌名
    loadSong(songs[songIndex]);

    // 以及要直接撥放
    playSong();
}

//下一首點擊之後要撥放下一首歌曲(Next song)
function nextSong() {

    //每次按下一首songIndex要加一才會跑到下一首
    songIndex++;

    //這邊要判斷當songIndex加到超過歌曲長度-1時(也就是全部index都跑完了)
    // 要回到index=0也就是回到第一首
    if (songIndex > songs.length - 1) {
        songIndex = 0;
    }

    // 當歌曲轉換自然要更改重置歌曲的名字音檔以及歌名
    loadSong(songs[songIndex]);

    // 以及要直接撥放
    playSong();
}


// 使progress bar隨歌曲進度更新(update progress bar)
function updateProgress(e) {

    // 解構srcElement出其中的duration以及currentTime
    const {
        duration,
        currentTime
    } = e.srcElement; //duration是整首歌的時間currentTime是過了多久

    //相處之後可以得出現在的進度幾趴就可以轉換成width顯示在progress bar了
    const progressPercent = (currentTime / duration) * 100;
    progress.style.width = `${progressPercent}%`;
}

//滑鼠點擊進度條移動(set progress bar)
function setProgress(e) {


    //this指向progress-container 所以它的width就是216
    const width = this.clientWidth;

    // 這個變數被指派了 滑鼠點擊progress-container身上的位置
    const clickX = e.offsetX;

    const duration = audio.duration; //音檔總時間

    //currentTime是指當下音檔的時間
    //progress bar的進度(是趴數)乘上音檔總時間 就是現在的進度!
    audio.currentTime = (clickX / width) * duration;
}
```

## 事件監聽

- 撥放按鍵
- 上一首下一首
- 讓進度條跟著音檔進度走(監聽時間更新進度事件)
- 滑鼠點擊哪邊進度條走哪邊(監聽點擊事件)
- 歌曲結束(監聽結束事件)

```javascript=
//event listeners

// 這邊的click用來確定現在的音檔狀態是撥放還是暫停
// 如果是撥放則暫停如果是暫停則撥放
playBtn.addEventListener('click', () => {
    const isPlaying = musicContainer.classList.contains('play');

    if (isPlaying) {
        pauseSong();
    } else {
        playSong();
    }
});

//上一首下一首切換change song
prevBtn.addEventListener('click', prevSong);
nextBtn.addEventListener('click', nextSong);


//time/song update(讓進度條隨著音檔跑)
audio.addEventListener('timeupdate', updateProgress);

//處理porgressbar進度條滑鼠點哪邊去哪邊(click on progress bar)
progressContainer.addEventListener('click', setProgress)


//使用ended事件處理audio讓它結束時觸發，並且執行nextSong 函式(song end)
audio.addEventListener('ended', nextSong);

```

小補充:

[Audio currentTime Property MDN](https://www.w3schools.com/Jsref/prop_audio_currenttime.asp)

[Audio duration Property MDN](https://www.w3schools.com/Jsref/prop_audio_duration.asp)

[Ended Event MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement/ended_event)

clientWidth 的範圍:
![](https://i.imgur.com/tSCQ0M5.png)

## JS 完整程式碼:

```javascript=
const musicContainer = document.getElementById('music-container');

const playBtn = document.getElementById('play');
const prevBtn = document.getElementById('prev');
const nextBtn = document.getElementById('next');

const audio = document.getElementById('audio');
const progress = document.getElementById('progress');
const progressContainer = document.getElementById('progress-container');
const title = document.getElementById('title');
const cover = document.getElementById('cover');

//設置好歌名給下面的src作抓取(song title)
const songs = ['hey', 'summer', 'ukulele'];

//設置檢索抓取選到的歌曲對應其images以及音檔
// keep track of song
let songIndex = 2;

//呼叫loadSong重置歌曲的名稱、images以及音檔
//Initiallly load song details into DOM
loadSong(songs[songIndex]);


//重置歌曲的名稱、images以及音檔(update song details)
function loadSong(song) {
    title.innerText = song;
    audio.src = `music/${song}.mp3`;
    cover.src = `images/${song}.jpg`;
}

console.dir(audio);

//play song
function playSong() {

    // 增加play詞墜到musicContainer裡面就可以觸發css animation的動畫
    //讓cover旋轉以及專輯名稱進度條跳上來
    musicContainer.classList.add('play');

    //並且按下play後圖案會改成pause
    playBtn.querySelector('i.fas').classList.remove('fa-play');
    playBtn.querySelector('i.fas').classList.add('fa-pause');

    // 這是audio的方法play可以直接撥放音檔
    audio.play();
}

//pause song
function pauseSong() {

    //去除play詞墜從musicContainer裡面就可以消除css animation的動畫
    //讓cover旋轉以及專輯名稱進度條 關閉
    musicContainer.classList.remove('play');

    //並且按下pause後圖案會改成play
    playBtn.querySelector('i.fas').classList.add('fa-play');
    playBtn.querySelector('i.fas').classList.remove('fa-pause');

    // 這是audio的方法pause可以直接停止音檔
    audio.pause();
}

//上一首點擊之後要撥放上一首歌曲(Previous song)
function prevSong() {

    //每次按上一首songIndex要減一才會跑到上一首
    songIndex--;

    //這邊要判斷當songIndex減到0以下的時候
    // 要回到index2使用length-1也就是3-1=2
    if (songIndex < 0) {
        songIndex = songs.length - 1;
    }

    // 當歌曲轉換自然要更改重置歌曲的名字音檔以及歌名
    loadSong(songs[songIndex]);

    // 以及要直接撥放
    playSong();
}

//下一首點擊之後要撥放下一首歌曲(Next song)
function nextSong() {

    //每次按下一首songIndex要加一才會跑到下一首
    songIndex++;

    //這邊要判斷當songIndex加到超過歌曲長度-1時(也就是全部index都跑完了)
    // 要回到index=0也就是回到第一首
    if (songIndex > songs.length - 1) {
        songIndex = 0;
    }

    // 當歌曲轉換自然要更改重置歌曲的名字音檔以及歌名
    loadSong(songs[songIndex]);

    // 以及要直接撥放
    playSong();
}


// 使progress bar隨歌曲進度更新(update progress bar)
function updateProgress(e) {

    // 解構srcElement出其中的duration以及currentTime
    const {
        duration,
        currentTime
    } = e.srcElement; //duration是整首歌的時間currentTime是過了多久

    //相處之後可以得出現在的進度幾趴就可以轉換成width顯示在progress bar了
    const progressPercent = (currentTime / duration) * 100;
    progress.style.width = `${progressPercent}%`;
}

//滑鼠點擊進度條移動(set progress bar)
function setProgress(e) {


    //this指向progress-container 所以它的width就是216
    const width = this.clientWidth;

    // 這個變數被指派了 滑鼠點擊progress-container身上的位置
    const clickX = e.offsetX;

    const duration = audio.duration; //音檔總時間

    //currentTime是指當下音檔的時間
    //progress bar的進度(是趴數)乘上音檔總時間 就是現在的進度!
    audio.currentTime = (clickX / width) * duration;

}




//event listeners

// 這邊的click用來確定現在的音檔狀態是撥放還是暫停
// 如果是撥放則暫停如果是暫停則撥放
playBtn.addEventListener('click', () => {
    const isPlaying = musicContainer.classList.contains('play');

    if (isPlaying) {
        pauseSong();
    } else {
        playSong();
    }
});

//上一首下一首切換change song
prevBtn.addEventListener('click', prevSong);
nextBtn.addEventListener('click', nextSong);


//time/song update(讓進度條隨著音檔跑)
audio.addEventListener('timeupdate', updateProgress);

//處理porgressbar進度條滑鼠點哪邊去哪邊(click on progress bar)
progressContainer.addEventListener('click', setProgress)


//使用ended事件處理audio讓它結束時觸發，並且執行nextSong 函式(song end)
audio.addEventListener('ended', nextSong);
```
