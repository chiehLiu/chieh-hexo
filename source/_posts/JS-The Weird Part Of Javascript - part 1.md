---
title: JS-The Weird Part Of Javascript - part 1(一萬字)
date:
tags: Javascript
category: Javascript
---

# The Weird Part Of Javascript - part 1


tags: Javascript relate
---

###### tags: `Javascript`


# Conceptual Aside

> 當我們寫好JS程式時，在執行時，我們宣告的變數、函式，就會呈現在記憶體中，由電腦去運作使用。


## 語法解析器 (Syntax Parsers)

翻譯程式:
* 直譯器(Interpreter)
* 編譯器(Compiler)

一個程式用來翻譯JS code成電腦可以理解的語法

## 詞彙環境 (Lexical Environment)

* 代表程式碼在程式中的實際位置
* 那些"翻譯程式"非常注重你把那些程式碼寫在哪以及當下環境是什麼


## 執行背景 (Execution Contexts)

* 別人寫好的程式來驗證以及執行使用者的程式碼
* 管理哪段程式碼先執行
* 管理的內容不只是使用者撰寫的還有更多


# Conceptual Aside

## 鍵值配(Name/ Value Pairs)

* 一個name 會配對到 一個 value
* 值(value) 也可以是 數個 name:value 的配對(也就是objects)


## 物件(Objects)

* 是數個name:value 配對的組合

address的值 裏面包含了數個鍵值配

```javascript=
address:{
    street:'Main',
    Number:'100',
    Apartment:{
        Floor:3,
        Number:301
    }
}
```

# The Global Environment and The Global Object

> 不論使用者的JS程式碼何時執行，它都會跑在執行背景(Execution Context)裡面，意味著別人已經寫好的程式會來驗證以及執行使用者的程式碼



## 基礎執行背景(Base Execution Context也就是Global Execution Context)

* 代表整段程式的任何地方都可以取用它們
* 基礎執行環境創造了兩個事情 1.Global Object 2.特殊變數 this


![](https://i.imgur.com/0AtZF3g.png)

就算使用者沒有撰寫任程式碼，JS引擎也會直接創造它們兩個

1.window(Global Object)(但如果在node.js運行的話會不一樣)
2.特殊變數 this

![](https://i.imgur.com/brA2yZq.png)

## Global

> 不在函式裡面就是Global
> Not Inside a Function

我們在IDE中輸入變數以及函式，會讓它們跟Glbal Object產生連結而我們剛剛設置的變數以及函式就變成了Global Object，因為它們都不在函式內部

```javascript=
var a = "Hello World!";

function b() {}
```

![](https://i.imgur.com/IbYW4PQ.png)

Execution Context會包裹住這些內容:

* Global Object(window)
* 'this'變數
* Outer Environment - Execution Context的外部環境
* Your Code(如果寫的位置不在任何函式內部)

![](https://i.imgur.com/UkmvpH1.png)


# The Execution Context: Creation And 'Hoisting'


## Hoisting 範例說明


```javascript=
var a = "Hello World!";

function b() {
  console.log("Called b!");
}

b();
console.log(a);
```

我們會預期這樣的程式碼得到下面的結果

![](https://i.imgur.com/z16LB4L.png)

---

但如果我們做些一些改變呢?

```javascript=
b();
console.log(a);

var a = "Hello World!";

function b() {
  console.log("Called b!");
}
```

如果有學過其他的語言應該會覺得這邊會直接出錯，因為程式碼應該是一行一行執行的，並且還沒宣告b函式所以b函式應該無法使用

但結果如下:

* 他執行了函式b()
* a的部份沒有出錯卻顯示undefined

所以儘管b函式在下方才宣告卻還是執行了，以及a的部份還是可以使用的雖然它目前是一個值undefined(尚未定義)，**這樣的現象被稱為'Hoisting'**，但並不是把宣告內容提升到最上方那麼單純!

![](https://i.imgur.com/kUSKFDe.png)

那我們直接把a移除會發生甚麼事呢?

```javascript=
b();
console.log(a);

function b() {
  console.log("Called b!");
}
```

出現錯誤訊息:a is not defined(沒有被定義)

![](https://i.imgur.com/vg4o9Ru.png)


---


## Execution Context is Created(Creation Phase創造階段)

> 變數或是函式沒有值卻還是可以取用
> JS會這樣運作是因為執行背景被分為兩個階段

### 第一階段創造(Creation Phase)

![](https://i.imgur.com/C7YYlAm.png)

**在記憶體內部設定好空間給變數以及函式被稱為'Hoisting'**

他的意思不是把程式碼移到最上方!!

而是在逐行執行程式碼之前也就是第一階段，JS引擎已經把變數以及函式設定好空間給它們了，也就是變數以及函式已經存在記憶體中，所以當程式逐行執行時，就可以使用它們



### 變數的不同點

不過變數的情況比較不一樣

```javascript=
b();
console.log(a);

var a = "Hello World!";

function b() {
  console.log("Called b!");
}
```


* 函式b()已經全部都在記憶體內了，代表他已經被執行了
* 但是JS騰出空間給變數a時，JS不知道它的值是什麼直到被執行了才知道所以會先放入undefined代表還不知道它的值就跟完全不設值的情況一樣

```javascript=
b();
console.log(a);

var a;

function b() {
  console.log("Called b!");
}
```
一樣會取得undefinded
![](https://i.imgur.com/qTbIzIe.png)


### 結論

* **所有的JS變數一開始都會被設定成undefined**
* **函式則是會被完全設定好放進記憶體裡**
* 所以盡量還是不要太依賴'Hoisting'，好好讓程式逐行執行的順序比較好!


# Conceptual Aside

## Javascript and Undefined

* undefined 是一個JS內建的特殊的值，代表這個變數還沒被設定
* undefined 是一個值並且實際佔據記憶體空間 代表一個變數的初始值
* undefined 是一個在變數再創造階段會被設定的值也就是(未設定)

下方程式碼代表undefine是一個特殊值不需要加上""

```javascript=
var a;

console.log(a);

if (a === undefined) {
  console.log("a is undefined");
} else {
  console.log("a is defined");
}
```

如果我們不宣告變數內容會得到undefined結果

```javascript=
var a;

console.log(a);
```

![](https://i.imgur.com/ZnYKpex.png)



## 作者建議

永遠不要設定變數為undefined，因為你其實可以這樣做並且不會出錯，但你會不知道出現的undefined是你設定好的還是程式碼中那些地方有出錯，最好使用的方式就是不設定它併用它來除錯

```javascript=
var a;

a = undefined; // 永遠別這樣做

console.log(a);
```


# The Execution Context: Code Execution

> 第一個階段是創造階段，第二個部分是執行

* 在創造階段就已經設定好所有東西
* 執行階段會執行使用者寫的程式碼**逐行**轉譯、轉換成電腦可以理解的內容

![](https://i.imgur.com/RMVW6WP.png)

## 範例說明

從下方程式碼以及結果可以理解:

* 程式碼逐行執行

第七行的a暫時還未指派因此印出結果為undefined
然後經過第九行新指派a = "Hello World!"，因此在11行重新印出a 的時候就印出被指派的內容Hello World!

```javascript=
function b() {
  console.log("Called b!");
}

b();

console.log(a);

var a = "Hello World!";

console.log(a);
```


![](https://i.imgur.com/89oShvj.png)



# Conceptual Aside

## 單執行緒(Single Threaded)

* 一次執行一個指令(使用者的視角)
* 瀏覽器下有很多程序在執行所以用瀏覽器的角度看的時候就不能這樣理解

## 同步執行(Synchronous Execution)

* 一次執行一行程式碼
* 並且按照順序
* 在JS中一次只會發生一件事情


# Funciton Invocation and The Execution Stack


## 函式呼叫(Funciton Invocation)

### Invocation

> 代表執行或是呼叫函式，會使用括號`()`

比方說要執行函式app可以這樣使用:

`app();`


## 執行堆(Execution Stack)

* 每個函式會多創造一層Execution Context
* 會逐行且同步地執行程式碼
* 執行結束後會從最上層開始拋棄

### 範例說明

橘色部分就是執行堆
![](https://i.imgur.com/mduoRi5.png)

每一層都會創造一個新的Execution Context都會經歷創造階段然後逐行執行程式，這邊就是函式被呼叫之後做事情
 
1. Global Execution Context 會處理所有的全域項目變數、函式等等
1. a() 這邊會創造一個嶄新的Execution Context 代表函式 a內的變數、函式
1. b() 這邊會創造一個嶄新的Execution Context 代表函式 b內的變數、函式

### 範例說明二

```javascript=
function a() {
  b();
  var c;
  console.log(c + " is c");
}

function b() {
  var d;
  console.log(d + " is d");
}

a();

var e;
console.log(e + " is e");

```

這邊可以先忽略undefined畢竟都沒指派內容當然都會是預設值，可以先注意印出順序
![](https://i.imgur.com/dOdzoLW.png)


> 執行堆最上方的程式就是正在執行的程式，逐行、同步地在被處理中

從上方程式碼可以理解函式呼叫以及執行堆的順序:

1. 呼叫 a();
2. 進到a的內部，這邊呼叫b()
3. 進到b的內部，印出 d (第一個印出結果)
4. 因為b()內部執行完成，所以從執行堆中移除換執行函式a()
5. 印出函式a()，印出 c (第二個印出結果)
6. 因為a()內部執行完成，所以從執行堆中移除換執行Global object(也就是最下面的e)並且印出



# Function, Context, and Variable Environments

## 變數環境(Variable Environments)

> 描述使用者創造變數的位置以及在記憶體中與其他變數的關聯，所以當你想到這個詞基本上就是在想變數在哪裡?

* 變數環境 = 變數的位置以及與其他變數的關聯
* 每個執行背景內部(Execution Context)的變數是不會彼此影響的


```javascript=
function b() {
  var myVar;
  console.log(myVar);
}

function a() {
  var myVar = 2;
  console.log(myVar);
  b();
}

var myVar = 1;
console.log(myVar);
a();
console.log(myVar);
```

![](https://i.imgur.com/1mC8Hv5.png)

上方的程式碼可以這樣理解:

> 每個執行背景內部的變數是不會彼此影響的

1. 印出13行結果 myVar = 1
2. 跑呼叫a()，內部函式印出結果 2，並且呼叫 b()
3. 進入函式b()，內部函式結果印出undefined
4. 執行堆移除函式b => 移除函式a => 回到Global Execution，15行在印出一次myVar = 1


# 範圍鏈(The Scope Chain)

* 簡單來說明就是當函式內部找不到變數時就會往外找(outer environment)而這個過程就是範圍鏈
* 函式的位置決定它的外部環境(outer environment)

![](https://i.imgur.com/7yVQZtW.png)


## 範例

```javascript=
function b() {
  console.log(myVar);
}

function a() {
  var myVar = 2;
  b();
}

var myVar = 1;
a();
``` 

印出myVar的結果是1
![](https://i.imgur.com/x6DtNiM.png)


由範例可以得知:

1. 呼叫a()
2. 進入函式a()，呼叫函式b()
3. 進入函式b()，內容需要印出myVar但內容沒有變數於是往外找
4. 函式b()的outer environment是Global Execution因此印出結果 1


## 範例二

我們把函式b()整個移進去函式a()內部

```javascript=
function a() {
  function b() {
    console.log(myVar);
  }

  var myVar = 2;
  b();
}

var myVar = 1;
b();
```

印出結果是錯誤 b is not defined
![](https://i.imgur.com/KJcmUHs.png)


由範例二可以得知:

* 呼叫函式b()位於Global Execution的環境中
* 位於Global Execution的環境中找不到函式b()，因為我們把它移動到函式a()裡面了
* 當呼叫函式找不到東西時就會顯示錯誤 `'XXX is not defined'`






## 範例三

函式b()的外層是函式a()

![](https://i.imgur.com/vvRCywU.png)


```javascript=
function a() {
  function b() {
    console.log(myVar);
  }

  var myVar = 2;
  b();
}

var myVar = 1;
a();
```

印出myVar的結果是2
![](https://i.imgur.com/Gj4zC6Q.png)


由範例三可以得知:

由於函式b()內部找不到變數因此往外層找到a()的`var myVar = 2;`故印出結果為2


## 範例四

去掉`var myVar = 2`

```javascript=
function a() {
  function b() {
    console.log(myVar);
  }

  b();
}

var myVar = 1;
a();
```
由範例四可以得知:

所以當 `var myVar = 2` 又被拉掉的時候，就會得到結果 1，因為又會繼續往外找
b的外層是a a的外層是Global Execution


# Scope, Es6, And let

## 範圍(Scope)

* 指的是變數可以被取用的區域
* 呼叫兩個函式它會各自有一個執行背景
* 如果有兩個看起來相同的變數但在記憶體中其實是兩個不同的變數(因為環境不同)

### 範例

```javascript=
function b() {
  console.log(myVar); // 步驟 4
}

function a() {
  function b() {
    console.log(myVar); // 步驟2
  }

  var myVar = 2;
  b();
}

var myVar = 1;

a();
console.log(myVar); // 步驟 3
b();
```

![](https://i.imgur.com/LcmlEqh.png)


從範例可以得知:

* 叫了兩遍一樣的函示b() 第11行、18行，他們會各有一個執行背景
* 這邊的變數myVar雖然變數名稱一樣但是結果完全不同
* 因為它們的範圍(scope)不同，並且處在不同的函式中彼此的變數不會互相干擾

1. 呼叫a() => 進去a()內部呼叫b()(位於a()內部)
2. b()內部的console找不到變數因此往外(函式a()是外部)找 故印出2
3. 接下來回到外層印出 Global Execution的 myVar = 1 故印出1
4. 最後又呼叫一次b()，很明顯地這次直接找尋了跟Global Execution位於同一層的b()(位於第一行)故印出結果往外找到myVar = 1 故印出1


## let簡介

* 區塊範圍(Block Scope) - 變數的作用範圍只限在大括號間`{}`


### 範例

```javascript=
var i = 0;

for (var i = 0; i < 10; i++) {
    console.log(`迴圈跑第${i}次`);
}

console.log(i);
```
很明顯的地方是外面的var i = 0被裡面的迴圈汙染到所以傳回來的結果是10
![](https://i.imgur.com/wexESY7.png)

所以改成let做操作時因為其作用域是{}因此沒有汙染到外面來

```javascript=
let i = 0;

for (let i = 0; i < 10; i++) {
    console.log(`迴圈跑第${i}次`);
}

console.log(i);
```
![](https://i.imgur.com/za2DaSb.png)


# What About Asynchronous Callbacks?

* JS引擎的內部處理方式是同步的，但是與外部引擎的合作就是非同步的
* 非同步的部分只是在於瀏覽器會把非同步的東西放進去Event Queue但JS依舊一行一行執行
* Event Queue的執行會排在執行堆任務執行完並且執行背景清除了才會動作

## 非同步(Asynchronous)

* 代表不只一件事情同時發生

但前面有說JS是同步的，那它會怎麼處理非同步事件呢?


![](https://i.imgur.com/ecNSwqe.jpg)

JS引擎其實在運行的時候，在瀏覽器下面還有其他的引擎同時在運行:

* 呈現引擎(Rendering Engine) - 處理畫面的呈現在螢幕上
* HTTP Request - 處理瀏覽器的HTTP請求，以及獲取資料

### 結論
所以我們可以理解的是JS引擎的內部處理方式是同步的，但是與外部引擎的合作就是非同步的(在瀏覽器下)


## 事件佇列(Event Queue)

* 當執行堆是空的 JS 才會注意事件佇列
 
當在瀏覽器中有一個事件需要被JS引擎處理時，就會被放在Event Queue排隊並且會被事件監聽並等待函式做處不過就是要等待在Event Queue之中
![](https://i.imgur.com/mfkOqWu.png)


上面提到Event Queue在排隊其實是在等Execution stack的任務處理完之後，才會輪到Event Queue的函式創造新的執行背景`clickHandler()`處理click事件接下來輪到HTTP Request(以圖片舉例)
![](https://i.imgur.com/9tyPbPp.png)

### 範例

![](https://i.imgur.com/gEUKBJ8.gif)

這個範例可以看出被放在Event Queue的事件(clickHandler)一直到執行堆的任務完成(3秒)之後才會執行，要等三秒函式完成並且清空execution stacks，才會跑Event Queue內的click事件。

```javascript=
function waitThreeSeconds() {
  var ms = new Date().getTime() + 3000;

  while (new Date() < ms) {}
  console.log("finished function");
}

function clickHandler() {
  console.log("click event!");
}

document.addEventListener("click", clickHandler);

waitThreeSeconds();
console.log("finished execution");
```

# Conceptual Aside

## 靜態型別(Static Typing)

常用在Java或是C#
代表必須在一開始就告訴編譯器目前使用的變數是甚麼型別

```java=
bool isNew = "hello"; 

// 前方就指示型別
// 明顯這邊會報錯因為'Hello'是字串不是布林值
```

## 動態型別(Dynamic Typing)

意味著你不需告訴JS引擎你使用的變數型別(字串、數字、布林值等等)，當程式執行時它會自己做辨識

```javascript=
var isNew = true; //不會報錯
isNew = 'yup!';
isNew = 1;
```

## 型別(Types And Javascirpt)


### 純值(Primitive Types)

* 是一種資料型態並且只代表一個值意味著不是物件


1. undefined

* 是所有變數的初始值
* 代表其值還尚未存在(千萬不要設到變裡)
* 會一直保持undefined直到你給變數設定值為止


2. null

* 代表其值"不存在"為空(可以設到變數裡)

3. Boolean

* 代表true or false其中一種可能

4. number

* 在JS中只有一種數字型態number(其他語言不是這樣可能有整數或其他類型)
* 它是一種浮點數代表後面總會有小數位
* 會讓數學在JS裡面比較奇怪

5. string

* 一連串的文字並且使用單引號或是雙引號包裹住
* Es6可以使用`(``)`包裹住文字並且使用變數在裡面

6. symbol

* 使用在ES6中尚未被全部瀏覽器支援
* 在後面的bouns課程會講解


# Conceptual Aside

## 運算子(Operators)

* 是種特殊的function並且在語法、寫法上都不一樣
* 一般來說運算子取兩個參數並且返回一個結果

### 範例

(+)加號運算子 做代表(-,>,<,% 這些也是一樣)

```javascript=
var a = 3 + 4;
console.log(a);
```

實際上 (+)的部分是是一個函式:

```javascript=
function +(a,b){
    return a+b;
}
```

但是我們要呼叫函式不是應該這樣寫嗎?

```javascript=
var a = 3 + 4;

+(3,4);
```

不過太惱人了對嗎? 還好JS提供了**中綴表示法 (Infix notation)**

讓我們可以把呼叫的部分寫在參數中間，讓程式看起來更人性化

```javascript=
3+4
```

# 運算子的優先性與相依姓(Operator Precedence and Associativity)

## 運算子的優先性

* 代表哪個運算子會被優先使用
* 當同一行程式有不只一個運算子時，函式會依序被呼叫
* 具備高優先性的運算子優先運算

## 運算子的相依姓

* 當優先順序都相同時才會使用到相依姓
* 代表運算子被呼叫的順序
* 左到右、右到左

## 範例

* 從下圖可以理解 *(乘號)的優先序高於 +(加號)

```javascript=
var a = 3 + 4 * 5;
console.log(a);

// a 為23
```

擷取自mdn
![](https://i.imgur.com/8UTEPpN.png)


* grouping - ()

相依姓最高的運算子，會優先計算括號內部的運算子

```javascript=
var a = (3 + 4) * 5;
console.log(a);

// a為35
```
擷取自mdn
![](https://i.imgur.com/duIO03J.png)



[運算子優先序參考 - MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)


## 範例二

```javascript=
var a = 2, b =3, c=4;

a = b = c;

console.log(a);
console.log(b);
console.log(c);

// 結果 4, 4, 4
```
* 印出結果都是四，因為他們都是相同的運算子具有相同的相同的優先性所以必須使用相依姓來處理，因此以MDN網站上的結果顯示必須從右到左執行
* a = b = c, 會先處理右邊的 等號(=) 所以會這樣執行:
a = (b=c)，必須先求出b=c，因c = 4，所以b = 4，外面則 a = 4


![](https://i.imgur.com/rg1yoF9.png)


# Conceptual Aside

## 強制轉型(Coercion)
 
*  轉換一個值從一個形態到另一個
(ex.你可能有的Number類型別被轉換成String)
*  在JS很常發生因為其為動態型別


## 隱性 vs. 顯性 (Implicit vs. explicit coercion)

### 顯性(explicit)

會直接顯示出要轉換的型別

````javascript=
Number(value)
````

### 隱性(implicit)

當指派運算子時:

 
```javascript=
1 == null, 2/’5', null + new Date()
```

當被轉換成boolean時:
```javascript=
if (value) {…}
````


## 三種強制轉換(Three types of conversion)

純值以及物件都只會有這三種轉換但是它們工作方式不太一樣

* to string
* to boolean
* to number

### 解釋純值轉型(Type coercion for primitives)

#### String conversion

* 顯性使用 String()函式直接轉換成字串
* 隱性使用 (+) 做轉換成字串，當兩個運算元(operand)有一方為字串就會觸發轉換成字串

```javascript=
String(123) // explicit
123 + ''    // implicit
```
* 所有的純值都可以被轉換成字串

```javascript=
String(123)                   // '123'
String(-12.3)                 // '-12.3'
String(null)                  // 'null'
String(undefined)             // 'undefined'
String(true)                  // 'true'
String(false)                 // 'false'
```

* Symbol 比較特別只能使用顯性的coercion

```javascript=
String(Symbol('my symbol'))   // 'Symbol(my symbol)'
'' + Symbol('my symbol')      // TypeError is thrown
```

* Symbol 使用所有數學運算子都會報錯

```
let uid = Symbol.for("uid"),
    sum = uid / 1;            // error!
```

[Symbol coercion - 參考](https://leanpub.com/understandinges6/read/#leanpub-auto-symbol-coercion)


#### Boolean conversion

* 顯性的使用`Boolean()`
* 隱性的必須使用在邏輯運算子的環境下或是被邏輯運算子直接影響

```javascript=
Boolean(2)          // explicit
if (2) { ... }      // implicit due to logical context
!!2                 // implicit due to logical operator
2 || 'hello'        // implicit due to logical operator
```

* 需要注意的是 ||以及&&運算子它們是會返回運算元的值的也就是不會返回true or false


```javascript=
// 返回123而不是true
// 'hello' and 123 在內部依舊是布林值來計算這個表達式
let x = 'hello' && 123;   // x === 123
```

* 下方列表以外的值都是返回true

```javascript=
Boolean('')           // false
Boolean(0)            // false     
Boolean(-0)           // false
Boolean(NaN)          // false
Boolean(null)         // false
Boolean(undefined)    // false
Boolean(false)        // false
```

* 物件、陣列、Symbol、Date、自定義function都會返回true

```javascript=
Boolean({})             // true
Boolean([])             // true
Boolean(Symbol())       // true
!!Symbol()              // true
Boolean(function() {})  // true
```

#### Numeric conversion


* 顯性的使用`Number()`函式

隱性的比較麻煩有多種觸發方式:

* 使用比較運算子(>, <, <=,>=)
* 使用位元算子( | & ^ ~)
* 算數運算子 (- + * / % )(注意當+包含的運算元有字串時會轉成字串)
* 單一使用+運算子
* 使用(==,!=)(注意當兩邊運算元都是字串時不會觸發數字轉型)

```javascript=
Number('123')   // explicit
+'123'          // implicit
123 != '456'    // implicit
4 > '5'         // implicit
5/null          // implicit
true | 0        // implicit
```

```javascript=
Number(null)                   // 0
Number(undefined)              // NaN
Number(true)                   // 1
Number(false)                  // 0
Number(" 12 ")                 // 12
Number("-12.34")               // -12.34
Number("\n")                   // 0
Number(" 12s ")                // NaN
Number(123)                    // 123
```

* 跳脫字元的部分如果內含不是數字則顯示NaN，為空則顯示0
* null, undefined比較特別需要特別記憶
* Symbols不能轉換為Number會直接報錯
```javascript=
Number("\n")                   // 0
Number(null)                   // 0
Number(undefined)              // NaN
+sym or sym | 0                // TypeError
```

[Symbol type conversions -MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol#symbol_type_conversions)


* 當== 應用到null, undefined時數字轉換不會進行
* null = null, null = undefined但不等於0

```javascript=
null == 0               // false, null is not converted to 0
null == null            // true
undefined == undefined  // true
null == undefined       // true
```

* NaN不等於任何東西連自己都不等於

```javascript=
if (value !== value) { console.log("we're dealing with NaN here") }

NaN === NaN
// return false
```

### 解釋物件轉型(Type coercion for objects)


#### 傳換成Boolean值

* 非純值的值都會轉成true
* 物件、陣列、空都會返回true

```javascript=
Boolean([NaN])
Boolean([123])
Boolean(['123'])
Boolean([false])
Boolean([undefined])

Boolean({NaN})
Boolean({123:123})
Boolean({'123':123})
Boolean({undefined})

//全部輸出都為true
```

#### 轉換成Number, String

* 物件會轉為純值藉由內部的`[[ToPrimitive]]`方法
* `ToPrimitive(input, PreferredType?)`(PreferredType可以為Number or String)
* 使用`valueOf` 、`toString` 

一般來說演算法如下:

1. 如果input已經是純值則直接返回
2. 呼叫input.toString() 如果結果是純值則返回
3. 呼叫input.valueOf() 如果解果是純值則返回
4. 都不是則產出TypeError

* 字串轉型 先呼叫 toString() 隨後 valueOf() 
* 數字轉型 先呼叫 valueOf() 隨後 toString()

過程是這樣的：

一個物件 obj 透過呼叫 ToPrimitive(obj, Number) 轉換成原始型別，接著在使用 ToNumber() 取得最後的結果


一個物件 obj 透過調用 ToPrimitive(obj, String) 轉換為原始型別，然後 ToString() 取得最後結果


* 可以觀察這個實作理解其觸發順序:
```javascript=
var obj = {
  valueOf: function () {
    console.log('valueOf')
    return {}
  },
  toString: function () {
    console.log('toString')
    return {}
  }
}

Number(obj); // 先印valueOf, 在接toString
String(obj); // 先印toString, 在接valueOf
```


* 大多數的build-in type方法不包含`valueOf()`或是會返回this.object(也就是會把同樣的元素回傳)然而並不是純值而被忽略，所以數字或是字串轉型可能都會返回呼叫`toString()`的內容
舉例:
![](https://i.imgur.com/1Xcp7FK.png)



#### loose equality(==), (+)這兩個運算子有特別之處

* 大多數的情況當這兩個運算子出現時都會預設使用Number 轉換
* 除了Date()
預設Date()會出現現在時間的字串
![](https://i.imgur.com/yDrcFGu.png)


## 小練習

```javascript=
true + false             // 1
12 / "6"                 // 2
"number" + 15 + 3        // 'number153'
15 + 3 + "number"        // '18number'
[1] > null               // true
"foo" + + "bar"          // 'fooNaN'
'true' == true           // false
false == 'false'         // false
null == ''               // false
!!"false" == !!"true"    // true
['x'] == 'x'             // true 
[] + null + 1            // 'null1'
[1,2,3] == [1,2,3]       // false
{}+[]+{}+[1]             // '0[object Object]1'
!+[]+[]+![]              // 'truefalse'
new Date(0) - 0          // 0
new Date(0) + 0          // 'Thu Jan 01 1970 02:00:00(EET)0'
```

### 題目解題

* true + false             // 1

使用 + 運算子會轉換成Numbe轉換
true = 1
false = 0

```javascript=
true + false
==> 1 + 0
==> 1
```

* 12 / "6"                 // 2

算數運算子 / 會轉換成Number轉換

```javascript=
12 / '6'
==> 12 / 6
==>> 2
```

* "number" + 15 + 3        // 'number153'

(+) 運算子的相依姓是由左自右
1. 所以這邊會先處理"number" + 15
2. 因為+號兩側有字串直接轉成字串"number15"
3. 在來處理 "number15" + 3 => "number153"

```javascript=
“number” + 15 + 3 
==> "number15" + 3 
==> "number153"
```

* 15 + 3 + "number"        // '18number'

1. 15+3 這邊就正常運算
2. 18+'number'因為有字串所以就變成'18number'

```javascript=
15 + 3 + "number" 
==> 18 + "number" 
==> "18number"
```

* [1] > null //true

比較運算子(>)會觸發Number轉換

```javascript=
[1] > null
==> '1' > 0
==> 1 > 0
==> true
```

* "foo" + + "bar"   //"fooNaN"

1. 單位元的 (+)運算子的優先級高於二進制(+)
1. 故+"bar" 先處理 因為轉型Number後內容物不是number故產出NaN
1. 跟"foo"串接觸發字串轉換故結果為"fooNaN"

```javascript=
"foo" + + "bar" 
==> "foo" + (+"bar") 
==> "foo" + NaN 
==> "fooNaN"
```
 
* 'true' == true  //false
* false == 'false'    //false

1. == 運算子觸發Number轉換
1. 'true' 轉換成Number轉換 因內容不是數字因此為NaN
1. 布林值 true的部分轉換成數字為1/ false為0
1. 所以他們不相等

```javascript=
'true' == true
==> NaN == 1
==> false

false == 'false'   
==> 0 == NaN
==> false
```

* null == ''   //false

Null比較特別
* 當== 應用到null, undefined時數字轉換不會進行
* null = null, null = undefined但不等於0

```javascript=
null == ''
==> false
```

* !!"false" == !!"true" //true
* 兩個驚嘆號代表如果內容為true則會顯示true
* 一般字串沒有為空的話是會顯示true的
* 下面是會顯示false的範例:
1. null;
1. NaN;
1. 0;
1. empty string ("" or '' or ``);
1. undefined.

```javascript=
!!"false" == !!"true"  
==> true == true
==> true
```

* ['x'] == 'x'   //true

1. == 觸發Number轉換
1. ['x'].valueOf()會得出他自己["x"] 這並不是純值所以不會返回結果
1. 故使用toString()得到"x"因此相等

```javascript=
['x'] == 'x'  
==> 'x' == 'x'
==>  true
```

* [] + null + 1    // 'null1'

1. (+)號運算子觸發Number轉換給[]
1. 然而陣列做Number轉換後因為陣列做`valueOf()`得出自己不是純值無法返回
1. 因此使用`toString()`空陣列轉為''空字串
1. '' 空字串出現在 (+)運算子中所以變成'null'+1 在得出結果'null1'

```javascript=
[] + null + 1  
==>  '' + null + 1  
==>  'null' + 1  
==> 'null1'
```

* 0 || "0" && {}     //{}

1. 邏輯運算子會轉換運算元為布林值(內部)但會返回原本的值
1. 0為false, "0"字串為true因為不為空, 空物件為true
1. || 運算子只要有false則取其左邊的值，&& 運算子如果運算元都為true取右邊的值故為{}

```javascript=
0 || "0" && {}  
==>  (0 || "0") && {}
==> (false || true) && true  // internally
==> "0" && {}
==> true && true             // internally
==> {}
```

* [1,2,3] == [1,2,3]   /false

1. 不需要強制轉型因為兩邊的型別一樣
1. ==會確認物件的id然而兩個array是不同的instance,id一定不同所以答出false

```javascript=
[1,2,3] == [1,2,3]
==>  false
```

* {}+[]+{}+[1] //'0[object Object]1'

1. (+)觸發Number轉型(但是因為物件以及陣列都會切換成toString())從最左邊開始轉換
1. 第一個{}轉換成""(透過toString())但因為沒有+在前面轉換成數字所以先不理
1. +[]會轉換成0
1. {}會轉換成字串'[object Object]'
1. [1]toString()會變成'1'
1. 最後做字串串接得出'0[object Object]1'
```javascript=
{}+[]+{}+[1]
==> +[]+{}+[1]
==> 0 + {} + [1]
==> 0 + '[object Object]' + [1]
==> '0[object Object]' + [1]
==> '0[object Object]' + '1'
==> '0[object Object]1'
```

* !+[]+[]+![]    //'truefalse'

1. 驚嘆號邏輯運算子優先權大於(+)
1. 故有驚嘆號的地方先處理(!+[]) + [] + (![])
1. !+[] => !=false, +[] = 0 = false ,兩個false則為true
1. ![] => []為true, 故得出false
1. [] => 做Number轉後轉成''
1. 三個串起來'truefalse'


```javascript=
!+[]+[]+![]  
==> (!+[]) + [] + (![])
==> !0 + [] + false
==> true + [] + false
==> true + '' + false
==> 'truefalse'
```

* new Date(0) - 0 //0

new Date(0).valueOf()會取得毫秒

```javascript=
new Date(0) - 0
==> 0 - 0
==> 0
```

* new Date(0) + 0 //'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)0'

1. new Date(0) 會出字串
1. 把0做String轉型
1. 串接得出答案'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)0'

```javascript=
new Date(0) + 0
==> 'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)' + 0
==> 'Thu Jan 01 1970 02:00:00 GMT+0200 (EET)0'
```

## 本篇參考來源: 

[JavaScript type coercion explained](https://www.freecodecamp.org/news/js-type-coercion-explained-27ba3d9a2839/)


# 比較運算子(Comparison Operators)

## 範例

* 兩個範例的優先順序都是一樣的(畢竟符號都一樣)
* 故比較的是相依姓(<)，(>)排序是由左至右

```javascript=
console.log(1<2<3)

// 結果得出 true
```
第一題處理:

1. 1<2 會得到 true, 接著處理true<3
1. 比較運算子會做Number強制轉型 true轉型為數字為1![](https://i.imgur.com/gw7Dkeg.png)
1. 故1<3 為true


```javascript=
console.log(3<2<1)

// 結果得出 true
```

第二題處理:

1. 3<2 會得到 false, 接著處理false<1
1. 比較運算子會做Number強制轉型 false轉型為數字為0 ![](https://i.imgur.com/9vLEghi.png)
1. 故0<1 為true

## null, undefined 是特別的

* 當== 應用到null, undefined時數字轉換不會進行
* null = null, null = undefined但不等於0

* 雖然使用Number()函式來取得數值 null有取得0，undefined取得NaN但是還是不能應用在(==)
![](https://i.imgur.com/tzWiWI3.png)

* 不過null<1是得出true ![](https://i.imgur.com/JxDpW2I.png)



```javascript=
null == null            // true
undefined == undefined  // true
null == undefined       // true
```


但是當情況越演越烈:

這樣強制型別轉換會讓程式碼難以預期，於是我們往下介紹**(===)Strict Equality**

```javascript=
null<1 // tru
"" == 0 //true
"" == false // true
```

## (===)Strict Equality

這個符號他不會強制轉換型別，如果運算元型別不同就會直接跑false

![](https://i.imgur.com/PqvIMJD.png)

## 作者建議

* 大多數的時間使用 (===)Strict Equality
* 除非你真的需要強制轉型來做一些功能不然不要輕易使用(==)
* 作者推薦文章 [內含(==, ===)比對表格 MDN](http://www-lia.deis.unibo.it/materiale/JS/developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness.html)


# 存在以及布林值(Existence and Booleans)


* 如果我們試著轉化null, undefined,"" 成布林值都會取得false
* 因此可以利用這個狀況使用if判斷式來尋找是否變數存在於內容之中
如果a存在的話則印出console.log()的內容

```javascript=
var a; // a is undefined
if (a) {
    console.log('Something is there.');
}
```


# 預設值(Default Values)

如果我們使用這個函式並且不輸入參數會發生什麼事呢?

```javascript=
function greet(name) {
  console.log('Hello' + name);
}
greet();
```

會印出Helloundefined，因為變數在這邊沒有被指定的情況下，預設值就會是undefined，然後碰上(+)運算子只要前方有字串就會把純值undefined轉換成字串因此得出這個結果
![](https://i.imgur.com/sGylF11.png)


但我們可以這樣寫讓這個預設值更有功能性:

* 使用 or 運算子
* 因為or運算子的優先級高於 (=)所以右邊會先處理
* 當name為undeined時因為or運算子會回傳true的結果也就是'Your name here'
* 當name不為undefined時就立即回傳，因為當兩邊都為ture時會回傳左側
* 唯一例外則為使用 0 因為 0 會回傳false
* 最後記得ES6有新的方法可以做參考使用

```javascript=
function greet(name) {
   name = name || 'Your name here';
   console.log('Hello' + name);
}
greet('Joan');
```

# 框架小叮嚀(Framework Aside)

想像一種情況當我們要使用複數個框架或是函式庫時，其中的變數名稱重複了，這時候撰寫位置於下方的程式會複寫上方的:

以下方的範例舉例的話，Lib2的變數內容會取代Lib1

```htmlembedded=
<script src="Lib1.js"></script>
<script src="Lib2.js"></script>
<script src="app.js"></script>
```

所以常常會看到函式庫使用預設值來避免這種被取代的現象發生:

* 如果變數已經存在(libraryName)則會使用現有的library的變數，如果沒有則使用Lib2
* 這樣的使用預設值的方式就是在檢查全域命名空間(global namespace)

```javascript=
window.libraryName = window.libraryName || "Lib2"
```