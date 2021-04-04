---
title: JS-OOP Crash Course (ES5 & ES6)
date:
tags: Javascript
category: Javascript
---


# JavaScript OOP Crash Course (ES5 & ES6)

---
tags: Javascript relate
---

###### tags: `Javascript`

我們先來解釋一下"**物件**"(object)


基本上就是一個**物品**，車子、人、房子等等。


其實"**物件**"就是用程式碼在電腦裡表達出： "這是個物品"，這樣的概念。


## 物件的構成:

* 屬性(property) 這就好比車子的廠牌 大小 人的姓名年齡等等各種資訊
* 方法(method) 就像是物件的運行方式，車子的發動、煞車，人的吃飯睡覺行走等等

用一個"物件"來形容人，上方的資料是這個人的屬性，下方的function是方法
![](https://i.imgur.com/WvnsOYh.png)


## 基本結構語法(basic literal)


下方的程式碼解釋了應用屬性(property)的用法以及產生新的object的用法

```javascript=
const s1 = 'helloaaa';
console.log(typeof (s1));
console.log(s1.toUpperCase());

// 這邊的 s 用typeof出來會顯示字串不是物件卻可以像object一樣使用屬性

const s2 = new String('hello');
console.log(typeof (s2));

//不過同時也可以直接把string這個屬性直接賦予他變成物件
```

window是所有的物件的父母層所以基本上在撰寫的時候可以省略

```javascript=
console.log(window);

window.alert(1);

alert(1);//同樣可以執行跟上方一樣的結果
```

下方的內容是一個object (.)後面接一個 property

```javascript=
console.log(navigator.appVersion);

```

----


下方我們舉些例子說明:


```javascript=
const book1 = {
    title: 'Bool one',
    author: "John Doe",
    year: '2013',
};

console.log(book1);

//結果如下
/* 

{title: "Bool one", author: "John Doe", year: "2013"}
author: "John Doe"
title: "Bool one"
year: "2013"
__proto__: Object 

*/

```
如果我們想要取得object裡面的key可以使用`Object.keys`:

```javascript=
console.log(Object.keys(book2));

// 這邊會印出這個object的property像是["title", "author", "year", "getSUmmary"]

```

如果我們想要取得object裡面的值可以使用`Object.values`:

```javascript=
console.log(Object.values(book2));

//會印出含有book2 values 的 array
```

如果我們想要使用其中的屬性(property)假設我們想要使用title:

```javascript=
console.log(book1.title);

// 會印出結果  Book one
```

## 物件實字 (Object Literals)

物件實字的語法重點：

* 會用大括號表示。
* 裡面的屬性 (Properties) 用名值對 (name-value pairs) 表示。ex.(title: 'Book one',)
* 多個屬性以逗號 (comma) 分隔。
* 宣告完後，還是可以再增加 Properties 進去。

```javascript=
const book1 = {
    title: 'Book one',
    author: "John Doe",
    year: '2013',
    getSUmmary: function () {
        return `${.title} was written by 
        ${this.author} in ${this.year}`;
    }
};

console.log(book1.getSUmmary());
```


## 建構子(constructor)

用來建構很大量內容的時候可以使用就不用重複寫很多地方可以建構起來重複使用

上方的function就是建構子的部分，下面是實體化(Instatiate)建構子使用物件，所以它會印出上方建構子的內容:

![](https://i.imgur.com/o2xs5CY.png)


```javascript=
// Constructor

function Book() {
    console.log('Book Initialized..')
}


// Instatiate an Object
const book1 = new Book();
const book2 = new Book();

console.log(book1.title);
//這邊一樣可以使用這個來取的它的title "Book One"
```

如果我們直接輸入:
會得到
![](https://i.imgur.com/hqtZbmQ.png)

![](https://i.imgur.com/kzLJ5sL.png)

就不需要再重複寫一次Book的內容以及它的function因為已經建構在上面了

```javascript=
console.log(book1);
```

```javascript=
console.log(book2.getSUmmary());
```

這個部分在上面建構子裡面寫入function這樣之後只要使用`console.log(book2.getSUmmary());`就可以呼叫了不需要重複寫入

```javascript=

function Book(title, author, year) {
    this.title = title;
    this.author = author;
    this.year = year;

    this.getSUmmary = function () {
        return `${this.title} was written by 
        ${this.author} in ${this.year}`;
    }
}
```

## 原型(Prototypes)

另一種建構方法(methods)的方式是使用`prototype`

把它額外拉出來做prototype這樣一樣可以用剛剛一樣的方式取得一樣的效果`console.log(book2.getSUmmary());`

```javascript=
//getSummary
Book.prototype.getSUmmary = function () {
    return `${this.title} was written by 
        ${this.author} in ${this.year}`;
}
```
這個時候我們在印出book2會發現function已經沒有在裡面了，而是會存在下方prototype裡面，會這樣做的原因是有些時候方法(method)不一定每個物件都要使用就可以這樣把他拉出來需要得再去取用它就好

![](https://i.imgur.com/Dioa6SV.png)

下個範例使用了兩個元素來表達想要獲取得書本歲數

* new Date()取的現在時間
* getFullYear()取得現在年分

```javascript=
//getAge
Book.prototype.getAge = function () {
    const years = new Date().getFullYear() - this.year;
    return `${this.title} is ${years} years old`;
}
```

下方會解釋如何操作內容的資料

我們想要修改裡面的時間，所以設定一個新的年分並且下方設定reviesed為true

```javascript=
//Revise / Change Year
Book.prototype.revise = function (newYear) {
    this.year = newYear;
    this.revised = true;
}
```

```javascript=
console.log(book2);
book2.revise('2018');
console.log(book2);
```

可以得出這個結果

![](https://i.imgur.com/BOhPzJ9.png)


## 繼承(Inheritance)

下方提到繼承這個特性:

創造一個Magazine來繼承Book的屬性之外還可以添加屬性使用`call`這個方法來達成

```javascript=
// Magazine Constructor

function Magazine(title, author, year, month) {
    Book.call(this, title, author, year);

    this.month = month;
}

//Instantiate Magazine Object

const mag1 = new Magazine('Mag One', 'John Doe', '2018', 'Jan');

console.log(mag1);
```
### Prototype methods Inheritance

prototype的方法卻不能直接繼承所以使用`create`這個屬性讓Magazine也可以繼承prototype**所有**的方法

```javascript=
Magazine.prototype = Object.create(Book.prototype);
```

因為Magazine是繼承上面Book的屬性所以在constructor的部分還是會顯示Book

![](https://i.imgur.com/nDROuBV.png)


如果想要修改的話可以使用constructor這個使用來修改:

```javascript=
// Use Magazine as Constructor instead of Book

Magazine.prototype.constructor = Magazine;
```

![](https://i.imgur.com/tmWKXpa.png)


## 創造(Object_create)

一開始使用一個const包住兩個方法，接下來使用`create`來創建新的物件來包含這兩個方法並且下方用新增的方式來把title,author,year加進去新的object book1裡面

```javascript=
//Object Of Protos

const bookProtos = {
    getSummary: function () {
        return `${this.title} was written by 
        ${this.author} in ${this.year}`;
    },

    getAge: function () {
        const years = new Date().getFullYear() - this.year;
        return `${this.title} is ${years} years old`;
    }
};

//Create Object

const book1 = Object.create(bookProtos);
book1.title = 'Book One';
book1.author = 'John Doe';
book1.year = '2013';

console.log(book1);
```

![](https://i.imgur.com/jzu1G7R.png)

下面這個寫法跟上面出來的結果是一樣的只是換個方式寫

```javascript=
const book1 = Object.create(bookProtos, {
    title: {value: 'Book One'},
    author: {value: 'John Doe'},
    year: {value: '2013'},
});


console.log(book1);
```


----------

## ES6的東西開始

### class

用法跟上面的建構子很像在做一樣的事情，也一樣需要建構物件以及實體化物件

```javascript=
class Book {
    constructor(title, author, year) {
        this.title = title;
        this.author = author;
        this.year = year;
    }
}

//Instantiate Object
const book1 = new Book('Book One', 'John Doe', '2013');

console.log(book1);
```

接下來放入方法進去跟前面的寫法差不多，引用跟使用的方式也差不多

```javascript=
class Book {
    constructor(title, author, year) {
        this.title = title;
        this.author = author;
        this.year = year;
    }
    getSummary() {
        return `${this.title} was written by 
        ${this.author} in ${this.year}`;
    }

    getAge() {
        const years = new Date().getFullYear() - this.year;
        return `${this.title} is ${years} years old`;
    }
    revise(newYear) {
        this.year = newYear;
        this.revised = true;
    }
}

//Instantiate Object
const book1 = new Book('Book One', 'John Doe', '2013');

console.log(book1);
book1.revise('2018');
```
輸出的結果如下:

![](https://i.imgur.com/78nS8BQ.png)


### 靜態語法(static)

會寫在class裡面，它的特性是不會被已經實體化的物件呼叫比方說，而是被類別本身(class)直接呼叫

```javascript=
static topBookStore() {
        return 'Barnes & Nobles'
    }
    //這邊就是實體化的部分所以book1無法呼叫static方法
    const book1 = new Book('Book One', 'John Doe', '2013');
    
    //可以這樣子直接使用
    console.log(Book.topBookStore());
```

### Subclasses

這邊很類似上面繼承的概念只是更新語法更簡潔

使用到`extend`來繼承Book的物件，然後一樣使用建構子`constructor`寫入所有的物件內容，之後使用`super`繼承物件內容，最後放入要新增的內容即可

```javascript=
class Book {
    constructor(title, author, year) {
        this.title = title;
        this.author = author;
        this.year = year;
    }
    getSummary() {
        return `${this.title} was written by 
        ${this.author} in ${this.year}`;
    }
}

//Magazine Subclass

class Magazine extends Book {
    constructor(title, author, year, month) {
        super(title, author, year);
        this.month = month;
    }
}

//Instantiate Magazine

const mag1 = new Magazine('Mag One', 'John Doe', '2018', 'Jan');

console.log(mag1.getSummary());
```