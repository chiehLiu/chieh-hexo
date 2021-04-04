---
title: Vue-Vue2 Tutorial
date:
tags: Vue
category: Vue2
---


#  Vue JS 2 Tutorial

---
tags: Javascript relate
---

###### tags: `Javascript, Vue.js`



# Introduction

## What is Vue.js

* 前端框架
* 可以創造以JS引擎為主的網頁APP
* 在瀏覽器中使用
* 不需要為了重整頁面，跑伺服器端

## Why Vue.js

* 非常輕量
* 高執行期表現

## Installation

建議把script放在body tag內

[CDN 連結](https://vuejs.org/v2/guide/installation.html)

![](https://i.imgur.com/sIy07l3.png)


## Before You Start

前置知識:

JavaScript
HTML(&CSS)


# Vue Instance

Vue實體做的事情:

1. 控制整個app功能或是部分元件的功能
2. 儲存不同的功能在option裡面像是data, methods
3. 控制template並呈現在DOM上


我們使用在html上面的tag並不會直接被使用，而是Vue.js會創造一個template並且是JS的格式並連接我們想要呈現的data並且結果會以html程式碼的方式呈現最後呈現到HTML DOM上面


## 範例

```javascript=

// 這個部分就是Vue實體

new Vue({
    el: '#vue-app',
    data: {
        name: 'Shaun',
    }
});
```

```htmlembedded=
<body>

<div id="vue-app">
        <h1>{{name}}</h1>
</div>

</body>
```

印出結果:
![](https://i.imgur.com/Bk8iiR0.png)


# Data & Methods



```javascript=
new Vue({
    el: '#vue-app',
    data: {
        name: 'Shaun',
        job: 'Ninja'
    },
    methods: {
        greet: function (time) {
            return 'Good' + time + ' ' + this.name;
        }
    }
});
```

```htmlembedded=
<div id="vue-app">
        <h1>{{greet(' afternoon')}}</h1>
        <p>name: {{name}}</p>
        <p>job: {{job}}</p>
</div>
```

## data

data的操作不需要做`this.data.name`

而是可以直接取得name或是job

`this.name`
`this.job`


## Methods

1. 可以在內部定義函式，並且return 的內容可以包含data
1. 使用this取得Vue實體後並操作返回的內容
2. 呼叫的方式`<h1>{{greet()}}</h1>`並可以在內部輸入參數


* 需要注意的點

位於Vue實體外面的大括號是無法操作的要注意！


# Data Binding

## v-bind

把資料綁定上特定的html tag讓其可以讀取Vue實體內部的改動


新增一個website的data內容
```javascript=
new Vue({
    el: '#vue-app',
    data: {
        name: 'Shaun',
        job: 'Ninja',
        website: 'http://www.google.com'
    },
    methods: {
        greet: function (time) {
            return 'Good' + time + ' ' + this.name;
        }
    }
});
```

* 如果要綁定tag的屬性的話則必須使用v-bind:並且在要使用的data要使用雙引號包裹住
* 也可以使用縮寫 :href 這樣使用也可以喔
```htmlembedded=
<div id="vue-app">
        <h1>Data Binding</h1>
        <a v-bind:href="website">Google</a>
</div>
```

就可以綁訂在a tag上面的屬性搂!(但不只是href可以綁定其他屬性也可以)
![](https://i.imgur.com/KbyOIf1.png)


* 這邊示範綁訂在input的value屬性上面並且呈現出data裡面的name的值呈現在DOM上

```htmlembedded=
<div id="vue-app">
        <h1>Data Binding</h1>
        <a v-bind:href="website">Google</a>
        <input type="text" v-bind:value="name">
</div>
```

印出結果會把Shaun 放在value的位置
![](https://i.imgur.com/LqFofet.png)


## v-html

如果想要綁定完整的html tag上去DOM上面可以使用

```javascript=
<div id="vue-app">
        <p v-html="websiteTag"></p>
</div>
```


```javascript=
new Vue({
    el: '#vue-app',
    data: {
        websiteTag: '<a href= "http://www.google.com">GOOGLEWEBSITE</a>'
    }
});
```

印出結果就會讓a tag 出現在 p tag內部

![](https://i.imgur.com/jMKsNA5.png)
![](https://i.imgur.com/Kp9dzFX.png)


# Events

## v-on:click

使用v-on可以綁定事件，範例處我們使用click當範例:
* 當點擊add按鈕，年齡會加一
* 當點擊substract按鈕，年齡會減一

```htmlembedded=
<div id="vue-app">
        <h1>Events</h1>
        <button v-on:click="add">Add a Year</button>
        <button v-on:click="substract">Subtract a Year</button>
        <p>My age is {{age}}</p>
</div>
```


```javascript=
new Vue({
    el: '#vue-app',
    data: {
        age: 25,
    },
    methods: {
        add: function () {
            this.age++;
        },
        substract: function () {
            this.age--;
        }
    }
});
```

![](https://i.imgur.com/ypn2jza.gif)


### 作者提醒

* 要特別注意寫在當v-on在呼叫函式的時候，add()，不需要加上括號!!(但要使用參數時，一樣可以使用括號)
* 但是使用在tempalte內部的test()則要使用括號


## v-on:dblclick

* 雙擊按鈕會年齡加10/減10

這邊不需要再加入新的方法，因此我們修改方法內容加入以參數的方式讓年齡依我們想要的年份更動

```javascript=
<div id="vue-app">
        <h1>Events</h1>
        <button v-on:click="add(1)">Add a Year</button>
        <button v-on:click="substract(1)">Subtract a Year</button>
        <button v-on:dblclick="add(10)">Add a Year</button>
        <button v-on:dblclick="substract(10)">Subtract a Year</button>
        <p>My age is {{age}}</p>
</div>
```

```java=
new Vue({
    el: '#vue-app',
    data: {
        age: 25,
    },
    methods: {
        add: function (inc) {
            this.age += inc;
        },
        substract: function (dec) {
            this.age -= dec;
        }
    }
});
```

## v-on:mousemove

* 可以使用mouse相關的event屬性
* 這邊的範例使用offsetX,Y用來取的框內的座標

```htmlembedded=
<div id="vue-app" v-on:mousemove="updateXY">{{x}},{{y}}
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        x: 0,
        y: 0
    },
    methods: {
        updateXY: function (event) {
            this.x = event.offsetX;
            this.y = event.offsetY;
        }
    }
});
```

當`console.log(event)`可以看到所以mouse相關的屬性可以使用
![](https://i.imgur.com/3lB9wVQ.png)

輸出滑鼠所在位置座標
![](https://i.imgur.com/pSFM4R2.png)


# Event Modifiers

[官方文件參考](https://vuejs.org/v2/guide/events.html#Event-Modifiers)

![](https://i.imgur.com/X1A1HL1.png)


## once

* 讓這邊的點擊事件只能觸發一次

```javascript=
<div id="vue-app">
        <h1>Events</h1>
        <button v-on:click.once="add(1)">Add a Year</button>
        <p>My age is:{{age}}</p>
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        age: 25
    },
    methods: {
        add: function (inc) {
            this.age += inc;
        }
    }
});
```

點擊按鈕上升到26後就不會再觸發事件
![](https://i.imgur.com/V7lvcr6.png)

## prevent

* 避免預設行為發動

```htmlembedded=
<div id="vue-app">
        <h1>Events</h1>
        <button v-on:click.once="add(1)">Add a Year</button>
        <p>My age is:{{age}}</p>
        <a v-on:click="click" href="https://google.com">google</a>
</div>
```


```javascript=
new Vue({
    el: '#vue-app',
    data: {
        age: 25
    },
    methods: {
        add: function (inc) {
            this.age += inc;
        },
        click: function () {
            alert("It's been clicked!");
        }
    }
});
```

* 當使用click點擊事件在a tag內部觸發順序如下:

1. 觸發click事件，警告跳出It's been clicked!
2. a tag的預設行為，事件網頁跳轉會發生

* 所以想要避免預設行為的發生可以使用prevent，頁面就不會跳轉到外部頁面搂!

```htmlembedded=
<a v-on:click.prevent="click" href="https://google.com">google</a>
```


# Keyboard Events

[官方文件參考](https://vuejs.org/v2/guide/events.html#Key-Codes)

![](https://i.imgur.com/kreSfXZ.png)

## keyup

* 當input被輸入鍵盤值時觸發事件內部的函式

```htmlembedded=
<div id="vue-app">
        <h1>Keyboard Events</h1>
        <label>Name:</label>
        <input type="text" v-on:keyup="logName">
        <label>Age:</label>
        <input type="text" v-on:keyup="logAge">
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {},
    methods: {
        logName: function () {
            console.log("you entered your name");
        },
        logAge: function () {
            console.log("you entered your age");
        }
    }
});
```

印出結果
![](https://i.imgur.com/ZCV1Jou.png)


## enter

當不需要每次輸入鍵盤值都觸發函式，可以使用enter，只有輸入鍵盤值enter時才會觸發函式

```htmlembedded=
<div id="vue-app">
        <h1>Keyboard Events</h1>
        <label>Name:</label>
        <input type="text" v-on:keyup.enter="logName">
        <label>Age:</label>
        <input type="text" v-on:keyup.enter="logAge">
</div>
```

必須輸入鍵盤值enter才會有觸發函式，甚至當input為空只輸入鍵盤值enter也會觸發函式
![](https://i.imgur.com/vfPwOpa.png)


## alt

使用方法跟enter一樣，但是需要搭配enter使用，必須按住alt + enter才會觸發函式

```htmlembedded=
<input type="text" v-on:keyup.alt.enter="logName">
```


# Two-Way Data Binding

## v-model

使用此directive可以把input的內容輸入到:
1. data內部對應的name,age
2. 呈現到DOM上

```htmlembedded=
<div id="vue-app">
        <h1>Keyboard Events</h1>
        <label>Name:</label>
        <input type="text" v-model="name">
        <span>{{name}}</span>
        <label>Age:</label>
        <input type="text" v-model="age">
        <span>{{age}}</span>
</div>
```


```javascript=
new Vue({
    el: '#vue-app',
    data: {
        name: '',
        age: ''
    },
    methods: {
        logName: function () {
            console.log("you entered your name");
        },
        logAge: function () {
            console.log("you entered your age");
        }
    }
});
```

輸出結果
![](https://i.imgur.com/u2zjwvm.gif)


# Computed Properties

* 可以辨識正在使用的函式(methods無法斷判)
* 只會跑當下需要跑的資料
* 大多數時候比使用methods更有效率

## 範例

![](https://i.imgur.com/OOwnMA3.png)

想要連動，當按下按鈕Add a A時，數字會連動變化
A - 1
Age + A = 21

```htmlembedded=
<div id="vue-app">
        <h1>Computed Properties</h1>
        <button v-on:click="a++">Add a A</button>
        <button v-on:click="b++">Add a B</button>
        <p>A - {{a}}</p>
        <p>B - {{b}}</p>
        <p>Age + A = {{addToA()}}</p>
        <p>Age + B = {{addToB()}}</p>
</div>
```
這邊使用methods呈現

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        age: 20,
        a: 0,
        b: 0
    },
    methods: {
        addToA: function () {
            console.log("addToA");
            return this.a + this.age;
        },
        addToB: function () {
            console.log("addToB");
            return this.b + this.age;
        },
    }
});
```

但這時候會發現，雖然我只按了按鈕A卻兩個函式都觸發了

![](https://i.imgur.com/Ngq3nB7.png)



因此我們可以使用computed這個property，把函式包起來，這樣一來Vue.js就會辨識正在使用的函式是哪一個瞜!


```javascript=
new Vue({
    el: '#vue-app',
    data: {
        age: 20,
        a: 0,
        b: 0
    },
    computed: {
        addToA: function () {
            console.log("addToA");
            return this.a + this.age;
        },
        addToB: function () {
            console.log("addToB");
            return this.b + this.age;
        }
    },
});
```


![](https://i.imgur.com/6ubsAsj.png)



# Dynamic CSS Classes


## v-bind:class(簡易介紹版)

為了動態的處理CSS class

`v-bind:class="{class名稱 : data內部資料也就是ture/false}"`

這邊範例使用點擊事件:

1. 當點擊div時會加上class avaliable
1. 再次點擊div時會移除class avaliable
 
```htmlembedded=
<div id="vue-app">
        <h1>Dynamic CSS</h1>
        <h2>Example 1</h2>
        <div v-on:click="avaliable = !avaliable" v-bind:class="{avaliable:avaliable}">
            <span>Ryu</span>
        </div>
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        avaliable: true,
    }
});
```

簡單的CSS

```css=
span {
    background: red;
    display: inline-block;
    padding: 10px;
    color: #fff;
    margin: 10px 0;
}

.avaliable span {
    background: green;
}

.nearby span:after {
    content: "nearby";
    margin-left: 10px;
}
```

這樣使用就可以開關class搂!

![](https://i.imgur.com/bFbGv6H.gif)


## v-bind:class(真實使用版)

為了避免寫死在html內的template，真實專案中使用的方式會是能夠在JS檔案中做靈活修改的:

* 使用呼叫函式的方式`<div v-bind:class="compClasses">`
* 並在JS程式碼中輸入在computed內部
* compClasses 會返回class所需要的內容，需要修改的話也在這邊執行
* 不需要寫死在html內的templat搂!

```htmlembedded=
<div id="vue-app">
        <h1>Dynamic CSS</h1>
        <h2>Example 2</h2>
        <button v-on:click="nearby = !nearby">Toggle nearby</button>
        <button v-on:click="avaliable = !avaliable">Toggle avaliable</button>
        <div v-bind:class="compClasses">
            <span>Ryu</span>
        </div>
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        avaliable: false,
        nearby: false,
    },
    computed: {
        compClasses: function () {
            return {
                avaliable: this.avaliable,
                nearby: this.nearby
            }
        }
    }
});
```

簡易CSS

```css=
span {
    background: red;
    display: inline-block;
    padding: 10px;
    color: #fff;
    margin: 10px 0;
}

.avaliable span {
    background: green;
}

.nearby span:after {
    content: "nearby";
    margin-left: 10px;
}
```

印出結果
![](https://i.imgur.com/YACJVvA.gif)


# Conditionals

## v-if

當`v-if="內容"`，內容處布林值為true時會顯示內容，false則否

使用`v-on:click="error = !error"`達到開關的效果

```htmlembedded=
<div id="vue-app">
        <h1>Conditionals</h1>
        <button v-on:click="error = !error">Toggle Error</button>
        <button v-on:click="sucess = !sucess">Toggle Sucess</button>
        <p v-if="error">There has been an error</p>
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        error: false,
        sucess: false
    }
});
```

印出結果，當點擊按鈕時下方p tag內文字會出現
![](https://i.imgur.com/1L73zlW.png)

## v-else-if

```htmlembedded=
<p v-if="error">There has been an error</p>
<p v-else-if="sucess">There has been an sucess</p>
```

當出現v-if以及v-else-if時，只要v-if的狀態是true，那麼就不會顯示else-if的部分跟JS的判斷式一樣

## v-show 

做的事情跟v-if幾乎一樣但是差別在於:

當內容布林值顯示為false時

* v-if
會把元素完全移除掉

![](https://i.imgur.com/DPGj6Ut.png)


* v-show
只會呈現display:none

![](https://i.imgur.com/3WNQH7C.png)

# Looping with v-for

## 陣列

逐一印出data內容，範例以ul表單為例:

`v-for="chracter in characters"`

* 這個部分的chracter可以名稱自訂
* characters這個部分就需要對照data內部


```htmlembedded=
<div id="vue-app">
        <h1>Looping through lists</h1>
        <ul>
            <li v-for="chracter in characters">{{chracter}}</li>
        </ul>
</div>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        characters: ['Mario', 'Luigi', 'Yoshi', 'Bowser']
```
印出結果
![](https://i.imgur.com/NmkvMCC.png)

## 物件

可以使用 (.)的方式去取得物件的屬性

```htmlembedded=
<ul>
    <li v-for="ninja in ninjas">
                {{ninja.name}} - {{ninja.age}}
    </li>
</ul>
```

```javascript=
new Vue({
    el: '#vue-app',
    data: {
        ninjas: [{
                name: 'Ryu',
                age: 25
            },
            {
                name: 'Yoshi',
                age: 35
            },
            {
                name: 'Ken',
                age: 55
            }
        ]
    }
});
```

印出結果
![](https://i.imgur.com/y6FfHFH.png)


## 輸出index

把index嵌入template中即可

使用在陣列或是物件的`v-for`都是可行的

```
(chracter, index) in characters
(ninja, index) in ninjas
```


```htmlembedded=
<ul>
    <li v-for="(chracter, index) in characters">{{index}} . {{chracter}}</li>
</ul>
<ul>
    <li v-for="(ninja, index) in ninjas">
                {{index}} . {{ninja.name}} - {{ninja.age}}
    </li>
</ul>
```

印出結果
![](https://i.imgur.com/4g2N7Zv.png)


## 使用li以外的容器包裹住v-for的內容

### 用div包裹住h3,p

使用div一樣可以做出li一樣的效果

```htmlembedded=
<div v-for="(ninja, index) in ninjas">
            <h3>{{index}}. {{ninja.name}}</h3>
            <p>{{ninja.age}}</p>
</div>
```

印出結果
![](https://i.imgur.com/IGhcAv5.png)


### 如果只想要內容物的h3,p tag

可以改用template tag就不會輸出到DOM上面，而只有包在裡面的內容會被輸出

```htmlembedded=
<template v-for="(ninja, index) in ninjas">
            <h3>{{index}}. {{ninja.name}}</h3>
            <p>{{ninja.age}}</p>
</template>
```

印出結果
![](https://i.imgur.com/RMsiKQL.png)


## 直接印出key,value而不用透過(.)

1. 第一次的v-for就正常發揮
1. 第二次的v-for則是印出每一個ninja的key,value
1. 把第二次的結果呈現在DOM上

```htmlembedded=
<template v-for="ninja in ninjas">
            <div v-for="(val,key) in ninja">
                <p>{{key}} - {{val}}</p>
            </div>
</template>
```
印出結果所有的 key-value pair
![](https://i.imgur.com/Mzus47P.png)


# Simple Punchbag Game

