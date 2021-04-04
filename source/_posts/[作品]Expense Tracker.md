---
title: 實作練習-Expense Tracker
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Expense Tracker- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個記帳簿

## 成品:

![](https://i.imgur.com/vVXIAQM.png)

[成品網址](https://vanillawebprojects.com/projects/expense-tracker/)

## 成品功能:

1.在最上方 yout balance 處顯示所剩餘額 2.在 income、expense 處顯示所以收入以及花費金額並呈現綠色以及紅色
3.History 的地方會記錄並顯示出花費狀態以及輸入的內容 ex 書本支出 100 元並且會有刪除品項的按鈕
ps.支出會顯示紅色 收入會顯示綠色
![](https://i.imgur.com/t8bWefX.png) 4.下方有新增各種行為的欄位並且有加入的 submit 按鈕

## HTML

### 上 CSS 之前的 HTML:

![](https://i.imgur.com/ukAEWT4.png)

### 程式碼:

```htmlembedded=
<body>
    <h2>Expense Tracker</h2>

    <div class="container">
      <h4>Your Balance</h4>
      <!--  這邊的h1金額的部分會跟JS連動 -->
      <h1 id="balance">$0.00</h1>

      <div class="inc-exp-container">
        <div>
          <h4>Income</h4>
          <!-- 這邊設置的id money-plus會給JS抓取 -->
          <!-- 後方的plus會修改文字顏色 -->
          <p id="money-plus" class="money plus">$0.00</p>
        </div>
        <div>
          <h4>Expense</h4>
          <!-- 這邊設置的id money-minus會給JS抓取 -->
          <!-- 後方的minus會修改文字顏色 -->
          <p id="money-minus" class="money minus">-$0.00</p>
        </div>
      </div>

      <h3>History</h3>

      <!-- 這個部分是JS操作的不會顯示出來但是因為要在CSS設定所以先打出來調整樣式 -->
      <ul id="list" class="list">
        <!-- <li class="minus">
          Cash<span>-$400</span><button class="delete-btn">x</button>
        </li> -->
      </ul>

      <h3>Add new transaction</h3>

      <!-- 設置id form抓取這邊input全區 -->
      <form id="form">

        <!-- 這區域有需要跟JS互動所以有設置id text amount分別是兩個input區域-->
        <div class="form-control">
          <label for="text">Text</label>
          <input type="text" id="text" placeholder="Enter text..." />
        </div>
        <div class="form-control">
          <label for="amount">
            Amount <br />(negative - expense, positive - income)
          </label>
          <input type="number" id="amount" placeholder="Enter amount..." />
        </div>
        <button class="btn">Add transaction</button>
      </form>
    </div>

    <script src="script.js"></script>
  </body>
```

## CSS:

### CSS 設置好的樣式

![](https://i.imgur.com/vVXIAQM.png)

### 程式碼

```css=
 @import url('https://fonts.googleapis.com/css?family=Lato&display=swap')

/* 讓特定的物件在瀏覽器上變的比較明顯 */
:root {
    --box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);
}

* {
    box-sizing: border-box;
}

/* body這邊用的是老樣子一樣全置中並且設定滿版margin0 */
body {
    background-color: #f7f7f7;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    font-family: 'Lato', sans-serif;
}

.container {
    margin: 30px auto;
    width: 350px;

}

h1 {
    letter-spacing: 1px;
    margin: 0;
}

h3 {
    border-bottom: 1px solid #bbb;
    padding-bottom: 10px;
    margin: 40px 0 10px;
}

h4 {
    margin: 0;
    text-transform: uppercase;
}

.inc-exp-container {
    background-color: #fff;
    box-shadow: var(--box--shadow);
    padding: 20px;
    display: flex;

    /* 讓income跟expnse各占一邊 */
    justify-content: space-between;
    margin: 20px 0;
}

.inc-exp-container>div {
    flex: 1;
    text-align: center;
}

/* 中間分隔線區域只設定第一個div的右方底線 */
.inc-exp-container>div:first-of-type {
    border-right: 1px solid #dedede;
}

/* 單純是money的部分處理文字大小間隔以及margin */
.money {
    font-size: 20px;
    letter-spacing: 1px;
    margin: 5px;
}

/* 這部分以動態的JS會修改文字顏色 */

.money.plus {
    color: #2ecc71;
}

/* 這部分以動態的JS會修改文字顏色 */

.money.minus {
    color: #c0392b;
}

/* 這邊設置inline-block讓label可以吃到margin  */
label {
    display: inline-block;
    margin: 10px 0;
}

input[type='text'],
input[type='number'] {
    border: 1px solid #dedede;
    border-radius: 2px;
    display: block;
    font-size: 16px;
    padding: 10px;
    width: 100%;
}


.btn {
    cursor: pointer;
    background-color: #9c88ff;
    box-shadow: var(--box--shadow);
    color: #fff;
    border: 0;
    display: block;
    font-size: 16px;
    margin: 10px 0 30px;
    padding: 10px;
    width: 100%;
}

/* 去除外框 */
.btn:focus,
.delete-btn {
    outline: 0;
}


.list {
    /* 去除圓點點 */
    list-style-type: none;
    padding: 0;
    margin-bottom: 40px;
}

.list li {
    background-color: #fff;
    box-shadow: var(--box--shadow);
    color: #333;
    display: flex;
    justify-content: space-between;

    /* 這邊設置定位relative是為了delete btn的設置 */
    position: relative;
    padding: 10px;
    margin: 10px 0;
}

/* 這邊是加入物件的顏色用classname區別 */
.list li.plus {
    border-right: 5px solid #2ecc71;
}

.list li.minus {
    border-right: 5px solid #c0392b;
}


.delete-btn {
    cursor: pointer;
    background-color: #e74c3c;
    border: 0;
    color: #fff;
    font-size: 20px;
    line-height: 20px;
    padding: 2px 5px;
    position: absolute;
    top: 50%;
    left: 0%;
    /* 調整位置往左邊一個自己往上半個自己ㄉ */
    transform: translate(-100%, -50%);

    /* 這邊設置隱藏 */
    opacity: 0;
    /* 透明度的特效設置 */
    transition: opacity 0.3s ease;

}

/* 當滑鼠滑過History的物件後delete btn 才會顯示 */
.list li:hover .delete-btn {
    opacity: 1;
}
```

小補充:

無

## JS:

### 變數設置

要使用 JS 處理的地方基本上都要抓取:

- balance 區域
  處理數字呈現
  ![](https://i.imgur.com/Swd19mn.png)

- money-plus,money-minus 區域
  處理數字呈現
  ![](https://i.imgur.com/LnCbwGH.png)

- list 區域
  處理加入的新的物件
  ![](https://i.imgur.com/MLTc6PF.png)

- form 區域
  主要處理 submit 事件
  ![](https://i.imgur.com/q1v3tWp.png)

- text,amount 區域
  處理輸入的內容
  ![](https://i.imgur.com/eVuVJqe.png)

```javascript=
const balance = document.getElementById("balance");
const money_plus = document.getElementById("money-plus");
const money_minus = document.getElementById("money-minus");
const list = document.getElementById("list");
const form = document.getElementById("form");
const text = document.getElementById("text");
const amount = document.getElementById("amount");
```

### functions:

- addTransactionDOM-把收入或是消費的新的 li 呈現到 History 上面(也就是 DOM 上面)

他會在 addTransaction function 被呼叫，因為只有當新的交易產生這個功能才會被需要

- 注意的點:
  作者使用 onclick 在 delete-btn 上面並且使用 template string`${}`放入動態的變數進去符合 id，這個用法只能用在字串中一般的 function 無法使用

```javascript=
//add transactions to DOM  把收入或是消費的新的li呈現到History上面(也就是DOM)
function addTransactionDOM(transaction) {
  // get sign 取得正負號(+-)
  const sign = transaction.amount < 0 ? "-" : "+";

  //創造新的li要放進去收入或是花費
  const item = document.createElement("li");

  //add class base on value 把剛創造的li加上class但是做要判斷
  // 當transactions的值amount<0時放入minus,>0時放plus
  item.classList.add(transaction.amount < 0 ? "minus" : "plus");

  //放入的字串用template string串接放入變數transacitons.text當作物品名稱
  //sign 表示正負
  //Math.abs(transactions.amount) 這段用數學方法取絕對值因為前面有sing判斷正負了
  item.innerHTML = `
    ${transaction.text} <span>${sign}${Math.abs(
    transaction.amount

    // 使用onlick事件並且使用動態參數`${}`包裹住transaction的id這樣一來參數就會是動態的
    //內容會隨著刪除的id不同而產生不同的array
  )}</span> <button class="delete-btn" onclick="removeTransaction(${
    transaction.id
  })">x</button>
    `;

  //appenChild item到list上面
  list.appendChild(item);
}
```

- updateValues
  讓 balance, income and expense 的數值可以即時隨著新的交易更新

- 注意的點:
  map reduce filter 的用法

尤其是 reduce 的寫法比較特別

```javascript=
reduce((acc, item) => (acc += item), 0)
```

```javascript=
//update the balance, income and expense
function updateValues() {

  // 這邊會創造出一個新的array裡面只有包含amount的值
  const amounts = transactions.map((transaction) => transaction.amount);

  // 加總所有的amount使用reduce也就是收入以及花費的的總數
  //acc代表總數 item代表每筆交易的內容金額
  //後方的toFixed代表取到小數點第幾位
  const total = amounts.reduce((acc, item) => (acc += item), 0).toFixed(2);

  //處理income部分的數字呈現
  const income = amounts
    .filter((item) => item > 0)
    .reduce((acc, item) => (acc += item), 0)
    .toFixed(2);

  //處理expense部分的數字呈現
  const expense = (
    amounts.filter((item) => item < 0).reduce((acc, item) => (acc += item), 0) *
    -1
  ).toFixed(2);

  //把剛剛處理好的income,total,expense放到DOM裡面更新文字
  balance.innerText = `$${total}`;
  money_plus.innerText = `$${income}`;
  money_minus.innerText = `$${expense}`;
}
```

- addTransaction

submit 後觸發的方法:

1. 加入新的交易資料
1. 把加入的資料更新到 DOM(History)
1. 更新 balance, income, expense 數字
1. 加入資料進去 localstorage

2.3.4 必須呼叫其他函式來處理

最後把空格清空

```javascript=
//add transation submit後觸發的方法:加入新的交易資料
function addTransaction(e) {
  e.preventDefault();

  // 如果text,amount其中一個為空則跳出警告，有正確輸入的話創造一個新的transaction
  if (text.value.trim() === "" || amount.value.trim() === "") {
    alert("Please add a text and amount");
  } else {
    const transaction = {
      id: generateID(),
      text: text.value,

      //注意這邊的amount出來必須是數字所以加上個+號
      amount: +amount.value,
    };

    //把新加入的transaction推進去原本的trasactions裡面
    transactions.push(transaction);

    //把收入或是消費的新的li呈現到History上面(也就是DOM)
    addTransactionDOM(transaction);

    //使balance, income, expense 數字可以即時更新
    updateValues();

    //當加入新的交易進去transactions裡面就要呼叫這裡就會更新localstorage
    updateLocalStorage();

    //當輸入完成之後恢復空白
    text.value = "";
    amount.value = "";
  }
}
```

- generateID

主要使用數學的方法來產生 id 給上面的 transaction

```javascript=
// Generate random ID
function generateID() {
  return Math.floor(Math.random() * 100000000);
}
```

- updateLocalStorage

設置鍵值對並且轉換成 JSON 格式推上去 localstorage 儲存

```javascript=
//update localstorage transactions 更新localstorage裡面的transactions資料
function updateLocalStorage() {
  // 把transactions的資料用JSON字串化的格式丟上去localstorage
  localStorage.setItem("transactions", JSON.stringify(transactions));
}
```

- removeTransaction

使用 filter 去做篩選出"沒有參數 id 的 array"並且重新指派給 transactions(原本的資料庫)
就可以刪掉放入 removeTransaction 裡面的物件

```javascript=
//remove transaction by id

function removeTransaction(id) {
  // 使用filter去做篩選出"沒有參數的輸入id的array"並且重新指派給transactions(原本的資料庫)
  // 就可以刪掉放入removeTransaction裡面的物件
  transactions = transactions.filter((transaction) => transaction.id !== id);

  // 刪除資料的時候也要更新localstorage
  updateLocalStorage();

  init();
}
```

- init

會更新所有檯面上數值以及 History 裡面的表格使用:

1. updateValues 更新 balance, income and expense 的數值
1. addTransactionDOM 更新 History 裡面的表格

```javascript=
function init() {
  list.innerHTML = "";

  //把transactions裡面的資料每一筆都執行addTransactionDOM這個function
  transactions.forEach(addTransactionDOM);

  updateValues();
}
```

- 事件監聽 submit

```javascript=
form.addEventListener("submit", addTransaction);
```

小補充:

`Math.floor`
函式會回傳小於等於所給數字的最大整數。

`Math.random`
回傳一個偽隨機小數 (pseudo-random)，小數也稱浮點數； 介於 0 到 1 之間(包含 0，不包含 1) 。

`toFixed()`
選擇性輸入數值。顯示數值至多少個小數點，範圍由 0 到 20 之間，執行時或可支援非常大範圍的數值。如果無輸入會默認做 0。

### 完整程式碼:

```javascript=
const balance = document.getElementById("balance");
const money_plus = document.getElementById("money-plus");
const money_minus = document.getElementById("money-minus");
const list = document.getElementById("list");
const form = document.getElementById("form");
const text = document.getElementById("text");
const amount = document.getElementById("amount");

//這邊先設置這個dummy用作展示使用，之後會使用的是localstorage裡面存放的資料
// const dummyTransactions = [
//   {
//     id: 1,
//     text: "Flower",
//     amount: -20,
//   },
//   {
//     id: 2,
//     text: "Salary",
//     amount: 300,
//   },
//   {
//     id: 3,
//     text: "Book",
//     amount: -10,
//   },
//   {
//     id: 4,
//     text: "Camera",
//     amount: 150,
//   },
// ];

//從localstorage抓取資料使用getItem並且需要轉換格式使用JSON.parse轉回原本的物件不然原本是JSON格式不能使用
const localStorageTransactions = JSON.parse(
  localStorage.getItem("transactions")
);

//判斷getItem得到的資料內容是否為空不是的話localStorageTransactions(我們存上去的內容)，是空的話則放入空的[]console.log的話可以看到
let transactions =
  localStorage.getItem("transactions") !== null ? localStorageTransactions : [];

console.log(transactions);

//add transation submit後觸發的方法:加入新的交易資料
function addTransaction(e) {
  e.preventDefault();

  if (text.value.trim() === "" || amount.value.trim() === "") {
    alert("Please add a text and amount");
  } else {
    const transaction = {
      id: generateID(),
      text: text.value,

      //注意這邊的amount出來必須是數字所以加上個+號
      amount: +amount.value,
    };

    //把新加入的一筆交易推進去原本的trasactions裡面
    transactions.push(transaction);

    //把收入或是消費的新的li呈現到History上面(也就是DOM)
    addTransactionDOM(transaction);

    //使balance, income, expense 數字可以即時更新
    updateValues();

    //當加入新的交易進去transactions裡面就要呼叫這裡就會更新localstorage
    updateLocalStorage();

    //當輸入完成之後恢復空白
    text.value = "";
    amount.value = "";
  }
}

//generate ID 取得隨機的ID

function generateID() {
  return Math.floor(Math.random() * 100000000);
}

//add transactions to DOM  把收入或是消費的新的li呈現到History上面(也就是DOM)
function addTransactionDOM(transaction) {
  // get sign 取得正負號(+-)
  const sign = transaction.amount < 0 ? "-" : "+";

  //創造新的li要放進去收入或是花費
  const item = document.createElement("li");

  //add class base on value 把剛創造的li加上class但是做要判斷
  // 當transactions的值amount<0時放入minus,>0時放plus
  item.classList.add(transaction.amount < 0 ? "minus" : "plus");

  //放入的字串用template string串接放入變數transacitons.text當作物品名稱
  //sign 表示正負
  //Math.abs(transactions.amount) 這段用數學方法取絕對值因為前面有sing判斷正負了
  item.innerHTML = `
    ${transaction.text} <span>${sign}${Math.abs(
    transaction.amount
    // 使用onlick事件並且使用動態參數``包裹住transaction的id
  )}</span> <button class="delete-btn" onclick="removeTransaction(${
    transaction.id
  })">x</button>
    `;

  //appenChild item到list上面
  list.appendChild(item);
}

//update the balance, income and expense  讓balance, income and expense可以即時更新隨著新的交易產生
function updateValues() {
  // 這邊會創造出一個新的array裡面只有包含amount的值
  const amounts = transactions.map((transaction) => transaction.amount);

  // 加總所有的amount使用reduce也就是收入以及花費的的總數
  //acc代表總數 item代表每筆交易的內容金額
  //後方的toFixed代表取到小數點第幾位
  const total = amounts.reduce((acc, item) => (acc += item), 0).toFixed(2);

  //處理income部分的數字呈現
  const income = amounts
    .filter((item) => item > 0)
    .reduce((acc, item) => (acc += item), 0)
    .toFixed(2);

  //處理expense部分的數字呈現
  const expense = (
    amounts.filter((item) => item < 0).reduce((acc, item) => (acc += item), 0) *
    -1
  ).toFixed(2);

  //把剛剛處理好的income,total,expense放到DOM裡面更新文字
  balance.innerText = `$${total}`;
  money_plus.innerText = `$${income}`;
  money_minus.innerText = `$${expense}`;
}

//remove transaction by id

function removeTransaction(id) {
  // 使用filter去做篩選出"沒有參數的輸入id的array"並且重新指派給transactions(原本的資料庫)
  // 就可以刪掉放入removeTransaction裡面的物件藉著他的id
  transactions = transactions.filter((transaction) => transaction.id !== id);

  // 刪除資料的時候也要更新localstorage
  updateLocalStorage();

  init();
}

//update localstorage transactions 更新localstorage裡面的transactions資料
function updateLocalStorage() {
  // 把transactions的資料用JSON字串化的格式丟上去localstorage
  localStorage.setItem("transactions", JSON.stringify(transactions));
}

//Init app 啟動app

function init() {
  list.innerHTML = "";

  //把transactions裡面的資料每一筆都執行addTransactionDOM這個function
  transactions.forEach(addTransactionDOM);

  updateValues();
}

init();


//事件監聽
form.addEventListener("submit", addTransaction);
```
