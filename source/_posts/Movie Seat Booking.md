---
title: 實作練習-Movie Seat Booking
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Movie Seat Booking - 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個電影定位動態表格

## 成品:

![](https://i.imgur.com/UlZtyQu.png)

[成品網址](https://chiehliu.github.io/git-projects/Movie%20seat%20booking/index.html)

## 成品功能:

1.最上方處可以選擇電影 2.可以選取尚未被占走(occupied)的位置 3.並且加總最後選取幾個位置以及消費總金額

## HTML

- 下拉式電影選單
- 標示座位狀態的`li`
- 六排座位區的呈現(有些空的有些被占走)
- 標示總共買了幾個位置以及總消費金額

### 上 CSS 之前的 HTML:

![](https://i.imgur.com/oRTbken.png)

### 程式碼:

```htmlembedded=
 <body>
    <div class="movie-container">
      <label>Pick a movie</label>

<!--使用下拉式選單tag`select` 以及 他的選項tag`option`製作可選取的電影清單 -->
      <select id="movie">
        <option value="10">Avengers:Endgame ($10)</option>
        <option value="12">Joker ($12)</option>
        <option value="8">Toy Story 4 ($8)</option>
        <option value="9">The Lion King ($9)</option>
      </select>
    </div>

    <!--這邊三個tag`li`是圖片標示代表座位的狀態 -->
    <ul class="showcase">
      <li>
        <div class="seat"></div>
        <small>N/A</small>
      </li>
      <li>
        <div class="seat selected"></div>
        <small>Selected</small>
      </li>
      <li>
        <div class="seat occupied"></div>
        <small>Occupied</small>
      </li>
    </ul>

<!-- 這邊的container是等下要成像的座位區的部分
    class有分兩總seat 以及 seat occupied 會呈現不同的CSS去修飾 -->
    <div class="container">
      <div class="screen"></div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
      </div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat occupied"></div>
        <div class="seat occupied"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
      </div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat occupied"></div>
        <div class="seat occupied"></div>
      </div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
      </div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat occupied"></div>
        <div class="seat occupied"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
      </div>
      <div class="row">
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat"></div>
        <div class="seat occupied"></div>
        <div class="seat occupied"></div>
        <div class="seat occupied"></div>
        <div class="seat"></div>
      </div>
    </div>

<!--最後這邊顯示總共買了幾個位置以及消費總金額並設置tag`span`待會做JS處理 -->
    <p class="text">
      You have selected <span id="conunt">0</span> seat for a price of
      <span id="total">$0</span>
    </p>

    <script src="script.js"></script>
  </body>
```

## CSS:

### 字體輸出

引入字體的部分要先點選你要的字體粗細大小後，點擊右上角綠色框框會跳出右邊視窗告訴你選了那些字體大小的選項後，點選下方紅框框處的@import 輸出成網址就可以使用瞜!
![](https://i.imgur.com/EZNXyLq.png)

### CSS 設置好的樣式

![](https://i.imgur.com/UlP97qm.png)

### 程式碼

```css=
/* 字體輸出的網址部分 */
@import url('https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap');

/* 讓margin padding boder不礙事的全域 box-sizing:border-box*/
* {
    box-sizing: border-box;
}

/* 把這邊設為flex 好處理全部物件置中 */
body {
    background-color: #242333;
    display: flex;
    flex-direction: column;
    color: #fff;
    align-items: center;
    justify-content: center;
/*一樣設置滿版 */
    height: 100vh;
    font-family: 'Lato', sans-serif, ;
    margin: 0;
}


/* pick a movie區域 */
.movie-container select {
    background-color: #fff;
    border: 0;
    border-radius: 5px;
    font-size: 14px;
    margin-left: 10px;
    padding: 5px 15px 5px 15px;

/*這邊因為我是windows系統可以不處理這邊但作者的會被影響padding所以做這個處理*/
    -moz-appearance: none;
    -webkit-appearance: none;
    appearance:none;
}

.container {
/*  perspective立體感數字越高越立體 */
    perspective: 1000px;
    margin-bottom: 30px;
}

/* 設置border-radius左右讓標示看起來像座墊 */
.seat {
    background-color: #444451;
    height: 12px;
    width: 15px;
    margin: 3px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

/* 當座位被選擇的時候顯示這個顏色 */
.seat.selected {
    background-color: #6feaf6;
}

/* 這些是原本就被占據的座椅的顏色 */
.seat.occupied {
    background-color: #fff;
}

/* 選取座位區第二個元素並使用margin-left把走道做出來 */
.seat:nth-of-type(2) {
    margin-right: 18px;
}
/* 選取倒數第二個處理走道 */
.seat:nth-last-of-type(2) {
    margin-left: 18px;
}

/* 滑到空位座椅就會放大並且滑鼠變成指標 */
.seat:not(.occupied):hover {
    cursor: pointer;
    transform: scale(1.2);
}

/* 這邊是被占走的位置所以滑鼠滑過他們時不做特效 */
.showcase .seat:not(.occupied):hover {
    cursor: default;
    transform: none;
}


.showcase {
/* 這邊最後面的數值是alpha值處理透明度:1不透明 0透明 */
    background-color: rgba(0, 0, 0, 0.1);
    padding: 5px 10px;
    border-radius: 5px;
    color: #777;
/*  這個可以消除li的圓點點 */
    list-style-type: none;
    display: flex;
/*  讓標示中間有空間 */
    justify-content: space-between;
}

/* 一樣套flex做全置中 */
.showcase li {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 10px;
}


.showcasse li small {
    margin-left: 2px;
}

/* 這條flex讓整個座位區成行非常重要 */
.row {
    display: flex;
}


/* rotateX以X為軸心旋轉 */
.screen {
    background-color: #fff;
    height: 70px;
    width: 100%;
    margin: 15px 0;
    transform: rotateX(-45deg);
    box-shadow: 0 3px 10pc rgba(255, 255, 255, 0.7);
}

p.text {
    margin: 5px 0;
}

p.text span {
    color: #6feaf6;
}
```

小補充:

[`appearance` `-moz-appearance` `-webkit-appearance` 根據不同作業系統使用的套件 MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/appearance)

[perspective 透視感 立體感 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/perspective)

[rotateX() 以 X 為軸心旋轉 MDN](<https://developer.mozilla.org/en-US/docs/Web/CSS/transform-function/rotateX()>)

[:nth-of-type 選取第()個元素 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:nth-of-type)

rgba(red 值, green 值, blue 值, alpha 值)- alpha 值代表透明度

![](https://i.imgur.com/KCxbV8i.png)

## JS:

JS 主要實現幾個部分:

- 儲存 movie index 以及 price 並放在 localstorage
  從 localstorage 取得儲存的資料以及填充回去 UI
  讓網頁在重新整理之後資料都還存在

- 讓作品下方的文字隨著內容作更動
  例如:選了三個位置藍色並且顯示多少錢
  ![](https://i.imgur.com/alMVVWO.png)

- 事件監聽得部分

處理點擊座椅會有藍色特效再次點擊會關閉特效

電影選擇事件(下拉式選單)觸發下面兩個 function:
![](https://i.imgur.com/4YtdY1K.png)

1. `setMovieData()`會處理下拉式選單選到的電影的 Index 號碼以及價錢並且儲存在 localstorage 上
2. `updateSelectedCount()` 會因應選取的電影票價(value)去改變 消費總金額

```javascript=
const container = document.querySelector('.container');
//querySelectorAll會把抓取到的物件轉成nodeList(類似array) 可以使用一些arrays methods
const seats = document.querySelectorAll('.row .seat:not(.occupied');
const count = document.getElementById('count');
const total = document.getElementById('total');
const movieSelect = document.getElementById('movie');

//把儲存的資料放上去UI
populateUI();


// 這邊ticketPrice必須使用let指派變數因為票價會隨著電影不同改變(不過在這個部分的設置只是讓他初始化要在後面的事件監聽才會針對電影做價錢更改)
//+的使用確保這邊出來的value為number
let ticketPrice = +movieSelect.value;



//Save selected movie index and price 儲存movie index以及price並放在localstorage
function setMovieData(movieIndex, moviePrice) { //這兩個參數代表(e.target.selectedIndex, e.target.value)

    //這部分因為moviePrice是字串所以不需要轉換 movieIndex使用上面不需要轉換成array 所以都沒有使用stringify
    //setItem使用鍵值對，傳上去localstorage
    localStorage.setItem('selectedMovieIndex', movieIndex);
    localStorage.setItem('selectedMoviePrice', moviePrice);
}



//計算幾個位置 以及 改變總金額 (Update total and count)
function updateSelectedCount() {

    // 這邊會把所有使用者點擊變成藍色的座椅使用nodeList呈現出來(ps.如果不加上.row，會連標示區域那個藍色的座位一起抓進去，所以要記得加上去.row)
    const selectedSeats = document.querySelectorAll('.row .seat.selected');

    //把藍色座位選取後出現的nodeList轉換成array (Copy seleted seats into array)
    //使用map方法印出array (Map through array)
    //並且使用indexOf方法回傳seat的索引(return a new array indexes)

    // 展開運算子(...)，這邊使用[...selectedSeats]代表把seletedSeats的值全部傳入進去[]讓他變成array
    //之後使用map印出每個一個藍色座位(被選擇的)之後返回從所有座位中使用搜尋檢索號碼(indexOf)
    const seatsIndex = [...selectedSeats].map(seat => [...seats].indexOf(seat));

    //這邊的localstorage會創造一個鍵值對(key, value)在application的localstorage可以看到
    //注意這邊使用stringfy轉換成字串才能存在localstorage上面(鍵值名稱和值皆為字串型式)
    localStorage.setItem('selectedSeats', JSON.stringify(seatsIndex));

    // 取得nodeList的長度也就是使用者點擊了幾次就可以知道了
    const selectedSeatsCount = selectedSeats.length;

    //這邊要改變作品下方那排的text所以使用innerTextx(You have selected 0 seats for a price of $0)
    count.innerText = selectedSeatsCount; //使用者點擊了幾次
    total.innerText = selectedSeatsCount * ticketPrice; //這邊乘上票價就是總金額
}



// 從localstorage取得儲存的資料以及填充回去UI(get data from localstorage and populate UI)

function populateUI() {

    //這邊使用parse把JSON資料轉換array回來，使用getItem到我們要使用的key也就是剛剛我們設定的'selectedSeats'並且指派給變數selectedSeats
    //往下做判斷式處理讓藍色座椅繼續留著，因為localstorage裡面儲存的資料符合條件
    const selectedSeats = JSON.parse(localStorage.getItem('selectedSeats'));

    //如果array selectedSeats不為空以及selectedSeats.length大於0則跑下面判斷式
    if (selectedSeats !== null && selectedSeats.length > 0) {

        //把所有座位使用forEach一個個印出並且判斷每個座位的index號碼是否跟selectedSeats的一樣，如果一樣則執行加上selected這個class
        seats.forEach((seat, index) => {
            if (selectedSeats.indexOf(index) > -1) {
                seat.classList.add('selected');
            }
        });
    }

    //這邊跟上面做類似的事情，判斷selectedMovieIndex是否為空，不為空則執行重新賦值給selectedMovieIndex下拉式選單選取的電影index
    const selectedMovieIndex = localStorage.getItem('selectedMovieIndex');

    if (selectedMovieIndex !== null) {
        movieSelect.selectedIndex = selectedMovieIndex;//這邊的selectedIndex是個方法取得select底下option tag的index
    }
}


//電影選擇事件(Movie Select Event)

//使用change事件 當下拉式選單value改變並且在提交的時候觸發(完成更換電影主題的時候提交)，ticketPrice的內容變成當下選擇的value並且上(+)確保其為number
//這邊會觸發兩個function
//1. setMovieData會處理下拉式選單選到的電影的Index號碼以及價錢並且儲存在localstorage上
//2. updateSelectedCount 會因應選取的電影票價(value)去改變 消費總金額
movieSelect.addEventListener('change', e => {

    // 要讓下拉選單在選擇某個電影價錢(value)的情況下，同時更改讓updateSelectedCount 這個function 做的加總部分乘上去的tickePrice符合現在選擇的電影票價
    ticketPrice = +e.target.value;

    //這部分會取得當下選取座位的index號碼以及票價(value並且是字串)並且儲存在localstorage上
    setMovieData(e.target.selectedIndex, e.target.value);//這邊的selectedIndex是個方法取得select底下option tag的index

    //這邊呼叫updateSelectedCount function會改變當下選取的消費總金額因應選取的電影場次的不同(value的不同)
    updateSelectedCount();
})


// seat click event 這邊處理點擊座椅會有藍色特效
container.addEventListener('click', e => {

    // 如果點擊事件的class包含seat以及點擊事件的class不包含occupied才可以執行下方程式碼
    if (e.target.classList.contains('seat') && !e.target.classList.contains('occupied')) {

        // 這邊使用toggle才可以開關，點擊一次開第二次關(開關的過程是處理selected是否加上去)
        e.target.classList.toggle('selected');

        //呼叫updateSelectedCount function，會因應事件更新座位以及消費總金額
        updateSelectedCount();
    }
})


//initial count and total set(讓顯示座位數量以及總金額的部分重新整理後持續顯示)
//會直接顯示出這個function的內容而不需要經過事件觸發保持讓事件重新整理後持續顯示

updateSelectedCount();
```

小補充:

[Spread syntax (...) MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

[selectedIndex MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLSelectElement/selectedIndex)

[localStorage MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/Window/localStorage)

[change 事件](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/change_event)
