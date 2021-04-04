---
title: JS-The Weird Part Of Javascript - part 2(一萬字)
date:
tags: Javascript
category: Javascript
---

# The Weird Part Of Javascript - part 2


tags: Javascript relate
---

###### tags: `Javascript`




# 物件與函式 (Objects And Functions)

> 在其他程式語言中物件、函式是兩種完全不同的存在，但是在JS裡面它們非常相似

## Objects And The Dot

* 物件(objects)是鍵值配對 (name:value pair) 的集合(不一定只有一對)
* 物件內可以包含有純值(Primitives)、另一個物件(Objects)、函式Function(或稱方法method)
* 上面標示的0x001是記憶體內部位置的範例，就像是它們的地址

![](https://i.imgur.com/zt3XHMD.png)

### 範例

這邊是為了作範例而這樣製作物件，不過會有更好的方式會在後面的章節介紹

```javascript=
var person = new Object();

person["firstname"] = "Tony";
person["lastname"] = "Alicea";

var firstNameProperty = "firstname";

person.address = new Object();
person.address.street = "111 Main St.";
person.address.city = "London";


console.log(person); //得到object
console.log(person["firstname"]); //得到Tony
console.log(person[firstNameProperty])//得到Tony
console.log(person.firstname);//得到Tony
console.log(person.address.street); //得到111 Main St.
console.log(person.address.city);//得到London
```

1. 我們設置一個物件person，並且新增兩個屬性firstname,lastname
1. 把firstname指派給變數，一樣可以使用變數取得新增的內容
2. 使用(.)可以更方便的新增屬性以及取得物件內容
3. 使用 [ ] , (.) 這兩個運算子都能取得物件內容以及新增屬性

![](https://i.imgur.com/tLJUO9h.png)


[ ]  運算子

* 需要使用字串型態
* 可使用變數指派的方式使用

(.) 運算子

* 編譯器可以直接閱讀不需要使用字串型態
* 不可使用變數指派方式使用
* 更簡潔易讀

![](https://i.imgur.com/QFtKBuI.png)


# 物件、物件實字(Objects And Object Literals)

* 為了創造物件我們可以使用{ } 是 `new Object();`的縮寫
* {} 不是運算子
* JS引擎會判斷使用{ } 就是正在創造物件
* 只要用{ } 來建立物件的語法，就稱為物件實字 (Object Literals)

```javascript=
var Tony = {firstname:'Tony',lastname:'Alicea'};
console.log(Tony);

var Tony = new Object();
person.firstname = "Tony";
person.lastname = "Alicea"

console.log(Tony);
```
會印出一樣的結果
![](https://i.imgur.com/aUcJqIY.png)


**物件創建在物件之內**

```javascript=
var Tony = {
    firstname:"Tony"
    address:{
        street:'111 Main St.',
        city:'New York'
    }
}
```

**創建在函式內部**

```javascript=
function greet(person){
 console.log('HI' + person)
};

greet({
firstname:'Mary',
lastname:'Doe'
});
```

**使用在增添屬性上面**

```javascript=
Tony.company = {
    street: '333 Second St.',
    companyName: 'Sucess'
}
```


# 框架小叮嚀(Framework Aside)

* JS是沒有namespace，因為{ }的關係不需要
* 可以使用{ } 創造出物件來假扮命名空間
* 在框架或是函式庫的原始碼中很常看到這樣的使用方式

## Faking Namespaces

### 命名空間(Namespace)

專門給變數以及函式使用的空間，讓同樣名字的變數或是函式可以做區隔

### 範例

兩個變數名稱一樣時上方的變數會被複寫，因此印出Hola!

```javascript=
var greet = 'Hello!';
var greet = 'Hola!';

console.log(greet); // Renders Hola!
```

為了避免上面的複寫情況發生，我們可以使用Faking Namespaces，創造一個物件來包裹住這些變數，這樣就能避免變數或是函式之間名字相同的衝突或是複寫的狀況發生摟!

```javascript=
var greet = 'Hello!';
var greet = 'Hola!';

var english = {};
var spanish = {};

english.greet = 'Hello!';
spanish.greet = 'Hola!';
```

### 範例二

命名空稱使用的{ }物件可以做很多層:

把greet包裹在greeting裡面

```javascript=
var greet = 'Hello!';
var english = {};

english.greeting = {};
english.greeting.greet = 'Hello!';

console.log(english);
```

![](https://i.imgur.com/xHDptD5.png)


也可以使用物件實字:

```javascript=
var greet = 'Hello!';
var english = {
    greeting:{
        greet:"Hello!"
    }
};

console.log(english);
```

![](https://i.imgur.com/MNGbIRI.png)


# JSON以及物件實字(JSON And Object Literals)


* JSON (JavaScript Object Notation)
* 跟物件的型態非常相似
* 有數個方法可以使用來轉換JSON

一般物件型態:

```javascript=
var objectLiteral = {
    firstname: 'Mary',
    isAProgrammer: true
};
```

JSON型態:
```json=
{
    "firstname": "Mary",
    "isAProgrammer": true
}
```

轉換物件成JSON格式可以使用`JSON.stringify()`

```javascript=
JSON.stringify(objectLiteral);
```

轉換JSON為物件給JS使用`JSON.parse()`

```javascript=
var jsonValue = JSON.parse('{ "firstname": "Mary", "isAProgrammer": true }');
```

# 函式就是物件(Function Are Objects)

## First Class Functions

* 你可以對函式做對於其他類型(字串、數字、物件、布林值等)都可以做的事情
* 可以指派函式為變數
* 可以把函式當成參數給其他函式使用
* 可以在literal syntax中使用函式


![](https://i.imgur.com/Uc94cSq.png)

函式是一種特殊的物件，但正因為它是物件所以他可以使用純值、物件、函式

以及兩種特殊的屬性 
1. name(非必須，有匿名函式)
2. code也就是使用者撰寫的程式碼並且它是可以被呼叫的"Invocable"()


## 範例

能成功地給函式加上屬性代表函式真的是一種物件

```javascript=
function greet() {
    console.log("h1");
}

greet.language = 'English';

console.log(greet.language);
```

1. 設置一個函式greet，內容為印出hi
1. 給函式加上屬性
1. 印出greet.language

得出結果 正是加上去的屬性
![](https://i.imgur.com/31dfkx9.png)

## "Invocable"()

![](https://i.imgur.com/eyOntey.png)

* 當創造這個greet 函式時，它會被放到記憶體裡(以目前的例子會放到全域物件裡)
* 函式會有個名字屬性 greet
* 函式會有code屬性也就是 `console.log("h1");`
* 然而當呼叫greet()這邊使用括弧來呼叫函式

## 作者非常強調
> JS的函式就是物件




# 函式陳述式、函式表達式(Function Statements And Function Expressions)

## 表達式(Expression)

* 它不必須存在變數之中
* 一段會創造值(value)的程式碼

### 表達式範例

* (=),(+)運算子都會回傳結果，因此他們兩個都是表達式

`var a;`

![](https://i.imgur.com/QWDWw1J.png)

* 只要有回傳值就是表達式(下方回傳物件)

![](https://i.imgur.com/Nwn6KsN.png)


## 陳述式(statement)

判斷式if 就是個很好的例子

* 不會返回值
* 無法把if判斷式指派給變數

```javascript=
if(a ===3){

}
```

## 函式陳述式範例

* 一開始就會被寫進記憶體中
* 具有Hoisting特性

```javascript=
function greet() {
    console.log('h1');
}
```

這段函式它不會回傳值因為它沒有被呼叫，所以它就是個函式陳述式，只代表它被放置於記憶體中，也就代表著**Hositing**

因此我們可以這樣使用:

1. 先呼叫函式
1. 撰寫函式本體
1. 依舊可以印出結果

```javascript=

greet();

function greet() {
    console.log('h1');
}
```

## 函式表達式範例

* 一開始不會被寫進記憶體
* 執行時建立這個函數物件使用指向該函數記憶體的變數進行呼叫(也就是指派給變數做呼叫)
* 匿名函式的部分就是函式表達式
 
![](https://i.imgur.com/T0hnU0W.png)


注意: 這邊可以發現匿名函式的部分就是函式表達式，因為它會產生值

1. 創造匿名函式
1. 把函式指派給變數 anonymousGreet
1. 使用"()"  anonymousGreet()
1. 就可以呼叫此匿名函式瞜

#關於匿名函式的部分，其實可以命名，但是基於程式碼簡潔的關係以及其實函式位置已經綁訂於變數所以命名這部分是比較多餘的

## 函式表達式無法做Hoisting

* 因為變數的預設值為undefined
* 要到變數被執行了才會知道它的值，所以只會先顯示undefined那當然不是個函式


```javascript=
anonymousGreet();

var anonymousGreet = function () {
    console.log('h1 ');
}
```

![](https://i.imgur.com/OtTr7EZ.png)


## 把函式作為參數丟進另一個函式


```javascript=
function log(a) {
    a();
}

log(function () {
    console.log('h1');
});
```

* 把函式做完參數傳送
* 這樣的寫法其實就是下方範例，也就是[First Class Functions](#First-Class-Functions)的概念

```javascript=
var a = function () {
    console.log('h1');
}

a();
```

# Conceptual Aside

## By Value vs By reference

* 這邊主要談論的都是指變數
* reference 像是記憶體中的地址
* value 代表變數的值

### By Value

> 讓兩個變數有相同的value藉由複製value的方式但是有兩個不同的reference

* 所有純值都是傳值(By value)

1. 設置 a = 純值(數字、字串)
1. 這時候純值會有個reference就像是它的地址讓變數a可以找到它
1. 讓 新的變數b b = a 
1. 這時候b就會複製純值的value到不一樣的地址b

![](https://i.imgur.com/pPMboQa.png)

### By Value 範例

```javascript=
// by value(primitives)
var a = 3;
var b;

b = a;

a = 2;
console.log(a);
console.log(b);
```
印出結果
![](https://i.imgur.com/piUJv9Y.png)


因為by value只會複製值不會複製reference所以，b還是保持在新的地址，a的變化跟b無關

### Mutate

改變某樣東西

* Immutable 代表無法被改變


### By reference

> 讓兩個物件有相同的物件藉由給予同樣的reference並不是複製同樣的內容

* 所有的物件都是傳址(by reference)
* 不管是處理把他們(物件)設置相等或是傳入函式

1. 設置 a = 純值(數字、字串)
1. 這時候純值會有個reference就像是它的地址讓變數a可以找到它
1. 讓 新的變數b b = a 
1. 這時候b會藉由原本 a 的reference找到其value

![](https://i.imgur.com/JMYnTYu.png)

### By reference 範例

```javascript=

// by reference(all objects(including function))

var c = {
    greeting: 'hi'
};
var d;

d = c;
c.greeting = 'hello';

console.log(c);
console.log(d);
```

印出結果:
![](https://i.imgur.com/1ixoIdP.png)


因為By reference 傳遞的是地址，所以兩個物件c d 基本上是在一樣的地址一樣的內容，修改其一另一個一樣也被修改

### By reference(even as parameters) 範例


```javascript=
function changeGreeting(obj) {
    obj.greeting = 'Hola';
}

changeGreeting(d);

console.log(c);
console.log(d);
```
印出結果:
![](https://i.imgur.com/VjO4C4H.png)


把物件使用參數做傳遞，一樣是傳址，因此兩個傳遞對象是一樣的地址，修改一個其他都會修改


### By reference 使用(=)指派 範例(特例)


```javascript=
c = {
    greeting: 'Howdy'
}

console.log(c);
console.log(d);
```

印出結果:
![](https://i.imgur.com/2Mbfcfb.png)

* 這邊可以看到不是說reference是傳址，所以兩方物件應該會一樣?
* 但是(=)運算子可以設定新的記憶體地址給c因此c,d印出來的結果不同了


# 物件、函式以及'this'(Objects, Functions, And 'this')


![](https://i.imgur.com/RIdUSQV.png)

* 函式就是物件: 其中有兩個特殊屬性 code, name
* 當函式被呼叫時(也就是code的部分)，會創造出執行背景(Execution Context)，接著會被擺入執行堆(Execution stack)，這會決定這個函式會如何被執行
* 當執行背景被創造出來時，內部都會有variable Environment也就是變數被創造在函式內部
* 也會有Outer Environment也就是當在函式內部找不到變數使用時，會往外部尋找參考一直找到全域變數為止(再來也沒了)
* 但我們也知道每天JS引擎創造執行背景時都會創造'this'這個變數，甚至我們不需要輸入任何內容
* 而這個this會指向(代表)不同的物件取決於這個函式是如何被呼叫

## 'this'的指向

### 範例一

```javascript=
function a() {
    console.log(this);
    this.newvariable = 'hello';
}

var b = function () {
    console.log(this);
}

a();
console.log(newvariable);
b();
```

這邊設置了三種情況

1. 一定有的golbal object
2. 函式陳述式
3. 函式表達式

結果印出來:

全部都指向window這個global object
並且可以直接給global object加上屬性都沒問題

![](https://i.imgur.com/DlKoeZ0.png)


* 當值是純值的時候被稱為property
* 當值是函式的時候被稱為method

### 範例二(例外)

這邊把this使用在物件內部的函式也就是methods

```javascript=
var c = {
    name: 'The c object',
    log: function () {
        console.log(this);
    }
}

c.log();
```
印出結果:
![](https://i.imgur.com/q1ClvKP.png)

竟然是指向了object

並且可以這樣使用

```javascript=
var c = {
    name: 'The c object',
    log: function () {
        this.name = "I can change name"
        console.log(this);
    }
}

c.log();
```
印出結果:
![](https://i.imgur.com/rBANwZ9.png)

竟然可以通過this的指向來操作物件的內容key的部分

### 範例三(類似bug)

於是我們找到一個類似於JS引擎比較類似缺點的地方:

透過函式表達式的方式使用變數傳遞函式在物件內部的methods內，並且使用this再次改寫一次name屬性，這邊理論上應該會使"I can change name"修改成'change name again'

```javascript=
var c = {
    name: 'The c object',
    log: function () {
        this.name = "I can change name"
        console.log(this);

        var setname = function (newname) {
            this.name = newname;
        }
        setname('change name again');
        console.log(this);
    }
}

c.log();
```
印出結果:

沒有任何變化
剛剛以為透過物件內部的methods內部的this會指向物件本身，但是這邊的this卻指向別的地方

![](https://i.imgur.com/p3yMbyc.png)


打開window全域物件查看發現，這邊的this竟然指向的位置是全域物件window
![](https://i.imgur.com/S0rUjDo.png)


### 範例四(範例三的解答)

如何避免這樣的情況發生呢?

把this的位置好好綁訂好並且把每個地方的this都使用變數確認是使用同一個this指向同一個地方就可以解決這個問題摟!

```javascript=
var c = {
    name: 'The c object',
    log: function () {
        var self = this;

        self.name = "I can change name"
        console.log(self);

        var setname = function (newname) {
            self.name = newname;
        }
        setname('change name again');
        console.log(self);
    }
}

c.log();
```

印出結果:

這次的this就正常的指向物件本身因此可以修改name屬性搂!

![](https://i.imgur.com/Xq4GGwA.png)


# Conceptual Aside

## Arrays Collection of Anything


創造一個array
`var arr = new Array();`

使用array literal syntax
`var arr = [];`

JS的array是以0為基底的:

`console.log(arr[0])`

可以印出array第一個元素