---
title: JS-DOM Crash Course(一萬字)
date:
tags: Javascript
category: Javascript
---

# JavaScript DOM Crash Course 

---
tags: Javascript relate
---

###### tags: `Javascript`


# JavaScript DOM Crash Course Part - 1

## DOM簡介

* Document Object Model
* 由瀏覽器建構的樹的節點(nodes)意味著每個節點都有各自的property跟方法可以運用
* JS可以被用來讀寫以及操作DOM
* 物件導向的呈現方式

![](https://i.imgur.com/Ph2hcZr.png)

## 作者使用下方這個Item Lister來做為範例教學DOM的操作

![](https://i.imgur.com/jOdC6jX.png)

這邊的HTML可直接貼上編輯器就可以直接使用

```htmlembedded=
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css"
    integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">
  <title>Item Lister</title>
</head>

<body>
  <header id="main-header" class="bg-success text-white p-4 mb-3">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <h1 id="header-title">Item Lister</h1>
        </div>
        <div class="col-md-6 align-self-center">
          <input type="text" class="form-control" id="filter" placeholder="Search Items...">
        </div>
      </div>
    </div>
  </header>
  <div class="container">
    <div id="main" class="card card-body">
      <h2 class="title">Add Items</h2>
      <form id="addForm" class="form-inline mb-3">
        <input type="text" class="form-control mr-2" id="item">
        <input type="submit" class="btn btn-dark" value="Submit">
      </form>
      <h2 class="title">Items</h2>
      <ul id="items" class="list-group">
        <li class="list-group-item">Item 1 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
        <li class="list-group-item">Item 2 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
        <li class="list-group-item">Item 3 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
        <li class="list-group-item">Item 4 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
      </ul>
    </div>
  </div>

  <script src="dom.js"></script>
</body>

</html>
```
## 檢視 document 的物件

`console.dir(document);`

這邊會在開發者工具印出非常多的properties以及methods不過作者會挑幾個比較重要的說明

```javascript=
//要使用document 的方法(.)

console.log(document.方法)

```
## document常用方法介紹:

```javascript=
console.log(document.domain);//127.0.0.1 - 可以查看網域(domain)
console.log(document.URL);//http://127.0.0.1:5500/index.html - 查看網址
console.log(document.title);//Item Lister - 查看title
console.log(document.doctype);//<!DOCTYPE html> - 查看檔案類型
console.log(document.body);// 可以在console查看body的元素
console.log(document.head);// 可以在console查看head的元素
console.log(document.forms);// 可以在console查看所有form的元素以及他的方法
console.log(document.links);//可以在console查看link的元素
console.log(document.images);//可以在console查看images的元素
```
也可以直接修改title

```javascript=

document.title = '123';
```

![](https://i.imgur.com/JmgXdYH.png)


下方這個方法會給我們一個HTMLCollection包含了所有的HTML元素以及很多可以使用的方法(methods)

```javascript=
console.log(document.all);
```

![](https://i.imgur.com/WEQB3tG.png)

如果我們想要擷取其中的內容:

可以這樣使用使用他的檢索號碼就可以抓取內容

```javascript=
console.log(document.all[1]);
```

![](https://i.imgur.com/ya1zcgB.png)


## selectors(選取器)介紹 用來抓取元素

### getElementById

輸入要選取的 id 就可以抓取選取的元素

```javascript=
console.log(document.getElementById('header-title'));
```

![](https://i.imgur.com/wljNYqG.png)

也可以把抓取的內容指派給變數使用，這樣在呼叫的時候就只要呼叫變數就好不用整串都打

```javascript=
var headerTitle = document.getElementById('header-title');

console.log(headerTitle);
```

### textContent & innerText

這兩個方法可以針對選取的元素修改其文字內容

它們的不同之處在於:

textContent不會看到CSS修改的部分
innerText會看到CSS修改的部分

```javascript=
// 把內文從item Lister改成 Hello 跟 Goodbye
headerTitle.textContent = 'Hello';
headerTitle.innerText = 'Goobye';
```

![](https://i.imgur.com/c7LjSGb.png)

### innerHTML 

用來加入新的HTML tag來加入舊的tag並不是直接取代

```javascript=
headerTitle.innerHTML = '<h3>HEllo</h3>';
```
原本的tag還保留
![](https://i.imgur.com/OxSt9Ah.png)

使用過後修改成`'<h3>HEllo</h3>'`
![](https://i.imgur.com/TXmXDYA.png)



### style 

修飾被抓取元素的CSS

選擇要使用的CSS屬性的部分不能照原本CSS格式的寫法要改成JS的寫法(camel型態的字首英文大小)

```javascript=
header.style.borderBottom = 'solid 3px #000';
```
多加了底線上去
![](https://i.imgur.com/TkBcCTz.png)


### getElementByClassName

一樣會用HTMLCollection包裝好內容印出給我們

```javascript=
var items = document.getElementsByClassName('list-group-item');

console.log(items);
```
印出結果:
![](https://i.imgur.com/Ah4tqy2.png)

這邊我們可以使用`console.log(items[1])`擷取內容

```javascript=

console.log(items[1]);
```
![](https://i.imgur.com/xnpMmf1.png)

並且修改選取的元素文字內容

```javascript=
items[1].textContent = 'hello2';
```
![](https://i.imgur.com/XdOdEVS.png)

也可以更改他的CSS

```javascript=

items[1].style.fontWeight = 'bold';// 字體變粗體
items[1].style.backgroundColor = 'yellow';//加上背景色黃色
```
![](https://i.imgur.com/11GKWCT.png)


CSS修飾全部選取的內容

使用下面這串是會報錯的

因為它是一個HTMLCollection沒有辦法直接使用方法，所以必須使用迴圈一個一個印出去使用方法

```javascript=
//錯誤寫法會報錯
items.style.backgroundColor = '#f4f4f4';
```
![](https://i.imgur.com/uBADpUJ.png)

正確解法:

```javascript=
for (i = 0; i < items.length; i++) {
    items[i].style.backgroundColor = 'red';
}
```
這樣就可以全部都上色瞜!
![](https://i.imgur.com/Sn8L3DK.png)


### getElementByTagName

這邊會的到跟上面getElementByClassName一樣的結果，因為選取的是一樣的元素

```javascript=
var li = document.getElementsByTagName('li');

console.log(li);
console.log(li[1]);
li[1].textContent = 'hello2';
li[1].style.fontWeight = 'bold';

li[1].style.backgroundColor = 'yellow';


for (i = 0; i < li.length; i++) {
    li[i].style.backgroundColor = 'red';
}
```

這邊的例子可以看到CSS的修飾的部分一樣會吃到item 5因為DOM Seletor這邊抓取的是tag`<li>`
如果這邊處理的在getElementByClassName的話就不會出現紅色的背景因為item 5 沒有class
![](https://i.imgur.com/aWdYiiV.png)

![](https://i.imgur.com/Cy5EfQV.png)


### querySelector

可以選取任何在HTML上面的元素以及class,id都可以，並做修改跟操作

```javascript=
var header = document.querySelector('#main-header');
header.style.borderBottom = 'solid 4px red'//增加底線

var input = document.querySelector('input');
input.value = 'Hello World';//改變input的value

var submit = document.querySelector('input[type ="submit"]');
submit.value = "Send";// 選取type的作法要加上[] 修改按鈕的value改成Send
```

![](https://i.imgur.com/10uRKIf.png)

![](https://i.imgur.com/cMcCPLm.png)


### querySelector - CSS偽類的使用

* 如果沒有作處理就影響第一個
* last-child
* nth-child(i)

```javascript=
var item = document.querySelector('.list-group-item');
item.style.color = 'red'//如果選取對象是複數並且沒有告訴它影響哪一個的話會影響第一個

var lastItem = document.querySelector('.list-group-item:last-child');//偽類（ Pseudo-classes ）

lastItem.style.color = 'green';

var secondItem = document.querySelector('.list-group-item:nth-child(2)');

secondItem.style.color = 'coral';
```

![](https://i.imgur.com/2rVT0TF.png)

### querySelectorAll

可以抓取所有選取的內容HTML tags, id, class並且產一個Nodelist它是可以使用array function的!!

```javascript=
var titles = document.querySelectorAll('.title');
console.log(titles);
```

![](https://i.imgur.com/GQselnn.png)


```javascript=

titles[0].textContent = 'Hello';// 當然它也可以這樣選取索引號碼後做修改
```

![](https://i.imgur.com/zqPPvpV.png)

### 選取基數元素上色(進階處理):

一樣使用偽類 `nth-child(i)`裝飾元素

```javascript=
var odd = document.querySelectorAll('li:nth-child(odd)');

for (var i = 0; i < odd.length; i++) {
    odd[i].style.backgroundColor = 'green'
}
```
![](https://i.imgur.com/JZHvsxu.png)


# JavaScript DOM Crash Course Part - 2


## DOM的移動(traversing the DOM)

### parentNode

抓取目前物件的parent也就是外層的物件

```javascript=
var itemList = document.querySelector('#items');

//parentNode
console.log(itemList.parentNode);
itemList.parentNode.style.backgroundColor = 'red'
```

這邊抓取的是item的id它的parentNode是外層的div

![](https://i.imgur.com/SMvczhU.png)

然後我們對它修飾CSS

![](https://i.imgur.com/EAN1S7H.png)

並且parentNode的使用是可以疊起來的

```javascript=
console.log(itemList.parentNode.parentNode.parentNode);
```
會找的外層的外層的外層找到body去了

![](https://i.imgur.com/iaubbVR.png)


#### parentElement

幾乎跟parentNode的功能一樣是可以互相替換的

```javascript=
console.log(itemList.parentElement);
itemList.parentElement.style.backgroundColor = 'red'
console.log(itemList.parentElement.parentElement.parentElement);
```



### childNodes(不推薦使用)

```javascript=
console.log(itemList.childNodes);
```

中間包含的text是指斷行
![](https://i.imgur.com/FHpM5v5.png)

所以當你把它們全都黏在一起時text就會消失
![](https://i.imgur.com/bPek77e.png)
因為中間的斷行消失
![](https://i.imgur.com/Uu1IXD4.png)



### children(推薦使用)

* 功能跟childNodes一樣不過不會顯示出進去斷行
* 並且呈現方式變成HTMLCollection

```javascript=
console.log(itemList.children);
```
![](https://i.imgur.com/ir7eVwY.png)

如果想要擷取裡面的內容:

```javascript=
console.log(itemList.children[1]);
```
![](https://i.imgur.com/05rhgYt.png)

要修改選取元素的CSS:

```javascript=
itemList.children[1].style.backgroundColor = 'yellow';
```
修改其CSS為背景色黃色
![](https://i.imgur.com/oTxM0NZ.png)



### Firstchild(不推薦使用)

會印出第一個元素，但是這個方法一樣會印出斷行所以基本上會印出text

```javascript=
console.log(itemList.firstChild);
```
![](https://i.imgur.com/PVAXlcm.png)

### FirstElementChild(推薦使用)

這個就不會印出text搂

```javascript=
console.log(itemList.firstElementChild);
```
![](https://i.imgur.com/Rh8e3pJ.png)

當然也可以針對它選取的元素做文字修改

```javascript=
itemList.firstElementChild.textContent = 'hello 1';
```
![](https://i.imgur.com/bzI0VjC.png)

### lastchild(不推薦使用)

跟firstchild相反印出最後一個元素但是缺點是會印出斷行印出text

```javascript=
console.log(itemList.firstChild);
```

### LastElementChild(推薦使用)

不會印出斷行text以及也可以進行文字修改操作

```javascript=
console.log(itemList.lastElementChild);

itemList.lastElementChild.textContent = 'hello 4';
```
![](https://i.imgur.com/X4jRXQF.png)

### nextSibling(不推薦使用)

會抓取sibling 下一個位於同一層的元素，一樣的缺點會抓取斷行出現text

```javascript=
console.log(itemList.nextSibling);
```
![](https://i.imgur.com/mAxqpVQ.png)

### nextElementSibling(推薦使用)

不會出現斷行正常抓取下一個同層元素

```javascript=
console.log(itemList.nextElementSibling);
```
![](https://i.imgur.com/9tOolhe.png)

### previousSibling(不推薦使用)

會抓取前一個位於同一層的元素 ，一樣的缺點會抓取斷行出現text

```javascript=
console.log(itemList.previousSibling);
```

### previousElemntSibling(推薦使用)

不會出現斷行正常抓取上一個同層元素

並且可以進行操作

```javascript=
console.log(itemList.previousElementSibling);
itemList.previousElementSibling.style.color = 'green';
```
![](https://i.imgur.com/DRQYoAD.png)

### createElement

創造新的元素

```javascript=
var newDiv = document.createElement('div');

//增加class給div
newDiv.className = 'hello'

//增加id給div
newDiv.id = 'hello1';

//增加attribute給div
newDiv.setAttribute('title', 'hello Div');

//創造文字並指派給變數
var newDivText = document.createTextNode('Hello World');

//把文字加入div
newDiv.appendChild(newDivText);

console.log(newDiv);
```
印出的結果
![](https://i.imgur.com/pZS4l73.png)


把創造出來的div放進去專案中


```javascript=
//抓取想要放的位置
var container = document.querySelector('header .container');
var h1 = document.querySelector('header h1');

container.insertBefore(newDiv, h1);//使用方法插入newDiv
```
印出結果
![](https://i.imgur.com/KurzuOc.png)

修改newDiv 的CSS

```javascript=
newDiv.style.fontSize = '30px';
```
![](https://i.imgur.com/2az5Uqi.png)








# JavaScript DOM Crash Course Part - 3

這個部分的主題會環繞著事件(event)


## 事件監聽 (addEventListener)

新增一個按鍵等下作範例使用

![](https://i.imgur.com/bLfJ37T.png)

我們可以對這個案件做事件監聽，並且在事件'click'發生的時候跑buttonClick這個function會印出'Button clicked'字樣

```javascript=
var button = document.getElementById('button').addEventListener('click', buttonClick);

function buttonClick() {
    console.log('Button clicked');
}
```

![](https://i.imgur.com/RZTW93z.png)

funciton內部的功能也可以改成改寫header-title的文字:

```javascript=
var button = document.getElementById('button').addEventListener('click', buttonClick);

function buttonClick() {
    //console.log('Button clicked');
    document.getElementById('header-title').textContent = 'change';
     document.querySelector('#main').style.backgroundColor = 'red';
}
```
點擊Click Here後Title的文字會變成change並且背景色改變為紅色

![](https://i.imgur.com/FuNkv2p.png)


### 印出事件本身

會出現很多事件本身可以使用的方法(properties)例如 滑鼠位置 className altkey等等

```javascript=
var button = document.getElementById('button').addEventListener('click', buttonClick);

function buttonClick(e) {
console.log(e);
}
```
只擷取一部份
![](https://i.imgur.com/3bihVBZ.png)

### properties使用方式介紹跟結果:

這邊列出的properties都可以在上面印出來的MouseEvent裡面找到

```javascript=
var button = document.getElementById('button').addEventListener('click', buttonClick);

function buttonClick(e) {
console.log(e.target);// 印出觸發事件本身的元素
console.log(e.target.id);// 印出觸發事件本身的元素的id
console.log(e.target.className);//印出觸發事件本身的元素的className
console.log(e.target.classList);// 印出觸發事件本身的元素classList 使用DOMTokenList
console.log(e.type);//印出觸發事件本身的type是甚麼

//也可以這樣操作把取得的id文字加入欄位中用文字串接的方式
var output = document.getElementById('output123');
output.innerHTML = '<h3>'+e.target.id+'</h3>';
}
```
印出的結果
![](https://i.imgur.com/4MgIsuz.png)


把取得的id文字加入欄位中用文字串接的方式
![](https://i.imgur.com/hwflr7y.png)


### 滑鼠位置擷取

* clientX,Y 滑鼠在瀏覽器上的位置
* offsetX,Y 滑鼠在物件元素上面的位置


```javascript=
function buttonClick(e) {
console.log(e.clientX);
console.log(e.clientY);

console.log(e.offsetX);
console.log(e.offsetY);
}
```
當點擊Click Here之後會印出它們的位置:
![](https://i.imgur.com/w9it4nW.png)

### 判斷是否按住該按鍵進而可以做不同的功能

當按住該按鍵的時候會顯示true放開則顯示false，可以用做if判斷式來做不同的功能

如:
當按住alt時，顯示XXX之類的功能

* altKey
* ctrlKey
* shiftKey

```javascript=
function buttonClick(e) {

console.log(e.altKey);
console.log(e.ctrlKey);
console.log(e.shiftKey);
}
```

### 滑鼠事件簡介+一個小練習

* click
* dblclick
* mousedown
* mouseup

```javascript=
var button = document.getElementById('button')

button.addEventListener('click', runEvent);//單點擊啟動事件
button.addEventListener('dblclick', runEvent);//雙點擊啟動事件
button.addEventListener('mousedown', runEvent);//按下去瞬間就啟動事件
button.addEventListener('mouseup', runEvent);//滑鼠放開瞬間就啟動事件


function runEvent(e) {
    console.log('Event type:'+e.type);
}
```
印出的類型:
![](https://i.imgur.com/rc09izl.png)




#### 為了展示mouseenter event創造一個新的黃色div
![](https://i.imgur.com/2UWxHep.png)


##### mouseenter & mouseleave / mouseover & mouseout

當滑鼠進出的瞬間就會印出方法runEvent

他們的功能很像不過有差異:

mouseenter & mouseleave只會在進出物件的時候會觸發
mouseover & mouseout 則是除了進出之外碰到內部的子元素(這邊的例子是HELLO)都會觸發

```javascript=
var box = document.getElementById('box');
box.addEventListener('mouseenter', runEvent);
box.addEventListener('mouseleave', runEvent);
box.addEventListener('mouseover', runEvent);
box.addEventListener('mouseout', runEvent);


function runEvent(e) {
    console.log('Event type:'+e.type);
}
```
![](https://i.imgur.com/AzlLPxM.png)

#### mousemove

當滑鼠在物件內移動時觸發事件

```javascript=
var button = document.getElementById('button');
var box = document.getElementById('box');

box.addEventListener('mousemove', runEvent);

function runEvent(e) {
    console.log('Event type:'+e.type);
}
```
通常觸發次數很高
![](https://i.imgur.com/rzgJcmH.png)

#### 加上滑鼠的位置呈現在頁面上

先抓取id後並指派給output變數，抓取box id指派給box變數，
並把box加入事件監聽使用mousemove並印出它的value呈現在頁面上

這個output的位置
![](https://i.imgur.com/3iuiubk.png)


```javascript=
var box = document.getElementById('box');
var output = document.getElementById('output123');

box.addEventListener('mousemove', runEvent);

function runEvent(e) {

    output.innerHTML = '<h3>MouseX: '+e.offsetX+'<h/3><h3>MouseY:'+e.offsetY+'</h/3>';//這邊修改它的HTML內容加入新的<h3>tag以及滑鼠位置
    
}
```
印出來的結果位置:
![](https://i.imgur.com/Uw02oHL.png)

#### 下一步我們要做的事情是把抓取到的滑鼠座標位置轉換成RGB的數字，進而讓我們在物件內移動滑鼠的時候改變顏色


```javascript=

var box = document.getElementById('box');
var output = document.getElementById('output123');

box.addEventListener('mousemove', runEvent);

function runEvent(e) {

box.style.backgroundColor = "rgb("+e.offsetX+","+e.offsetY+",40)";
    //直接操作boxCSS修改其背景色為RGB並使用字串串接的方式改變RGB的顏色
}
```

結果如下:
![](https://i.imgur.com/wQzj2fS.gif)


### 處理上方的Add items

![](https://i.imgur.com/f34bXa1.png)

#### 當輸入文字在input區的時候就會觸發事件

```javascript=
var itemInput = document.querySelector('input[type="text"]');
var form = document.querySelector('form');

itemInput.addEventListener('keydown', runEvent);

function runEvent(e) {
    
     console.log('Event type:'+e.type);

}
```
![](https://i.imgur.com/S6UME9Q.gif)


### 簡介一些其他Event

* keydown  按下鍵盤時觸發
* keyup    離開按紐時觸發
* keypress 按住按紐時觸發
* focus    按在input中的時候觸發
* blur     離開focus時觸發
* cut      剪下內容時觸發
* paste    貼上內容時觸發
* input    在input內部做的任何事情跟內文有關係的打字剪下貼上等等都會觸發
* change   當抓取物件發生改變的時候觸發
* submit   當按下submit按鍵後觸發

```javascript=
itemInput.addEventListener('keydown', runEvent);
itemInput.addEventListener('keyup', runEvent);
itemInput.addEventListener('keypress', runEvent);

itemInput.addEventListener('focus', runEvent);
itemInput.addEventListener('blur', runEvent);

itemInput.addEventListener('cut', runEvent);
itemInput.addEventListener('paste', runEvent);

itemInput.addEventListener('input', runEvent);
itemInput.addEventListener('change', runEvent);

itemInput.addEventListener('submit', runEvent);

```



#### 讓輸入的文字內容完整地呈現在瀏覽器上

```javascript=
var itemInput = document.querySelector('input[type="text"]');
var form = document.querySelector('form');

itemInput.addEventListener('keydown', runEvent);

function runEvent(e) {

     console.log('Event type:'+e.type);

     console.log(e.target.value);
     //這邊抓取要呈現的地方也就是output123，並使用innerHTML修改內部內容使用文字串接e.target.value的方式呈現
     document.getElementById('output123').innerHTML = '<h3>'+e.target.value+'</h3>';

}
```

結果
![](https://i.imgur.com/atvgRy2.png)




#### 當選取下拉式選單的時候觸發事件使用"change"事件

一點選下拉選單就會觸發事件並印出事件類型

```javascript=
var select = document.querySelector('select');

select.addEventListener('change', runEvent);
// select.addEventListener('input', runEvent);  使用input也行得通會產生一樣的結果
function runEvent(e) {
     console.log('Event type:'+e.type);
}
```

![](https://i.imgur.com/vqeog9W.png)


#### 印出選取的下拉式選單的值

使用`console.log(e.target.value);`

```javascript=
var select = document.querySelector('select');

select.addEventListener('change', runEvent);
// select.addEventListener('input', runEvent);  使用input也行得通會產生一樣的結果

function runEvent(e) {

     console.log('Event type:'+e.type);
    console.log(e.target.value);
}
```

![](https://i.imgur.com/kVxXxvy.png)


#### 按下submit按鍵後印出type


```javascript=
var form = document.querySelector('form');

form.addEventListener('submit', runEvent);

function runEvent(e) {
    e.preventDefault();
     console.log('Event type:'+e.type);
}
```

![](https://i.imgur.com/7oZqkGu.png)




# JavaScript DOM Crash Course Part - 4


使用上面三個part做出一個真正的小作品來呈現

[作品程式碼](https://codepen.io/bradtraversy/pen/Bwapow)


作品Item Lister
![](https://i.imgur.com/cwzFqpF.png)

## 功能:

* 可以在Add items品項並且在submit後加入下方的items
* 點X有刪除功能
* 右上角可以搜尋已加入的items(filter)

## HTML:

```htmlembedded=
<body>
  <header id="main-header" class="bg-success text-white p-4 mb-3">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
            <h1 id="header-title">Item Lister</h1>
        </div>
        <div class="col-md-6 align-self-center">
            <input type="text" class="form-control" id="filter" placeholder="Search Items...">
        </div>
      </div>
    </div>
  </header>
  <div class="container">
   <div id="main" class="card card-body">
    <h2 class="title">Add Items</h2>
    <form id="addForm" class="form-inline mb-3">
      <input type="text" class="form-control mr-2" id="item">
      <input type="submit" class="btn btn-dark" value="Submit">
    </form>
    <h2 class="title">Items</h2>
    <ul id="items" class="list-group">
      <li class="list-group-item">Item 1 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
      <li class="list-group-item">Item 2 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
      <li class="list-group-item">Item 3 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
      <li class="list-group-item">Item 4 <button class="btn btn-danger btn-sm float-right delete">X</button></li>
    </ul>
   </div>
  </div>
    </div>
  </div>
  <script src="dom.js"></script>
</body>
```

## JS:


### 取得submit的值並且加入Items最底層

輸入123最底部加入123
![](https://i.imgur.com/jXzzTOJ.png)

```javascript=
//設置兩個變數並且指派抓取好的 form,item 區域
var form = document.getElementById("addForm");
var itemList = document.getElementById("items");

//form submit event  設置form區域submit事件並且設置新的funciton addItem來加入新的items
form.addEventListener("submit", addItem);

//add item 處理addItem內函式功能的身體
function addItem(e) {
  e.preventDefault();

  // get input value 用抓取到的變數加上(.value)來抓輸入的值
  var newItem = document.getElementById("item").value;

  //create new li element 要增加新欄位到Items下面所以創造一個"li"
  var li = document.createElement("li");

  //add class 其他li有的class他也得加上去
  li.className = "list-group-item";

  //add text node with input value這邊因為createTextNode是document的方法所以得這樣使用
  li.appendChild(document.createTextNode(newItem));
  
  // add del button element 抓取button
  var deleteBtn = document.createElement("button");

  // add classes to delete button 創造className
  deleteBtn.className = 'btn btn-danger btn-sm float-right delete';

  //append text node 把"X"加給delete btn
  deleteBtn.appendChild(document.createTextNode('X'));
    
  //append button to li 把delete btn 加到li
  li.appendChild(deleteBtn);

  // append li to list 把il加到list
  itemList.appendChild(li);
}
```
### 刪除加入的items

`confirm()`
用來跳出需要使用者確認的對話視窗，對話視窗中會有確定及取消兩個按鈕。

```javascript=

//delete event 做點擊事件
itemList.addEventListener('click', deleteItem);

//remove item

function deleteItem(e) {
    //這邊再判斷是否點擊的元素有包含delete這個class不然點整條form都會delete掉
    if (e.target.classList.contains('delete'))
    {    
        //這邊在使用confirm這個跳出視窗做判斷點擊是的話則執行
        if (confirm("Are you sure you want to delete?")) {
        
            //這邊把的e參數因為上面的判斷所以已經侷限在delete btn裡面了所以她的parentElement就是li也就是我們要刪除的對象
            var li = e.target.parentElement;
            
            //使用刪除removeChild元素li
            itemList.removeChild(li);
        }
    }
}
```

### filter篩選內容


`indexOf() `

方法返回啟動它的對像String中第一次出現的指定值的索引，從fromIndex處進行搜索。**如果未找到該值，則返回-1。**

```javascript=

//抓到filter這個id
var filter = document.getElementById("filter");


//filter event 創造事件keyup打字觸發事件發動filterItems
filter.addEventListener("keyup", filterItems);



// filterItems

function filterItems(e) {
    // convert text to lowercase
    var text = e.target.value.toLowerCase();
    //get lis

    // var items = itemList.getElementsByTagName('li');
    var items = document.querySelectorAll('li');

    //convert to an array
    //這邊因為想要使用forEach這個array方法所以直接把items轉換成array
    Array.from(items).forEach(function (item) {

        //這邊要使用firstChild來抓取item前面的名字不然就會連後面的"X"一起抓進來
        var itemName = item.firstChild.textContent;

        //抓進來的itemName一樣轉小寫，並使用indexOf判斷text是否不是-1(-1代表沒找到一樣的字串)
        //不是-1則執行下方的display 顯示出來
        //是-1則執行displaynone因為不一樣
        if (itemName.toLowerCase().indexOf(text) != -1) {
            item.style.display = 'block';
        } else {
            item.style.display = 'none';
        }
    
    });
}
```
