---
title: Vue-文件閱讀 part 1- Introduction + Installation(5000字)
date:
tags: Vue
category: Vue2
---



#  Vue.js 文件閱讀 part 1- Introduction + Installation

---
tags: Javascript relate
---

###### tags: `Javascript, Vue.js`


# 簡介(Introduction)

## Vue.js是什麼?

* 一個用來搭建使用者介面的框架
> 框架(Framework)：由包含各種功能與開發規則的函數庫組成。我們可以利用其提供的功能加速開發，不必從零開始；而其開發規則通常是經過驗證的良好開發方法，只要follow它，就可以避免很多問題與錯誤。因此框架通常有著加速開發並易於維護的特性。
* 在MVVM的架構下以視圖(view layer)為核心的網頁介面(Web UI)開發方法
* 容易上手並且容易整合進其他的資料庫或是其他的現存的專案
* 可以完美的強化單頁應用程式是(SPA)藉著一些[現代工具](https://vuejs.org/v2/guide/single-file-components.html)以及[輔助使用的資料庫](https://github.com/vuejs/awesome-vue#components--libraries)

[影片學習 - Intro to Vue 2](https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/)

<script async src="//jsfiddle.net/chiehLiu/80nLrhmp/embed/"></script>



# 安裝使用(Getting Started)

> 這份官方手冊需要有HTML, CSS, and JavaScript基本知識必較容易讀懂
> 有其他框架使用經驗也有幫助

## 相容性指示(Compatibility Note)

* Vue不支援IE8甚至更低的版本
* 因為Vue使用ECMAScript 5 features但IE8不支援

![](https://i.imgur.com/TWcuTRw.png)


## 語意化的版本控制

簡單來說就讓版本名稱具有意義好辨識並且達成共識，避免相容性出現問題

[語意化版本](https://semver.org/lang/zh-TW/)


## 最新版本釋出

[最新版本 Github](https://github.com/vuejs/vue/releases)


## Vue 開發工具(Vue Devtools)

相當推薦使用在一個使用者友善介面下，可以更好的檢視你的作品以及幫忙debug

[Vue Devtools Github](https://github.com/vuejs/vue-devtools#vue-devtools)


## 使用`<script>`引入使用Vue

建議開發的時候引入Development Version才不會省略掉一些常見的錯誤訊息

![](https://i.imgur.com/Wsi9NjJ.png)


## 內容傳遞網路 (CDN - Content delivery network)

作為原型或是學習使用
```htmlembedded=
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.js"></script>
```

要用在產品身上則推薦使用特定的版本，因為最新版本可能尚未完善
```htmlembedded=
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.12"></script>
```

使用原生ES Module相容的版本

```htmlembedded=
<script type="module">
  import Vue from 'https://cdn.jsdelivr.net/npm/vue@2.6.12/dist/vue.esm.browser.js'
</script>
```

可以從此處瀏覽原始碼

[NPM package 原始碼](https://cdn.jsdelivr.net/npm/vue/)


[unpkg](https://unpkg.com/vue@2.6.12/dist/vue.js)

[cdnjs (最新版本有可能會比較慢登上這邊)](https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.12/vue.js)

### 小提醒

在你要發布的網站上面可以使用`vue.min.js`取代`vue.j`可以優化檔案大小以及執行速度


## NPM

當要使用在大型規模的app時推薦使用NPM，因為可以跟[Webpack](https://webpack.js.org/) or [Browserify](http://browserify.org/)相容的很好，


```
# latest stable
$ npm install vue
```

## CLI

使用官方CLI需要一些node.js的相關知識

[Vue CLI 官網](https://cli.vuejs.org/)

[CLI 影片教學](https://www.vuemastery.com/courses/real-world-vue-js/vue-cli/)









## Explanation of Different Builds

在[NPM package 原始碼](https://cdn.jsdelivr.net/npm/vue/) dist/處有很多不同的builds下方是他們的不同之處:


<table>
<thead>
<tr>
<th></th>
<th>UMD</th>
<th>CommonJS</th>
<th>ES Module (for bundlers)</th>
<th>ES Module (for browsers)</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Full</strong></td>
<td>vue.js</td>
<td>vue.common.js</td>
<td>vue.esm.js</td>
<td>vue.esm.browser.js</td>
</tr>
<tr>
<td><strong>Runtime-only</strong></td>
<td>vue.runtime.js</td>
<td>vue.runtime.common.js</td>
<td>vue.runtime.esm.js</td>
<td>-</td>
</tr>
<tr>
<td><strong>Full (production)</strong></td>
<td>vue.min.js</td>
<td>-</td>
<td>-</td>
<td>vue.esm.browser.min.js</td>
</tr>
<tr>
<td><strong>Runtime-only (production)</strong></td>
<td>vue.runtime.min.js</td>
<td>-</td>
<td>-</td>
<td>-</td>
</tr>
</tbody>
</table>


### 名詞解釋(Term)

* Full: 包含Compiler, Runtime

* Compiler: 負責編譯模板字版進去JS呈現相關的函式
* Runtime: 負責Vue instances, 呈現以及修補 virtual DOM(基本上處理Compiler以下的事情)
* UMD: UMD相關的builds可以直接使用在瀏覽器下藉著`<script>`tag
UMD (Universal Module Definition)，就是一種javascript通用模塊定義規範，讓你的模塊能在javascript所有運行環境中發揮作用。
* CommonJS: 給browserify or webpack使用
* ES Module: 
2.6Vue版本後才開始提供下面兩種builds
1. ESM for bundlers: 給webpack 2 or Rollup使用
1. ESM for browsers (2.6+ only): 直接引入現代的瀏覽器使用`<script type="module">`




# 宣告式渲染(Declarative Rendering)


> Vue.js的核心藉著好理解的模板語法讓使用者把資料呈現到DOM上面

## 範例

index.html
```htmlembedded=
<div id="app">
  {{ message }}
</div>

<script src="index.js"></script>
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

index.js
```javascript=
var app = new Vue({
  el: '#app', // 抓取哪邊的DOM
  data: {
    message: 'Hello Vue!' // 此處是要呈現的內容
  }
}
// 輸出 Hello Vue!

app.message = 'I have changed the data!'
// 輸出 I have changed the data
```


[影片說明Hello Vue!](https://scrimba.com/scrim/cQ3QVcr?pl=pXKqta)


* 資料以及DOM已經做了連結並且是隨時反應的
ex. app.message修改內容後輸出內容也會即時更改
* 不需要再跟HTML互動，直接在Vue instance就可以操作DOM

## 範例二

index.html
```htmlembedded=
<div id="app-2">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </span>
</div>
```

index.js
```javascript=
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date().toLocaleString()
  }
})
```

![](https://i.imgur.com/ItiTipU.gif)

當hover的時候在當前的string會顯示 字串+載入日期時間


* `v-bind`

這個有v前墜屬性被稱做指示(directive)，是Vue提供使用的，而這個v-bind的用法在於讓這個title的屬性隨著message屬性作同步修在Vue instance上面


所以當我使用下面的方法時，title的屬性也會及時更新
```javascript=
app2.message = 'some new message'
```

# 條件式以及迴圈(Conditionals and Loops)


## 條件式

index.html
```htmlembedded=
<div id="app-3">
  <span v-if="seen">Now you see me</span>
</div>
```

index.js
```javascript=
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

* `v-if`

可以理解成 v-if後方的文字必須為true(然而是否為true則要去看js程式碼如何操作)，才會讓span內的文字被看見

![](https://i.imgur.com/SjH0Sk5.png)   


因此當判斷式內容改成flase時，就看不見文字
```javascript=
app-3.seen = false;
```

## 迴圈



index.html
```htmlembedded=
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
index.js
```javascript=
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
```

* `v-for`

可以用來製作清單類型的呈現

![](https://i.imgur.com/AimG2bx.png)


如果想要再加入新的清單可以這樣做
```javascript=
app4.todos.push({ text: 'New item' })
```


# 處理使用者的輸入(Handling User Input)

## 範例

index.html
```htmlembedded=
<div id="app">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```

index.js
```javascript=
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```

* `v-on:click`

跟使用者互動藉由v-on 指示來連接事件監聽click並觸發函式來處理

點擊按鈕後把文字順序反過來

![](https://i.imgur.com/ETYNgvk.png)

![](https://i.imgur.com/pEqBa79.png)


# 建構組件(Composing with Components)

為了建構大型專案藉著拆分成不同的小組件的優點

* 可重複利用
* 是獨立的組件
* 容量小

![](https://i.imgur.com/tbekM4J.png)

## 範例

index.js
```javascript=
// 定義一個新的組件 todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})

var app = new Vue(...)
```

index.html
```htmlembedded=
<div id="app">
    <ol>
        <todo-item></todo-item>
        <todo-item></todo-item>
    </ol>
</div>
```

首先在js先撰寫組件todo-item後就可以在html裡面直接使用

## 範例二

index.js
```javascript=
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```

index.html
```htmlembedded=
<div id="app-7">
  <ol>
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```

* 首先於component處新增`porp`是一個可以客製化的屬性並命名todo
* 介下來使用`v-bind`讓文字可以被動態的傳入DOM同時傳入key的部分會在後面章節作解釋
* 並且使用`v-for`製作清單列表

![](https://i.imgur.com/OmEZP4f.png)


---

在大型專案中把內部的app做拆分是必要的，讓開發過程容易管理，下面程式碼是個範例說明比較多組件且複雜的html長相

```htmlembedded=
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```


# 與自定義元素的關係(Relation to Custom Elements)

* Vue的組件非常類似於[Custom Elements](https://developers.google.com/web/fundamentals/web-components)

* 舉例說明
Vue組件執行[Slot API](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/slot) 以及 [is](https://v3.vuejs.org/api/special-attributes.html#is) 特殊屬性

> Slot是存在web component内部的占位符，用户可以通過slot屬性在web component的内部插入自定義的標記文本。

* 不同之處
1. Web Components規範已經完成通過但是依舊沒有被所有瀏覽器支援
(目前 Safari 10.1+、Chrome 54+ 和 Firefox 63+ 原生支持 Web Components)
2. Vue 组件不需要任何 polyfill，並且支援所有瀏覽器 (IE9以下不支援)，必要時Vue组件也可以包裝於原生自定義元素之内

> polyfill代指為舊瀏覽器實現或模擬現有版本已實現之功能的程式碼片段

3. Vue 组件提供了Custom Elements沒有的功能，跨组件數據流、自定義事件溝通以及bulid整合工具。


* Vue 並沒有使用Custom Elements，不過在應用以及發布Custom Elements上還是有很好的[互通性](https://custom-elements-everywhere.com/#vue)，Vue CLI 也支持 Vue 组件建構成為原生的Custom Elements