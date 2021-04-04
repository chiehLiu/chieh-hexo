---
title: 實作練習-Exchange rate
date:
tags: [HTML, CSS, JavaScript, jQuery]
category: Javascript作品
---

# Exchange rate - 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個匯率轉換表

## 成品:

![](https://i.imgur.com/jTjqOnx.png)

[成品網址](https://chiehliu.github.io/git-projects/exchange-rate/index.html)

## 成品功能:

1.可以更改各國的貨幣內容並調整金額 2.可以更換順序 例如 1 美金換 0.81 歐元改成 1 歐元換 1.23 美金 點選 Swap 直接更換 3.有個區域顯示匯率(下圖紅框框處)
![](https://i.imgur.com/LwEcNaG.png) 4.使用 fetch 更新 API 的內容並使用回傳回來的資料修改匯率

# HTML

- 上方大圖
- 一些簡單的文字描述
- 下拉式選單表格
- 更換匯率的按鈕
- 顯示匯率的 div

沒有甚麼太特別的地方

### 上 CSS 之前的 HTML:

![](https://i.imgur.com/cn8LL8N.png)

### 程式碼:

```htmlembedded=
<body>
  <img src="img/money.png" alt="" class="money-img" />
  <h1>Exchange Rate Calculator</h1>
  <p>Choose the currency and the amounts to get the exchange rate</p>

  <div class="container">
    <div class="currency">
      <select id="currency-one">
        <option value="AED">AED</option>
        <option value="ARS">ARS</option>
        <option value="AUD">AUD</option>
        <option value="BGN">BGN</option>
        <option value="BRL">BRL</option>
        <option value="BSD">BSD</option>
        <option value="CAD">CAD</option>
        <option value="CHF">CHF</option>
        <option value="CLP">CLP</option>
        <option value="CNY">CNY</option>
        <option value="COP">COP</option>
        <option value="CZK">CZK</option>
        <option value="DKK">DKK</option>
        <option value="DOP">DOP</option>
        <option value="EGP">EGP</option>
        <option value="EUR">EUR</option>
        <option value="FJD">FJD</option>
        <option value="GBP">GBP</option>
        <option value="GTQ">GTQ</option>
        <option value="HKD">HKD</option>
        <option value="HRK">HRK</option>
        <option value="HUF">HUF</option>
        <option value="IDR">IDR</option>
        <option value="ILS">ILS</option>
        <option value="INR">INR</option>
        <option value="ISK">ISK</option>
        <option value="JPY">JPY</option>
        <option value="KRW">KRW</option>
        <option value="KZT">KZT</option>
        <option value="MXN">MXN</option>
        <option value="MYR">MYR</option>
        <option value="NOK">NOK</option>
        <option value="NZD">NZD</option>
        <option value="PAB">PAB</option>
        <option value="PEN">PEN</option>
        <option value="PHP">PHP</option>
        <option value="PKR">PKR</option>
        <option value="PLN">PLN</option>
        <option value="PYG">PYG</option>
        <option value="RON">RON</option>
        <option value="RUB">RUB</option>
        <option value="SAR">SAR</option>
        <option value="SEK">SEK</option>
        <option value="SGD">SGD</option>
        <option value="THB">THB</option>
        <option value="TRY">TRY</option>
        <option value="TWD">TWD</option>
        <option value="UAH">UAH</option>
        <!-- 這邊做這個是預設值 -->
        <option value="USD" selected>USD</option>
        <option value="UYU">UYU</option>
        <option value="VND">VND</option>
        <option value="ZAR">ZAR</option>
      </select>
      <input type="number" id="amount-one" placeholder="0" value="1" />
    </div>

    <div class="swap-rate-container">
      <button class="btn" id="swap">
        Swap
      </button>
      <div class="rate" id="rate"></div>
    </div>

    <div class="currency">
      <select id="currency-two">
        <option value="AED">AED</option>
        <option value="ARS">ARS</option>
        <option value="AUD">AUD</option>
        <option value="BGN">BGN</option>
        <option value="BRL">BRL</option>
        <option value="BSD">BSD</option>
        <option value="CAD">CAD</option>
        <option value="CHF">CHF</option>
        <option value="CLP">CLP</option>
        <option value="CNY">CNY</option>
        <option value="COP">COP</option>
        <option value="CZK">CZK</option>
        <option value="DKK">DKK</option>
        <option value="DOP">DOP</option>
        <option value="EGP">EGP</option>
        <option value="EUR" selected>EUR</option>
        <option value="FJD">FJD</option>
        <option value="GBP">GBP</option>
        <option value="GTQ">GTQ</option>
        <option value="HKD">HKD</option>
        <option value="HRK">HRK</option>
        <option value="HUF">HUF</option>
        <option value="IDR">IDR</option>
        <option value="ILS">ILS</option>
        <option value="INR">INR</option>
        <option value="ISK">ISK</option>
        <option value="JPY">JPY</option>
        <option value="KRW">KRW</option>
        <option value="KZT">KZT</option>
        <option value="MXN">MXN</option>
        <option value="MYR">MYR</option>
        <option value="NOK">NOK</option>
        <option value="NZD">NZD</option>
        <option value="PAB">PAB</option>
        <option value="PEN">PEN</option>
        <option value="PHP">PHP</option>
        <option value="PKR">PKR</option>
        <option value="PLN">PLN</option>
        <option value="PYG">PYG</option>
        <option value="RON">RON</option>
        <option value="RUB">RUB</option>
        <option value="SAR">SAR</option>
        <option value="SEK">SEK</option>
        <option value="SGD">SGD</option>
        <option value="THB">THB</option>
        <option value="TRY">TRY</option>
        <option value="TWD">TWD</option>
        <option value="UAH">UAH</option>
        <option value="USD">USD</option>
        <option value="UYU">UYU</option>
        <option value="VND">VND</option>
        <option value="ZAR">ZAR</option>
      </select>
      <input type="number" id="amount-two" placeholder="0" />
    </div>
  </div>

  <script src="script.js"></script>
</body>
```

# CSS:

### CSS 設置好的樣式

![](https://i.imgur.com/jTjqOnx.png)

### 程式碼

```css=
 :root {
   --primary-color: #5fbaa7;
 }

 * {
   box-sizing: border-box;
 }

 body {
   background-color: #f4f4f4;
   font-family: Arial, Helvetica, sans-serif;
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
   height: 100vh;
   margin: 0;
   /* 這邊加入一點padding讓螢幕比較小的用戶不會直接切到瀏覽器邊緣 */
   padding: 20px;
 }

 h1 {
   color: var(--primary-color);
 }

 p {
   text-align: center;
 }

 .btn {
   color: #fff;
   background: var(--primary-color);
   cursor: pointer;
   border-radius: 5px;
   font-size: 12px;
   padding: 5px 12px;
 }

 .money-img {
   width: 150px;
 }

 .currency {
   padding: 40px 0;
   display: flex;
   align-items: center;
   justify-content: space-between;
 }

 .currency select {
   padding: 10px 20px 10px 10px;
   -moz-appearance: none;
   -webkit-appearance: none;
   appearance: none;
   border: 1px solid #dedede;
   font-size: 16px;
   background: transparent;

/* 這邊是黑色箭頭的圖檔輸入 */
   background-image: url('data:image/svg+xml;charset=US-ASCII,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22292.4%22%20height%3D%22292.4%22%3E%3Cpath%20fill%3D%22%20000002%22%20d%3D%22M287%2069.4a17.6%2017.6%200%200%200-13-5.4H18.4c-5%200-9.3%201.8-12.9%205.4A17.6%2017.6%200%200%200%200%2082.2c0%205%201.8%209.3%205.4%2012.9l128%20127.9c3.6%203.6%207.8%205.4%2012.8%205.4s9.2-1.8%2012.8-5.4L287%2095c3.5-3.5%205.4-7.8%205.4-12.8%200-5-1.9-9.2-5.5-12.8z%22%2F%3E%3C%2Fsvg%3E');
   background-position: right 10px top 50%, 0, 0;
   background-size: 12px auto, 100%;
   background-repeat: no-repeat;
 }

 .currency input {

   /* 這邊讓邊框跟背景色消失 */
   border: 0;
   background: transparent;
   font-size: 30px;
   text-align: right;
 }

 .swap-rate-container {
   display: flex;
   align-items: center;
   justify-content: space-between;
 }

 .rate {
   color: var(--primary-color);
   font-size: 14px;
   padding: 0 10px;
 }


 /* 把所有進入focus狀態的物件邊框都消除 */
 select:focus,
 input:focus,
 button:focus {
   outline: 0;
 }

 @media (max-width: 600px) {
   .currency input {
     width: 200px;
   }
 }
```

小補充:

無

# JS:

```javascript=
// 轉換匯率1(左上角)
const currencyEl_one = document.getElementById('currency-one');

// 匯率1的總計
const amount_one = document.getElementById('amount-one');

// 轉換匯率2(左下角)
const currencyEl_two = document.getElementById('currency-two');

// 匯率2的總計
const amount_two = document.getElementById('amount-two');

//抓取顯示匯率的綠色文字的div
const rateEl = document.getElementById('rate');

// 抓取交換匯率的按鈕
const swap = document.getElementById('swap');

// Fetch exchange rates and update the DOM
// 取得匯率更新使用(fetch) 以及 把取得的資料更新DOM
function calculate() {

  // 抓取下拉式選單選到得value
  const currency_one = currencyEl_one.value;
  const currency_two = currencyEl_two.value;

  // 使用這個網址只有更改最後面得國家名稱即可即使取得更新資料
  fetch(`https://api.exchangerate-api.com/v4/latest/${currency_one}`)

    //取得JSON格式的資料回來
    .then(res => res.json())
    .then(data => {
      // console.log(data);

      //這邊資料抓取裡面的rates部分裡面的currency_two的value也就是你下拉式選單選到的值
      const rate = data.rates[currency_two];

      //把剛剛抓到的值放進去顯示匯率的div裡面並用ES6的字串串接方式擺入變數
      //讓呈現的資料變成動態的
      rateEl.innerText = `1 ${currency_one} = ${rate} ${currency_two}`;

      // 找到的匯率乘上amount_one的value就是amount_two
      amount_two.value = (amount_one.value * rate).toFixed(2);
    })
}

//Event listeners
//下拉式選單處使用change
//<tag>input處使用input

// 這邊的currencyEl_one改變 1.匯率div顯示會改變 2.匯率2的總計會改變
currencyEl_one.addEventListener('change', calculate);

//匯率1的總計的改變要靠使用者輸入或者是使用箭頭去改變會影響匯率2的總計
amount_one.addEventListener('input', calculate);

//匯率的div會改變 匯率2的總計也會改變
currencyEl_two.addEventListener('change', calculate);

//隨著的值改變都會改變
amount_two.addEventListener('input', calculate);

// 這邊處理點擊則交換匯率1,2的值也就是下拉式選單的值對調並呼叫calculate()再修改全部的值
swap.addEventListener('click', () => {
  const temp = currencyEl_one.value;
  currencyEl_one.value = currencyEl_two.value;
  currencyEl_two.value = temp;
  calculate();
})
```

小補充:

無

# jQuery:

以 currencyOne 為主軸去計算所有的空位

主要使用 jQuery 的部分主要是處理

- 抓取 id
- 抓取下拉式選單的 value
- 呈現 value 到 DOM
- 更改內文使用 text()

監聽事件的部分主要是處理使用

- change 當內容物改變時觸發事件

```javascript=
let currencyOne = $("#currency-one");
let amountOne = $("#amount-one");
let currencyTwo = $("#currency-two");
let amountTwo = $("#amount-two");

const swapBtn = $("#swap");
const showRate = $("#rate");

function calculate() {
  fetch(`https://api.exchangerate-api.com/v4/latest/${currencyOne.val()}`)
    .then((res) => res.json())
    .then((data) => {

      // 從API中取的rates的資料中currencyTwo的value所代表的匯率
      const rate = data.rates[currencyTwo.val()];

      // 呈現amountTwo的DOM
      amountTwo.val((rate * amountOne.val()).toFixed(2));

      // 呈現匯率到DOM
      showRate.text(`1${currencyOne.val()} = ${rate} ${currencyTwo.val()}`);
    });
}

//事件監聽部分當change的時候呼叫calculate函式
currencyOne.change(() => calculate());
amountOne.change(() => calculate());
currencyTwo.change(() => calculate());
amountTwo.change(() => calculate());

swapBtn.click(() => {
  // 必須要使用temp當作currencyOne因為他已經先被指派別的value了
  let temp = currencyOne.val();

  currencyOne.val(currencyTwo.val());
  currencyTwo.val(temp);

  calculate();
});

// 讓頁面一進來就呈現amount部分
calculate();

```
