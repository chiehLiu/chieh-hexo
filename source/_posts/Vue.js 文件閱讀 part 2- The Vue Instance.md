---
title: Vue-文件閱讀 part 2- The Vue Instance(5000字)
date:
tags: Vue
category: Vue2
---


#  Vue.js 文件閱讀 part 2- The Vue Instance

---
tags: Javascript relate
---

###### tags: `Javascript, Vue.js`

# 創造Vue實體 (Creating a Vue Instance)

* 所有的Vue app 都會從創造實例(Instance)開始
* 裡面的options處就是我們操作的地方，可以瀏覽[ API reference](https://vuejs.org/v2/api/#Options-Data)來做操作


```javascript=
var vm = new Vue({
  // options
})
```


* 一個Vue app通常會有會有個root Vue instance由new Vue產生
* 伴隨著的是巢狀的樹組成的component，它具有可重複使用的特性
* 在ROOT下面的都是component的部分

```javascript=
Root Instance
└─ TodoList
   ├─ TodoItem 
   │  ├─ TodoButtonDelete
   │  └─ TodoButtonEdit
   └─ TodoListFooter
      ├─ TodosButtonClear
      └─ TodoListStatistics
```

## 範例

index.js
```javascript=
var app = new Vue({
    el:#app,
    data: {
    product: "Socks"

})

```

index.html
```htmlembedded=
<div id="app">
    <h2>{{ product }} </h2>
</div>    

```

* app使用el連接到html檔案內部的id = "app"的div
* 連結app內的data: poduct到html上{{product}}
* 藉由改變index.js 內 product的內容可以及時修改html內的{{product}}的內容


呈現在網頁上的結果
![](https://i.imgur.com/Q0nZBMD.png)


藉著改變屬性也可以及時修改頁面內容

```javascript=
app.product = 'Coat'
//印出結果變成Coat

app.product = "Compass"
//印出結果變成Compass
```

![](https://i.imgur.com/ZtJ5TBm.png)


![](https://i.imgur.com/tvzMv4N.png)


# 資料與方法(Data and Methods)

## $data

```htmlembedded=
<div id="app">{{msg}}</div>
```

```javascript=
let data = {
            msg: '123123'
        }

let vm = new Vue({
            el: '#app',
            data,
        });
```

這兩個是相同的結果

```javascript=
vm.$data === data   //true

data.msg === vm.msg  //true
```

因此當我們操作

```javascript=
data.msg =456
vm.msg = 123
```

畫面也會如此響應

但是如果使用不存在的屬性時畫面則不會響，得使用不同的方法

```javascript=
vm.b = 'hi'
```

但是如果你知道可能稍後會有屬性會使用到，但目前得空著或是還未存在，因此就必須設預設值

比方說要規畫一個todoList app可能會使用到的data:

```javascript=
data: {
  newTodoText: '',
  visitCount: 0,
  hideCompletedTodos: false,
  todos: [],
  error: null
}
```

## Object.freeze()

可以關閉reative，讓畫面不被響應



```htmlembedded=
<div id="app">{{msg}}</div>
```

```javascript=
let data = {
            msg: 'hello Vue'
        }

Object.freeze(data);

let vm = new Vue({
            el: '#app',
            data,
        });
```

在這個情況下

```javascript=
data.msg =456
vm.msg = 123
```

畫面也不會有任何響應

並vm也會變成只能讀不能寫
![](https://i.imgur.com/IBZOEP4.png)


## $前綴API
$這個符號代表Vue提供給我們的功能
如
$data,
$el,
$watch等等

[Instance Properties](https://vuejs.org/v2/api/#Instance-Properties)



# 生命週期裝置實例(Instance Lifecycle Hooks)

到特定的時間就會呼叫特定的函式

每個Vue實體都會經歷一連串的初始化階段舉例:

1. 需要設置好data observation
1. 編譯模板
1. 把Vue實體推到DOM上
1. 更新DOM當data被更新

在這個階段過程中也會跑一些functions被稱為**Lifecycle Hooks**，讓使用者寫自己的程式碼在特定的階段使用

## 範例

當Vue實體已經被創造時，created這個函式可以被使用:

```javascript=
new Vue({
  data: {
    a: 1
  },
  created: function () {
    // `this` points to the vm instance
    console.log('a is: ' + this.a)
  }
})
// => "a is: 1"
```

![](https://i.imgur.com/kCZ5wYN.png)


在不同的階段還有其他的hooks會被呼叫例如:

所有的hook指向調用它的實體

* mounted
* updated
* destroyed

## 作者提醒

千萬不要使用箭頭函式在Vue實體，因為箭頭函示沒有this常常會導致報錯

```
Uncaught TypeError: Cannot read property of undefined 
Uncaught TypeError: this.myMethod is not a function
```


使用一般的函式:

```javascript=
new Vue({
            data: {
                a: 1
            },
            created: function () {
                console.log(this)
            }
        })
```
才能印出 Vu實體
![](https://i.imgur.com/utK0icf.png)



使用箭頭函式:

```javascript=
new Vue({
            data: {
                a: 1
            },
            created: () => {
                console.log(this)
            }
        })
```

只會印出外層的windows
![](https://i.imgur.com/yZu3ut0.png)


## Lifecycle Diagram

從上方那張圖可以得知hook如下:


**beforeCreate**
Vue實體初始化後立刻呼叫此函式，不過此時Vue實體還未創建所以其中的設定都還未能使用(如data observation, event, watcher setup)

**created**
Vue實例創建完成後立刻呼叫此函式，已設置 data, computed properties, methods, watch/event callbacks，但尚未開始mounting階段，且 $el 還不能在此階段使用。


**beforeMount**
在mounting階段開始前被調用：render function首次被調用。

mounted
選項物件中的el被新創建的vm.$el替換，並掛載到到 vm 上，並調用mounted這個鉤子。

beforeUpdate
數據被更新時會調用，發生在 Virtual DOM re-render 和 patch 之前(連結：Day4: Virtual DOM)，可以在此時更改狀態數據，並不會增加重新渲染的成本。

updated
由於數據更新導致 Virtual DOM re-render 和 patch 之後會調用updated這個鉤子。

不精確白話文為：由於updated被調用時，DOM 已經更新。所以在此時更新數據很可能會導致updated無限循環的被調用。

beforeDestroy
在 Vue Instance 被銷毀前被調用，因此 Vue Instance 在beforeDestroy中仍可運作。

不精確白話文為：Vue Instance 可以在此時做垂死前的掙扎。

destroyed
在 Vue Instance 被銷毀後被調用，此時 Vue Instance 所有東西會解除綁定，事件監聽也都會被移除，子實例也會被銷毀。


# 模板語法(Template Syntax)

