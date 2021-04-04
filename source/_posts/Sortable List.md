---
title: 實作練習-Sortable List
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Sortable List | Drag & Drop API- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個可拖曳的列表(可分辨對錯)

## 成品:

![](https://i.imgur.com/1LpLUJA.png)

[成品網址](https://chiehliu.github.io/git-projects/SortableList/index.html)

## 成品功能:

1.所有表格中的人名可以拖曳 2.下方有個確認順序是否正確的按鈕 3.會顯示綠色以及紅色表示順序的對錯 4.拖曳途中經過的人名會顯示灰色代表將可以跟拖曳的人名做替換

# HTML

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Top 10 Richest People</title>
    <link rel="stylesheet" href="style.css" />
    <script
      src="https://kit.fontawesome.com/3da1a747b2.js"
      crossorigin="anonymous"
    ></script>
  </head>
  <body>
    <h1>10 Richest People</h1>
    <p>Drag and drop the items into their corresponding spots</p>

    <!-- 在JS裡面呈現 -->
    <ul class="draggable-list" id="draggable-list"></ul>
    <button class="check-btn" id="check">
      Check Order
      <i class="fas fa-paper-plane"></i>
    </button>

    <script src="script.js"></script>
  </body>
</html>
```

# CSS:

## CSS 設置好的樣式

![](https://i.imgur.com/1LpLUJA.png)

## CSS 完整程式碼

```css=
 @import url('https://fonts.googleapis.com/css?family=Lato&display=swap');

:root {
  --border-color: #e3e5e4;
  --background-color: #c3c7ca;
  --text-color: #34444f;
}

* {
  box-sizing: border-box;
}

body {
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: center;

  /* 對其最頂端 */
  justify-content: flex-start;
  height: 100vh;
  margin: 0;
  font-family: 'Lato', sans-serif;
}

.draggable-list {
  border: 1px solid var(--border-color);
  color: var(--text-color);
  padding: 0;
  list-style-type: none;
}

.draggable-list li {
  background-color: #fff;
  display: flex;
  flex: 1;
}

/* 使用偽類not()排除()內部以外的其他元素做修飾 */
.draggable-list li:not(:last-of-type) {
  border-bottom: 1px solid var(--border-color);
}

.draggable-list .number {
  background-color: var(--background-color);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  height: 60px;
  width: 60px;
}

.draggable-list li.over .draggable {
  background-color: #eaeaea;
}

.draggable-list .person-name {
  margin: 0 20px 0 0;
}

.draggable-list li.right .person-name {
  color: #3ae374;
}

.draggable-list li.wrong .person-name {
  color: #ff3838;
}

.draggable {
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  flex: 1;
}

.check-btn {
  background-color: var(--background-color);
  border: none;
  color: var(--text-color);
  font-size: 16px;
  padding: 10px 20px;
  cursor: pointer;
}

/* 點擊時放大 */
.check-btn:active {
  transform: scale(0.98);
}

/* 去除邊框 */
.check-btn:focus {
  outline: none;
}

```

小補充:

[:not()](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:not)

# JS:

## 變數設置

- draggable_list -整個 ul 的區域都是
  ![](https://i.imgur.com/zex1AQ8.png)

- check -按鈕的部分
  ![](https://i.imgur.com/SgozMvX.png)

- richestPeople - 有錢人的順序
- listItems - 空的陣列把創造好的 li 推進去
- dragStartIndex -為了讓 dragStart 抓到 index 使用的

```javascript=
const draggable_list=document.getElementById('draggable-list');
const check = document.getElementById('check');

const richestPeople =[
    'Jeff Bezos',
  'Bill Gates',
  'Warren Buffett',
  'Bernard Arnault',
  'Carlos Slim Helu',
  'Amancio Ortega',
  'Larry Ellison',
  'Mark Zuckerberg',
  'Michael Bloomberg',
  'Larry Page'
];

//Store list items
const listItems =[];

// console.log(listItems);
let dragStartIndex;
```

## functions:

### createList

- 使用[...]展開運算子才能把名字一條一條列出不然會直接印出一整個陣列
  ![](https://i.imgur.com/iPk8n55.png)

使用[...]展開運算子後才能這樣印出
![](https://i.imgur.com/y2DfY4E.png)

- a.sort 後面的 sort 部分是上面 object 的屬性不是方法要注意

- 這邊的事件監聽處理的內容都在這個創造的 li 上面所以使用 function 在這裏面直接呼叫
  `addEventListeners();`

```javascript=
function createList(){

    // 如果不使用展開運算子就會只印出一個陣列包含所有名字而無法迭代
    [...richestPeople]

    //這部分使順序變成隨機因為後方有賦予它一個屬性是隨機的
    .map((a) =>({value:a, sort:Math.random()}))

    // 這邊使用sort來做排序sort大的網前擺
    // 這邊a.sort後面的sort部分是上面object的屬性不是方法要注意
    .sort((a,b) =>(a.sort-b.sort))
    .map((a) =>a.value)
    .forEach((person, index)=>{
        // console.log(person);

        const listItem = document.createElement('li');

        listItem.setAttribute('data-index',index);

        // 為了讓排名的數字不是從零開始所以給它加一
        listItem.innerHTML = `
        <span class="number">${index+1}</span>
        <div class="draggable" draggable ="true">
        <p class="person-name">${person}</p>
        <i class="fas fa-grip-lines"></i></div>`;


        listItems.push(listItem);

        // 把剛剛做好的li內容貼到DOM上
        draggable_list.appendChild(listItem);
    })

    // 這邊的事件處理的內容都在這個創造的li上面所以這樣處理
    addEventListeners();
}
```

### 事件監聽 function

- dragStart -
  這個 func 的目的在於交換跟 drop 區域的內容
  `dragStartIndex`這個變數設置在全域是因為整個轉換的過程會在 drop 那邊進行，這邊只是先抓取 index 而已
- dragEnter - 當拖曳的目標進入 li 時觸發 class=over 也就是變灰框框
- dragLeave -當拖曳的目標進入 li 時觸發 class=over 也就是變灰框框
- dragOver - 這邊做避免預設的狀況才有辦法使用 swapItems 這個函式不然會被一直提交
- dragDrop - 這邊的函式作用在於取的 start,end 的 index 並丟進去 swapItems 去作用

```javascript=

// 這個func的目的在於交換跟drop區域的內容
//dragStartIndex這個變數設置在全域是因為整個轉換的過程會在drop那邊進行，這邊只是先抓取index而已
function dragStart(){

    // 這邊的this抓取的是div而我們要的是它外層的li
    // 所以使用closest("li")去抓取
    dragStartIndex = +this.closest("li").getAttribute("data-index");
}

// 當拖曳的目標進入li時觸發class=over也就是變灰框框
function dragEnter(){
    this.classList.add("over")
}
// 當拖曳目標離開li時觸發，會拉掉class=over
function dragLeave(){
    this.classList.remove("over")

}

function dragOver(e){
    // 這邊做避免預設的狀況才有辦法使用swapItems這個函式不然會被一直提交
    e.preventDefault();
}

// 這邊的函式作用在於取的start,end的index並丟進去swapItems去作用
function dragDrop(){
    const dragEndIndex = +this.getAttribute('data-index');
    swapItems(dragStartIndex, dragEndIndex);

    this.classList.remove("over");
}
```

### swapItems

運用剛剛取的的 start,end index 來尋找其中的 div 並且指派給變數 itemOne,itemTwo

並且做交換使用 appendChild 交換兩方的內容

```javascript=
function swapItems(fromIndex, toIndex){

    // 這邊會抓取到名字內容的div
    const itemOne = listItems[fromIndex].querySelector('.draggable');
    const itemTwo = listItems[toIndex].querySelector('.draggable');

    // 兩個互相appnedChild交換內容
    listItems[fromIndex].appendChild(itemTwo);
    listItems[toIndex].appendChild(itemOne);
}
```

### checkOrder

設立變數 personName 並且指派 draggable 的 innerText 然後跟 richestPeople 作對比

確認是否是正確的順序
對的話加上 class="right"
錯的話加上 class="wrong"

```javascript=
//確認是否是正確的順序(跟richestPeople作對比)
function checkOrder(){
    listItems.forEach((listItem, index) =>{
        const personName = listItem.querySelector('.draggable').innerText.trim();

        if(personName !== richestPeople[index]){
            listItem.classList.add('wrong');
        }else{
            listItem.classList.remove('wrong');
            listItem.classList.add('right');
        }
    })
}
```

## 事件監聽

主要使用 drag&drop 系列的事件:

- dragstart - 點擊下去物件
- dragover -把拖曳的物件滑過其他物件時觸發
- drop -放下物件時觸發
- dragenter - 當拖曳物件進去其他物件時觸發
- dragleave- 當拖曳物件離開其他物件時觸發

確認順序的按鈕

- check -當按下按鈕會確認順序是否正確，正確顯示綠色錯誤顯示紅色

```javascript=
function addEventListeners() {
    const draggables = document.querySelectorAll('.draggable');
    const dragListItems = document.querySelectorAll('.draggable-list li');

    draggables.forEach(draggable => {
      draggable.addEventListener('dragstart', dragStart);
    });

    dragListItems.forEach(item => {
      item.addEventListener('dragover', dragOver);
      item.addEventListener('drop', dragDrop);
      item.addEventListener('dragenter', dragEnter);
      item.addEventListener('dragleave', dragLeave);
    });

}

check.addEventListener('click', checkOrder);
```

小補充:
[Drag and Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)

[closest()](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/closest)

[Higher Order Functions & Arrays 筆記](https://hackmd.io/UwrfbMhASlaWWPOXNiO_1Q)

## JS 完整程式碼:

```javascript=
const draggable_list=document.getElementById('draggable-list');
const check = document.getElementById('check');

const richestPeople =[
    'Jeff Bezos',
  'Bill Gates',
  'Warren Buffett',
  'Bernard Arnault',
  'Carlos Slim Helu',
  'Amancio Ortega',
  'Larry Ellison',
  'Mark Zuckerberg',
  'Michael Bloomberg',
  'Larry Page'
];

//Store list items
const listItems =[];

// console.log(listItems);
let dragStartIndex;

createList();


//Insert list items into DOM
function createList(){

    // 如果不使用展開運算子就會只印出一個陣列包含所有名字而無法迭代
    [...richestPeople]
    .map((a) =>({value:a, sort:Math.random()}))

    // 這邊a.sort後面的sort部分是上面object的屬性不是方法要注意
    .sort((a,b) =>(a.sort-b.sort))
    .map((a) =>a.value)
    .forEach((person, index)=>{
        // console.log(person);

        const listItem = document.createElement('li');

        listItem.setAttribute('data-index',index);

        // 為了讓排名的數字不是從零開始所以給它加一
        listItem.innerHTML = `
        <span class="number">${index+1}</span>
        <div class="draggable" draggable ="true">
        <p class="person-name">${person}</p>
        <i class="fas fa-grip-lines"></i></div>`;


        listItems.push(listItem);

        // 把剛剛做好的li內容貼到DOM上
        draggable_list.appendChild(listItem);
    })

    // 一次要附上多個事件監聽時可以這樣使用
    addEventListeners();
}

// 這個func的目的在於交換跟drop區域的內容
//dragStartIndex這個變數設置在全域是因為整個轉換的過程會在drop那邊進行，這邊只是先抓取index而已
function dragStart(){

    // 這邊的this抓取的是div而我們要的是它外層的li
    // 所以使用closest("li")去抓取
    dragStartIndex = +this.closest("li").getAttribute("data-index");
}

// 當拖曳的目標進入li時觸發class=over也就是變灰框框
function dragEnter(){
    this.classList.add("over")
}
// 當拖曳目標離開li時觸發，會拉掉class=over
function dragLeave(){
    this.classList.remove("over")

}

function dragOver(e){
    // 這邊做避免預設的狀況才有辦法使用swapItems這個函式不然會被一直提交
    e.preventDefault();
}
function dragDrop(){
    const dragEndIndex = +this.getAttribute('data-index');
    swapItems(dragStartIndex, dragEndIndex);

    this.classList.remove("over");
}


function swapItems(fromIndex, toIndex){

    // 這邊會抓取到名字內容的div
    const itemOne = listItems[fromIndex].querySelector('.draggable');
    const itemTwo = listItems[toIndex].querySelector('.draggable');

    // 兩個互相appnedChild交換內容
    listItems[fromIndex].appendChild(itemTwo);
    listItems[toIndex].appendChild(itemOne);
}

//確認是否是正確的順序(跟richestPeople作對比)
function checkOrder(){
    listItems.forEach((listItem, index) =>{
        const personName = listItem.querySelector('.draggable').innerText.trim();

        if(personName !== richestPeople[index]){
            listItem.classList.add('wrong');
        }else{
            listItem.classList.remove('wrong');
            listItem.classList.add('right');
        }
    })
}


function addEventListeners() {
    const draggables = document.querySelectorAll('.draggable');
    const dragListItems = document.querySelectorAll('.draggable-list li');

    draggables.forEach(draggable => {
      draggable.addEventListener('dragstart', dragStart);
    });

    dragListItems.forEach(item => {
      item.addEventListener('dragover', dragOver);
      item.addEventListener('drop', dragDrop);
      item.addEventListener('dragenter', dragEnter);
      item.addEventListener('dragleave', dragLeave);
    });

}

check.addEventListener('click', checkOrder);
```
