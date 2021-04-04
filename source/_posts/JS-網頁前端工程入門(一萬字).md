---
title: JS-網頁前端工程入門(一萬字)
date:
tags: Javascript
category: Javascript
---


# 網頁前端工程入門 
---
tags: Javascript relate
---

###### tags: `Javascript`

## Javascript 簡介

*  現代網頁的必需品
*  Java V.S Javascript

接下來他介紹了可以在HTML檔案裡寫入JS的其中一種方式如下:

![](https://i.imgur.com/czM75KC.png)


## Javascript 變數與運算子

* 資料: 數字 字串 布林值 物件
* 變數: 可存放資料的空間並且它可以命名
* 運算子: 可對資料做操作的符號


### 單行的註解以及多行註解:

![](https://i.imgur.com/q6YqNsN.png)


### 數字 字串(需要""包裹或是''包裹) 布林值

![](https://i.imgur.com/0Y3B0De.png)


### 變數

*  需要宣告並且賦予值之後才能跑
*  等號右邊的值被抓取給變數
*  可以被覆蓋，跟文章一樣有順序由上至下

![](https://i.imgur.com/JB1XwY5.png)

### 運算子

常見的有加減乘除

單元運算 `++`把數值加一
result`++` => result = result + 1

![](https://i.imgur.com/tHnVQHQ.png)

### 布林值

比較運算 

![](https://i.imgur.com/DvCSF3M.png)

一個 = 是指派
兩個 = 是相等的值

![](https://i.imgur.com/VAxT3TU.png)

也可以用變數做運算

![](https://i.imgur.com/G42xNwd.png)


### 輸入、輸出

使用者有感的程式:

輸入: `prompt(提示語,預設值)`-> 程式做運算 -> 輸出:`alert(資料)`

prompt的效果裡面的提示語是字串"請輸入數字"，"1"就是預設值

![](https://i.imgur.com/NDC9t6U.png)


一個簡單的可以跟使用者互動的程式:

![](https://i.imgur.com/QHcrp0S.png)


## 流程控制

* 判斷式
* 迴圈


### 第一個: if

`if(){}`

當小括號的布林值為true的時候會跑後面大括號的程式，如果為false則跳過

![](https://i.imgur.com/mUp72db.png)

像這邊就會讓使用者輸入值並去判斷大小，再根據判斷內容去決定是否跑後面的程式

![](https://i.imgur.com/oIxiI6C.png)


### 第二個:  else

當if後面的比較式出錯之後就會跑else

![](https://i.imgur.com/d4BF56Z.png)

### 第三個: else if

會一直做判斷如果都不是true的話則執行else

![](https://i.imgur.com/ya7BbMw.png)

一個簡單的四則運算使用上面所學:

一個重點在於prompt會要求輸入字串所以必須做資料型態轉換

![](https://i.imgur.com/SuiUIC0.png)


## 迴圈 

### while迴圈(跟if不一樣的地方在while會一直跑)


下圖就是個很好的while的範例，他會跑50遍在n變成51的時候跳脫迴圈被印出51

![](https://i.imgur.com/iOoAJMj.png)

另一個很常見的1+~100:

![](https://i.imgur.com/PQUcHTq.png)

### do 迴圈

還有個do 迴圈跟while不一樣的是do 一定會跑至少一次，while如果條件不成立就一次都不會跑。

下圖可以觀察出do 的執行式在上面所以他一定至少會跑一次程式
![](https://i.imgur.com/LY35pGc.png)

### for迴圈

* 第一個分號之前initializes整個loop，同時定義binding
* 第二個部分check整個loop要不要繼續跑
* 最後一個部分更新整個loop狀態在每一次迴圈結束之後

![](https://i.imgur.com/MfL6MgZ.png)


### break 強制跳出迴圈

直接跳出迴圈印出50:

![](https://i.imgur.com/Mcs874U.png)


### continue 強制進行下一次的迴圈

因為continue會強制進行迴圈所以下方的x被省略了25次也就是100裡面整除4的數字的數量所以印出75

![](https://i.imgur.com/KN8UGdW.png)


## 迴圈仔細新手教學

計算1+~+50:
![](https://i.imgur.com/V5Q7i0G.png)

建議直接把數字帶進去可以幫助理解:
![](https://i.imgur.com/DXicri4.png)


這邊來理解continue:

觀察下方追蹤的數字可以發現x必須執行兩次才會+1一次，所以印出x是50

![](https://i.imgur.com/ZBFFWKK.png)


![](https://i.imgur.com/m4gShlK.png)


## 函式教學

### 函式基礎

#### 內建函式

人家內建好的程式碼，例如:
`alert();`

#### 設計階段

當多個參數的時候可以使用(,)隔開

```javascript=
function test(message//參數名稱){
//函式的本體
    alert(message)
}
```
#### 呼叫/使用階段

```javascript=
test("Helloe World"//傳入函式的參數資料);
```

這邊的result因為上方function沒有輸入return回傳值，所以下面的alert(result)會回傳undefined

![](https://i.imgur.com/uWbVPIC.png)

因此這邊要介紹到reture，他會把函式本體跑的結果回傳到呼叫的位置，這樣下方的alert(result)就會回傳7瞜!

![](https://i.imgur.com/qFu3lbH.png)

return回傳明確可以做些甚麼呢?可以再利用return回傳到呼叫位置，再去做運算結果會得掉210!

![](https://i.imgur.com/0aWqZD2.png)

#### 整合範例

因為函式就是設定一個方法來做重複使用，所以數字上面不能寫死，用max來代替之後輸入max值之後就可以用在其他地方了

![](https://i.imgur.com/hFagRlX.png)




### 函式變形與名稱空間


#### 函式變形
創造函式有兩種方法:

第一種就是上面介紹的創造函式
![](https://i.imgur.com/z9xYOMS.png)

第二種比較像是使用變數指派函數給變數
![](https://i.imgur.com/Q8OdUrz.png)

所以她是可以這樣使用的像是變數一樣改變指派的內容一樣可以跑這個函式
test後面的add就代表函式的本體(因為她沒有做呼叫)
![](https://i.imgur.com/6YuDkPG.png)

判別x後面的資料是什麼他就可以做甚麼事情
![](https://i.imgur.com/WBxkE6L.png)


#### 函是創造新的名稱空間

變數找不到往外找

!!外部的程式碼不能使用內部的變數!!

![](https://i.imgur.com/iv0M4uM.png)


## 物件object

### 建立物件:

```javascript=
var point = new Object();

point.x=3; //物件裡面裝的東西不是函式就是屬性
point.y=4;
point.getPosition=function(){//如果是函式就是方法
alert(this.x+this.y);
};

//使用物件

//這邊跟函式的呼叫很像
point.getPosition();
```

綜合範例

![](https://i.imgur.com/6Y008E5.png)


### 使用建構式:

建構式就是要取代設計的部分讓未來要產生類似的物件的時候會更輕鬆

建構式的函式呼叫必須加上new

　![](https://i.imgur.com/BwJ96JP.png)

紅框框的部分是讓這個函式可以讓複數的變數呼叫

![](https://i.imgur.com/52TGuOM.png)


## HTML DOM

### 基本教學

然後有個小地方windows這個部分可以不寫程式一樣可以正常執行

這張圖特別重要這張圖就代表DOM  
![](https://i.imgur.com/MfGGsvP.png)

下圖可以看出那個樹狀圖出現在程式碼中並且加上一個innerHTML去修改裡面的內容:

![](https://i.imgur.com/fDEaHMp.png)

但是他修改整個body會導致泛用性不高因此可以這樣改:

使用getElementId的工具來取的id來做修改這樣子就到處都可以用摟!

![](https://i.imgur.com/p2nuB1D.png)


剛剛上面都是修改內容其實還可以修改CSS:

這邊有個重點因為CSS裡面有很多功能有包含(-)JS不能使用，因此都改成字首大寫例如:font-weight會改成fontWeight

![](https://i.imgur.com/RW70Ynv.png)


### 選單操作開合範例

使用onclick在HTML裡面，並且設定id去操作:

![](https://i.imgur.com/ZmJX3be.png)


不過在搭配class 選擇器使用之後可以讓他更精簡:

![](https://i.imgur.com/apqRb7S.png)


![](https://i.imgur.com/l5oNcaM.png)


接下來當選單不只一個需要開闔的時候就可以放入編號:

並且在選單處的id放入編號就可以針對點擊的選單收放摟!

![](https://i.imgur.com/u22EjXv.png)


## 事件處理

### 基本教學

基本上任何標籤都可以加上事件處理:on+事件的名稱

當使用者對畫面做出動作的時候，程式必須偵測到這個動作並且做出反應

最簡單的就是點擊`onclick`:

![](https://i.imgur.com/zNACDqg.png)

類似CSS裡面的hover功能:

`onmouseover`

`onmouseout`


![](https://i.imgur.com/NbmZWGh.png)

![](https://i.imgur.com/V1lhneK.png)

靜態的事件處理器:

直接寫入HTML裡面，不推薦這樣寫
![](https://i.imgur.com/VOqJuIx.png)



動態的事件處理器:

必須先在要處理的tag裡面設置id，這邊是設置"btn"

下方的addEvenListener是比較好的寫法

![](https://i.imgur.com/NbK1u2M.png)

有很多的功能參數使用在事件裡面，例如: click, mouseover, focus, blur....
![](https://i.imgur.com/H0oIswo.png)

[MDN網站:事件參考](https://developer.mozilla.org/zh-TW/docs/Web/Events)

### 事件物件的取得和使用


這是個簡單的跳出式窗hello的程式在你點擊瀏覽器之後

```javascript=
function init(){ // 這邊這個init會對應到HTML中tag裡面
    var btn=document.getElementById("btn");
    var handler=function(){ // 註冊函式
        alert("hello");
    };
    btn.addEventListener("click", handler); // 註冊事件處理器
}
```



有三件事情會發生在當你點擊瀏覽器上的物件後:

* 使用者點擊了按鈕，觸發了click事件
* 瀏覽器主動收集和事件有關的資訊，並製造出Even object 事件物件
var eventobj=事件物件
* 呼叫已經註冊的事件處理器(事件處理函式)

這要先做取得事件物件:

這邊的事件物件就是滑鼠的座標

![](https://i.imgur.com/9E4QuzQ.png)


這邊的事件物件就是鍵盤的代表的值

比較特別的點是他直接把註冊的函式直接寫入處理器裡面，這種作法叫做匿名函式直接當作事件處理使用
![](https://i.imgur.com/bSWS2AZ.png)


## 自動排程

一個簡單的基本例子:

讓瀏覽器在1秒之後跳出alert視窗說HELLO

![](https://i.imgur.com/j8e2oJo.png)


一般自動排程的應用

這邊介紹`window.setTimeout`這個倒數工具:

![](https://i.imgur.com/OJXsARi.png)

`window.setIterval`

使用這個工具的話就不需要再if那邊再重新倒數一次因為它會在設定的時間後每次都執行一次:

![](https://i.imgur.com/73wUXNE.png)

## 跨平台的網頁伺服器架設教學


[chrome插件網址](https://chrome.google.com/webstore/detail/web-server-for-chrome/ofhbbkphhbklhfoeikjpcbhemlocgigb/related)


* 程式中選擇資料夾
* 開啟伺服器或式關閉伺服器按鈕
* 測試網站的網址

![](https://i.imgur.com/GmiEH3q.png)

下方有個可以輸入port值，當要正式上線的時候可以使用80這個值

![](https://i.imgur.com/p57vPB1.png)


在資料夾裡面放入HTML檔就可以測試檔案瞜!


## Ajax教學 - JS 與伺服器的互動

> 用程式來做網路的連線就是Ajax

這邊有使用到 `get` 來送出資料在使用onload來把資料載入頁面藉由搜尋HTML裡面的id處理

![](https://i.imgur.com/hIYACq3.png)

## JSON基本教學

Javascript object Notation(Javascript 物件表示法)

JSON可以讓一般object做到比較簡潔寫法

上下兩個表達一樣的東西:
![](https://i.imgur.com/IZFF1lD.png)




`JSON.stringify`
回應使用JSON編碼過後的內容回來並且轉換成字串，但是它會忽略函式(get不見了)
把上面的point轉換成字串輸出
![](https://i.imgur.com/OkrD8Bh.png)
![](https://i.imgur.com/XZt8be4.png)

`JSON.parse`
擷取出被編譯前的內容出來將字串轉換成物件結構又轉換回來的概念
![](https://i.imgur.com/AyDf3mL.png)
![](https://i.imgur.com/JUwM7IJ.png)


## Hoisting 宣告提升

前端工程師面式的常見議題:

### 變數與函式的宣告提升 Hoisting

JS程式在執行的時候會內建把變數往上提升，所以就算這樣寫，跑出來的結果也是正常的10

![](https://i.imgur.com/sqSdBm0.png)

這邊要特別注意只有宣告變數提升而已，給定初始值並不會提升所以這邊的結果會印出undefined

![](https://i.imgur.com/yUgavdK.png)


在JS裡面可以先呼叫函式在寫宣告也一樣可以執行，因為函式的宣告跟變數的宣告一樣會被提升到程式的最上方
![](https://i.imgur.com/oYRQ5pt.png)

這邊一樣要特別注意的點是變數一樣只有宣告的部分提升函式的部分留在原地所以一樣沒有執行

![](https://i.imgur.com/H91XNnV.png)

