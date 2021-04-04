---
title: Vue-Crash Course 2021
date:
tags: Vue3
category: Vue3
---

#  Vue JS Crash Course 2021

---
tags: Javascript relate
---

###### tags: `Javascript, Vue.js`

# 簡介

## What is Vue?


* 是一個前端JS框架主要為了建構USER以及網頁頁面
* 常常使用在SPA(single-page-application)在客戶端使用
* 可以使用在全端的app藉著HTTP requests 送到後端
* 可以跑在伺服器端使用SSR框架像是Nuxt(非常類似於Next 之於 React)


## Why use Vue?

* 創造動態的前端 app&網頁
* 有比較簡單的學習曲線(比較像是結構化的JS)
* 容易跟其他專案做整合
* 快速且檔案較小
* Virtual DOM(只會更新頁面上需要更新的部分而不是整頁重整)
* 非常受歡迎且在崛起中
* 擁有良好的社群資源

## What should you know first?

* JS基礎
* Async Programming(promises)
* Array Methods(forEach, map, filter,etc)
* Fetch API/ HTTP Requests
* NPM(Node Package Manger)


## UI Components

![](https://i.imgur.com/69RLxhm.png)

這個作品是本課程最後會完成的UI部分:

* 橘色部分是: header
* 連接著藍色部分是: button

它們都是可以重複使用的，可以使用prop呈現文字或是顏色

* 綠色部分是: 新增任務的區域也就是form的區域
* 紅色部分是: 任務呈現區
* 紅色內部的水藍色也都是組件: 包含每一個任務
* 紫色部分: 連接到about page
 
## Basic Layout of Component

### template

你的輸出以及HTML的位置  
變數或是表達式使用宣告式渲染 

![](https://i.imgur.com/HQ7Cerg.png)


### JS part 

邏輯呈現
此處可以宣告props、特定的資料並且連到到相應的組件
也可以使用function
也可以連接到cycle methods

![](https://i.imgur.com/VYRh2uC.png)


### style

這邊的範例使用了scope

代表內部的修飾只會出現在這一個header，其他header都不會支援到

![](https://i.imgur.com/GIyEYiP.png)


### 嵌入Component

傳入props的方法就像是html裡面的屬性方式很像

也就是導入script部分的title，那個title就會使用在template裡面的`<h1>`裡

![](https://i.imgur.com/pe8XJeO.png)


## Working with State/ Data

* 組件會擁有自己的狀態(state)，這將會決定組件本身的行為以及甚麼樣的資料會被呈現
* 有一些狀態(state)會在本地端發生，然而會有一些發生在global以及app端此時他們會分享複數的組件
* 如果你有很多的app等級的狀態時可以使用VueX是狀態管理模式(像是Redux 之於 React)


## Option API vs. Composition API

* Vue3擁有composition API目標在於讓code更易讀且可以重複使用尤其在大型app專案下
* 這篇筆記不會包含compositoin API的介紹只要會專注使用傳統的option API(也就是使用在Vue2,3都有)


## Vue CLI

* Vue.js的基本工具
* 是CLI的介面來操作vue apps
* 擁有Dev server
* 擁有自己的圖形化使用者介面(GUI)
* 整合testing, TypeScript, ESLint & more

# Let's Learn Vue JS!

## 使用Vue CDN

[Vue 官網 嵌入CDN](https://v3.vuejs.org/guide/installation.html#vue-devtools)

這個指令`@next`可以嵌入最新版本的Vue.js

```htmlembedded=
<script src="https://unpkg.com/vue@next"></script>
```

引入HTML的位置跟方式

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Random User Generator</title>
  </head>
  <body>
    <div id="app"></div>

    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
</html>
```

## 範例

index.html
```htmlembedded=
<body>
    <div id="app"></div>
    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
```

app.js
```javascript=
const app = Vue.createApp({
    template: '<h1> Hello World! </h1>'
});

app.mount('#app');
```

印出結果
![](https://i.imgur.com/lLbSCcp.png)


* 在HTML的幾乎只要設定好id後就不用動作
* 主要處理在JS
* 使用Vue.createApp 內處理template`'<h1> Hello World! </h1>'`
* 使用mount選取('#app)並且把template的內容鑲嵌進去HTML裡面


## 範例二

index.html
```htmlembedded=
<body>
    <div id="app"></div>
    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
```

app.js
```javascript=
const app = Vue.createApp({
    template: '<h1> Hello {{firstName}} </h1>',
    data() {
        return {
            firstName: 'John'
        }
    }
})

app.mount('#app');
```

印出結果
![](https://i.imgur.com/vvovy0W.png)


* 讓文字可以動態呈現使用`{{}}`雙大括號
* 並且內部包裹住data()函式return的物件名稱firstName(特別注意data是函式)
* 最後使用mount推上HTML


## 範例三

index.html
```htmlembedded=
<body>
    <div id="app">
        <h1> Hello {{firstName}} </h1>
    </div>
    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
```

app.js
```javascript=
const app = Vue.createApp({
    data() {
        return {
            firstName: 'John'
        }
    },
})

app.mount('#app');
```

印出結果
![](https://i.imgur.com/vvovy0W.png)


* 把template移動到html內會有一樣的效果

### 移動template到`<div>app`外面

則沒有任何效果只會是純字串

index.html
```htmlembedded=
<body>
    <div id="app">
        <h1> Hello {{firstName}} </h1>
    </div>
    <h1> Hello {{firstName}} </h1>
    
    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
```
印出結果
![](https://i.imgur.com/9JosyV4.png)

# 製作一個 user 製造器

## 成品:

![](https://i.imgur.com/wxZUUip.gif)


[成品網址]()

## 成品功能:

1. 點擊get random user後會出現隨機的人
2. 包括 全名 大頭貼 email
3. 男女使用的邊框顏色會切換(男生藍色、女生粉紅)


## HTML


## html程式碼:

```htmlembedded=
<body>
    <div id="app">
      <img
        :class="gender"
        v-bind:src="picture"
        :alt="`${firstName} ${lastName}`"
      />
      <h1>{{firstName}}{{lastName}}</h1>
      <h3>Email:{{email}}</h3>
      <button v-on:click="getUser()" :class="gender">Get random User</button>
    </div>

    <script src="https://unpkg.com/vue@3.0.5"></script>
    <script src="app.js"></script>
  </body>
```

## CSS:

在本篇不是重點不過有興趣可以參照以下網址

[CSS part](https://codepen.io/bradtraversy/pen/LYbzJjK)

## JS:

* `<template>`
1. 主要使用在整體頁面的動態文字呈現h1,h3的部分

* `v-bind`
1. 可以在HTML上面做縮寫 冒號後面接上要動態顯示的內容 (ex. :class，需要動態顯示class名稱 )
1. 使用在動態屬性的呈現上面 `<img>`的屬性以及`<button>`的屬性

* `v-on`
監聽點擊事件，當點擊時觸發getUser函式

* `getUser()`

* 使用非同步函式取得`fetch('https://randomuser.me/api/')`後
* 解構取得的results : {results} 並且取用內部資料去填入`data()`return的結果呈現在HTML上
![](https://i.imgur.com/nnWxdK9.png)

* 藉由取得gender的動態文字來修改邊框顏色

![](https://i.imgur.com/Ap1zcaE.png)

![](https://i.imgur.com/5BYKvej.png)

![](https://i.imgur.com/3yxQti2.png)

## JS完整程式碼:
```javascript=
const app = Vue.createApp({
    data() {
        return {
            firstName: 'John',
            lastName: 'Doe',
            email: 'john@gmail.com',
            gender: 'male',
            picture: 'https://randomuser.me/api/portraits/men/10.jpg',
        }
    },
    methods: {
        async getUser() {
            const res = await fetch('https://randomuser.me/api/')
            const {
                results
            } = await res.json()
            console.log(results);
            this.firstName = results[0].name.first,
                this.lastName = results[0].name.last,
                this.email = results[0].email,
                this.gender = results[0].gender
            this.picture = results[0].picture.large
        },
    },
})

app.mount('#app');
```

# Vue CLI


## Installation

終端機輸入

```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
```

確認是否安裝成功
```
vue --version
```

更新內容

```
npm update -g @vue/cli

# OR
yarn global upgrade --latest @vue/cli
```

## 使用 GUI

### 方法一

```
vue ui
```

會開啟app 即可使用但沒辦法自定義一些細節
![](https://i.imgur.com/5fKIQ4G.png)


### 方法二


```
vue create 名稱自訂(這邊我輸入vue-crash-2021)
```

會出現一些問題需要回答:

這邊作者選擇Maunally select features
![](https://i.imgur.com/jW0ghVg.png)

可以視專案需求做選擇
![](https://i.imgur.com/vVCw2Mk.png)

下一步選擇vue.js的版本
![](https://i.imgur.com/YFRho9t.png)

下一步選擇 In dedicated config files
![](https://i.imgur.com/xb3SfHX.png)

下一步會詢問是否儲存設定建議選擇N 畢竟每次專案設定不同看需求而定


接下來我們進入資料夾 cd vue-crash-2021會發現需要的資料都已經載入

![](https://i.imgur.com/hyCcMPd.png)

下一步使用
```
npm run serve
```
![](https://i.imgur.com/eXlTVHv.png)

就可以成功叫出來瞜!
![](https://i.imgur.com/fnsycfI.png)

---

#### 方法二內容物介紹

index.html

* 就是剛剛看到個landing page
* 並且紅框處app的功能都會呈現在裡面

![](https://i.imgur.com/y7rBHbP.png)


main.js

* 這邊是匯集程式碼的地方
* 會有import在裡面
* 會有App來源的位置
* 並且把App的內容呈現到DOM上

![](https://i.imgur.com/9zGMsqS.png)



App.vue

這個部分就跟上面簡介處介紹的一樣[Basic-Layout-of-Component](#Basic-Layout-of-Component)

```javascript=
<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```
# 作者推薦

setting 修改讓emmet能在vue使用
![](https://i.imgur.com/BcFcHQx.png)

安裝highlight 套件 才不會程式碼都沒有顏色區別
![](https://i.imgur.com/DIJOz4g.png)



# 製作一個 任務追蹤器

## 成品:




[成品網址]()

## 成品功能:



## HTML



## html程式碼:

```htmlembedded=

```


## CSS:

## CSS完整程式碼

```css=

```

## JS:


## 變數設置


## functions:


## JS完整程式碼:
```javascript=

```