---
title: JS 幼幼班 - jQuery 篇
date:
tags: jQuery
mathjax: true
---

# JS 幼幼班 - jQuery 篇

---

## tags: Javascript relate

###### tags: `Javascript, jQery`

# jQuery 簡介

## 01 為何還要繼續使用 jQuery 呢?

1.台灣還是有高市佔率
![](https://i.imgur.com/h05To2m.png)

2.支援套件仍然是最多

3.從 jQuery 了解 JS 在瀏覽器能做些什麼

- DOM 操作
- 事件觸發 (滑鼠點擊、鍵盤點擊)
- 表單送出

### JQuery 就是把 JS 的內容"擷取"其精華，讓 JS 變得更具體更好操作

jQuery 的寫法
![](https://i.imgur.com/qfAiSTZ.png)

JS 的寫法
![](https://i.imgur.com/e19NOf4.png)

很明顯可以比較出 jQuery 的寫法是比較精簡好讀的

## 02 如何使用 jQuery 並實現第一個範例

步驟一到官網下載檔案
[jQuery 官網](https://jquery.com/)

![](https://i.imgur.com/doCOYon.png)

步驟二創建資料夾並把剛剛下載的檔案以及要使用 jQuery 的檔案擺在一起
![](https://i.imgur.com/4taZYsp.png)

步驟三在 head 內引入 link(跟引入 CSS 很像)

```javascript=
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script src="jquery-3.5.1.js"></script>
</head>
```

步驟四撰寫小範例:

點擊按鈕修改顏色

- `$()`選擇器
- `.click` 點擊事件
- `.css` 修改 CSS

```javascript=
<body>
    <h1 id="hello world">hello world</h1>
    <button id="btnred">red</button>
    <button id="btnblue">blue</button>

    <script>
        $("#btnred").click(function () {
            $("#btnred").css('color', 'red');
        })
        $("#btnblue").click(function () {
            $("#btnblue").css('color', 'blue');
        })
    </script>
</body>
```

![](https://i.imgur.com/L1kNdgS.png)

## 03 jQuery 到底在做些什麼 ?

JS 可以在瀏覽器做的事情以及讓它更精簡且易讀

- 當 按下按鈕 => 跳出視窗
- 當 送出表單 => 跳轉頁面
- 當 上傳檔案 => 通知完成

## 04 jQuery 的三大重點

### 1. 選擇器:

`$()`

選取要觸發的元素

例如: `$("body")` 選取整個`<body>`

### 2. 事件觸發:

決定那些事件可以觸發 callback 函式

例如: `.click` 點擊觸發事件

### 3. callback 函式:

事件觸發後會執行甚麼動作

- 顯示、隱藏元素
- 改變 CSS 效果
- DOM 操作

而上面的小範例就是點擊後執行修改按鈕顏色

![](https://i.imgur.com/L1kNdgS.png)

# 第一章 選擇器

## id 選擇器

```javascript=
<body>
    <h1 id="hello world">hello world</h1>
    <button id="btnred">red</button>
    <button id="btnblue">blue</button>

    <script>
        $("#btnred").click(function () {
            $("#btnred").css('color', 'red');
        })
        $("#btnblue").click(function () {
            $("#btnblue").css('color', 'blue');
        })
    </script>
</body>
```

一樣以上面的範例舉例:

`$("#btnred")` - 抓取要操作的 id 加上#並用雙引號包起來就完成瞜!

## class 選擇器

跟 id 抓法不同會抓取一樣 class 的全部內容

`$(".btnred")` - 抓取要操作的 class 加上(.)並用雙引號包起來就完成瞜!

### 元素選擇器

一樣會選取全部的該名稱的元素

直接輸入名稱就可以抓取他們瞜

`$("p")`抓去段落`<p>`

# 第二章 事件

## 01 滑鼠事件，點擊(click) 與連續兩次點擊(dblclick)

我繼續沿用上面的範例做操作

- 點擊一次改變紅色按鈕(click)
- 點擊兩次改變藍色按鈕(dblclick)

```javascript=
<script>
        $("#btnred").click(function () {
            $("#btnred").css('color', 'red');
        })
        $("#btnblue").dblclick(function () {
            $("#btnblue").css('color', 'blue');
        })
</script>
```

印出結果:
![](https://i.imgur.com/L1kNdgS.png)

## 02 滑鼠事件，移入(mouseenter)與移出(mouseout)

- 當滑鼠移入目標觸發事件
- 當滑鼠移出目標觸發事件

```javascript=
<script>
        $("#btnred").mouseenter(function () {
            $("#btnred").css('color', 'red');
        })
        $("#btnblue").mouseout(function () {
            $("#btnblue").css('color', 'blue');
        })
</script>
```

- red 是進入觸發顏色
- blue 是出去觸發顏色
  ![](https://i.imgur.com/aMizEwl.gif)

## 03 滑鼠的 hover 事件

當取得焦點時觸發事件

```javascript=
<script>
        $("#btnred").hover(function () {
            $("#btnred").css('color', 'red');
        })
        $("#btnblue").hover(function () {
            $("#btnblue").css('color', 'blue');
        })
</script>
```

當取得焦點時觸發事件
![](https://i.imgur.com/bVL8M6l.gif)

## 04 如果遇到沒看過的滑鼠事件該怎麼辦?

[閱讀官方文件](https://api.jquery.com/)

[w3cschool](https://www.w3schools.com/jquery/)

## 05 遇到 jQuery 文件中不懂得地方該怎麼辦 ?

知道大方向在處理什麼內容
並從文件中去搜尋

## 06 on('click', ..) 與 click()是等價的

click 事件其實是個縮寫:

後面的 handler 是 callback 函式

`.on("click", handler)`

其實跟原生的 JS 的寫法很像

```javascript=
clickHandler(){
console.log(123)
}

addEventListener('click', clickHandler)
```

## 07 我們怎麼知道 DOM 是否已經就緒 ? 使用 ready()

ready()這個方法提供了我們一個方式讓我們去跑 JS 並且在網頁的 DOM 載入完全的情況下去操作

下列方法都是等價的

```
* $( handler )
* $( document ).ready( handler )
* $( "document" ).ready( handler )
* $( "img" ).ready( handler )
* $().ready( handler )
```

## 08 如何在 vscode 中快速產生 ready() code snippet

尋找這個套件
![](https://i.imgur.com/PgDTgY7.png)

使用 jq 前墜去尋找就可以找到搂!
![](https://i.imgur.com/3toG4kv.png)

# 第三章 選擇器的進階

## 選擇器的進階 Traversal 鄰居、爸爸與小孩 - 鄰居篇

使用`.siblings()`印出 id:1 以外其他同一層的鄰居

```javascript=
<body>
    <h1 id="hello world">hello world</h1>

    <p id="1">1</p>
    <p id="2">2</p>
    <p id="3">3</p>

<script>
        $('#1').siblings().css('color','red');

</script>
```

讓其他同一層的鄰居呈現紅色
h1 以及 p 都在同一階層

![](https://i.imgur.com/sShTlwU.png)

### 搭配使用

使用`first()`去找到鄰居的第一個也就是 h1

```javascript=
<script>
      $("#1").siblings().first().css("color", "red");
</script>
```

印出結果
![](https://i.imgur.com/6UhZ47W.png)

也可以搭配[]中括號使用 index 抓取內容去操作

不過要注意整段 sinbings 加上中括號的部分需要再用選擇器包裹住一次才有辦法使用

```javascript=
<script>
      $($("#1").siblings()[2]).first().css("color", "red");
</script>
```

印出 index 為 2 的物件呈現紅色
![](https://i.imgur.com/n6DvYyU.png)

## 選擇器的進階 Traversal 鄰居、爸爸與小孩 - 父母篇

尋找元素本身的上一層就是找父母的意思

使用`parent()`這個方法

```javascript=
<body>
    <div>
      <p id="1">1</p>
    </div>
    <div>
      <p id="2">2</p>
    </div>
    <div>
      <p id="3">3</p>
    </div>
    <script>
      $("#1").parent().css("background-color", "red");
    </script>
</body>
```

尋找段落 p 的 parent 也就是它外層的 div 並讓他上紅色

![](https://i.imgur.com/tvhQf2P.png)

![](https://i.imgur.com/G9ftHQM.png)

### 搭配使用

一樣可以使用`siblings()`去尋找父母的鄰居

```javascript=
<script>
      $("#1").parent().siblings().css("background-color", "red");
</script>
```

會得到這個結果

![](https://i.imgur.com/ZFk2NEP.png)

![](https://i.imgur.com/gZL8ley.png)

## 選擇器的進階 Traversal 鄰居、爸爸與小孩 - 小孩篇

去尋找子層的元素做操作

```javascript=
<body>
    <div>
      <p id="1">
        <l1>1</l1>
        <l1>1</l1>
        <l1>1</l1>
      </p>
    </div>
    <div>
      <p id="2">2</p>
    </div>
    <div>
      <p id="3">3</p>
    </div>
    <script>
      $("#1").children().css("background-color", "red");
    </script>
  </body>
```

這三個 li 就是 id:1 元素的子層
![](https://i.imgur.com/fBlSOuN.png)

印出結果
![](https://i.imgur.com/ZQabatx.png)

### 搭配使用

使用`.last()`抓取子層的最後一個元素做操作

```javascript=
<script>
      $("#1").children().last().css("background-color", "red");
</script>
```

抓取最後一個元素做操作
![](https://i.imgur.com/xMJVkez.png)

印出結果
![](https://i.imgur.com/e3112f8.png)

## chain method

如果要操作的元素外面有很多層也可以把`children()`疊很多層做操作

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="2">2</p>
    </div>
    <div>
      <p id="3">3</p>
    </div>
    <script>
      $("#divgrand")
        .children()
        .children()
        .children()
        .last()
        .css("background-color", "red");
    </script>
  </body>
```

找了三層進去並且使用 last()設定最後一個元素
![](https://i.imgur.com/3zcBPSI.png)

印出結果
![](https://i.imgur.com/B5rnI3K.png)

## parant(), parants(), parentsUntil()的差異

比較上面三者的不同

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="2">2</p>
    </div>
    <div>
      <p id="3">3</p>
    </div>
    <script>
      $("#1").parent().css("border", " 5px solid red");
    </script>
</body>
```

### `parant()`

只取其上層一個 parent

![](https://i.imgur.com/78XdUAR.png)

也就是外面的這層 divparent
![](https://i.imgur.com/pAfCSeV.png)

### `parants()`

取全部的 parent
![](https://i.imgur.com/FbdAjTU.png)

![](https://i.imgur.com/vF99WZn.png)

### `parentsUntil()`

取到哪個 parent 為止

```javascript=
<script>
      $("#1").parentsUntil("#divgrand").css("border", " 5px solid red");
</script>
```

取到 parent - divgrand 為止所以只會給他的上一層 divparent 上外框
![](https://i.imgur.com/kY1UIFW.png)

印出結果
![](https://i.imgur.com/Yos10bF.png)

## Traversal : Traversing 中的 first(), last(), find()

### `first()`

使用`first()`去找到鄰居的第一個也就是 h1

```javascript=
<script>
      $("#1").siblings().first().css("color", "red");
</script>
```

印出結果
![](https://i.imgur.com/6UhZ47W.png)

### `last()`

使用`.last()`抓取子層的最後一個元素做操作

```javascript=
<script>
      $("#1").children().last().css("background-color", "red");
</script>
```

抓取最後一個元素做操作
![](https://i.imgur.com/xMJVkez.png)

印出結果
![](https://i.imgur.com/e3112f8.png)

### `find()`

尋找特定 id 底下的元素(任何都可以 div, p, li 等等)

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="2">2</p>
    </div>
    <div>
      <p id="3">3</p>
    </div>
    <script>
      $("#divgrand").find("p").css("border", " 5px solid red");
    </script>
  </body>
```

尋找 divgrand 底下的 p 段落並且全部加上邊框

印出結果
![](https://i.imgur.com/HrNk2Py.png)

## Traversal 中的 eq(), filter() 與 not()

### eq()

可以選取指定的位置的元素

注意:ndex 得部分不一定從 0 開始 是可以自訂成從 1 或是從 0 開始

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1" class="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="1" class="1">
        <l1>a</l1>
        <l1>b</l1>
        <l1>c</l1>
      </p>
    </div>
    <div>
      <p id="1" class="1">
        <l1>A</l1>
        <l1>B</l1>
        <l1>C</l1>
      </p>
    </div>
<script>
      $(".1").eq("2").css("border", "5px solid red");
</script>
</body>
```

選取 index2 為 ABC
![](https://i.imgur.com/jxnaNhR.png)

### filter()

可以篩選內容

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1" class="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="1" class="1">
        <l1>a</l1>
        <l1>b</l1>
        <l1>c</l1>
      </p>
    </div>
    <div>
      <p id="1" class="1">
        <l1>A</l1>
        <l1>B</l1>
        <l1>C</l1>
      </p>
    </div>

    <span class="1">span</span>
    <script>
      $("span").filter(".1").css("border", "5px solid red");
    </script>
</body>
```

使用 filter 篩選 span 裡面有 id = 1 元素加上紅框框就不會抓到 div 去搂!

![](https://i.imgur.com/wglnP0T.png)

### not()

篩選"不是的"內容做操作

```javascript=
<body>
    <div id="divgrand">
      <div id="divparent">
        <p id="1" class="1">
          <l1>1</l1>
          <l1>2</l1>
          <l1>3</l1>
        </p>
      </div>
    </div>
    <div>
      <p id="1" class="2">
        <l1>a</l1>
        <l1>b</l1>
        <l1>c</l1>
      </p>
    </div>
    <div>
      <p id="1" class="1">
        <l1>A</l1>
        <l1>B</l1>
        <l1>C</l1>
      </p>
    </div>

    <span class="2">span</span>
    <script>
      $("p").not(".1").css("border", "5px solid red");
    </script>
</body>
```

這邊我做篩選段落中的 P 不是 class = 1 的會產紅框框

由上面可以理解小寫的 abc 不符合所以上色
![](https://i.imgur.com/R1lYusp.png)

# 第四章：快速理解 jQuery API (一) 特效類

## 顯示或隱藏元素 hide() 與 show()

這邊我設置點擊事件作範例

```javascript=
<body>
    <button id="show">show</button>
    <button id="hide">hide</button>

    <div>div</div>
    <div>div</div>

    <script>
      $("#hide").click(function () {
        $("div").hide();
      });

      $("#show").click(function () {
        $("div").show();
      });
    </script>
  </body>
```

show,hide 的效果
![](https://i.imgur.com/7OR5I3T.gif)

## 淡入與淡出 fadeIn() fadeOut()

這邊我設置個持續一秒效果如下:

```javascript=
<script>
      $("#hide").click(function () {
        $("div").fadeOut(1000);
      });

      $("#show").click(function () {
        $("div").fadeIn(1000);
      });
</script>
```

![](https://i.imgur.com/CgLEUwH.gif)

## 特效類 animate() 實現簡單動畫

一般不會這樣使用，會放到 CSS 裡面操作

不過使用起來長這樣:

- 設定了變長
- 設定了透明

```javascript=
<script>
      $("#hide").click(function () {
        $("div").animate({ opacity: 0.3 });
      });

      $("#show").click(function () {
        $("div").animate({ width: "400px" });
      });
</script>
```

![](https://i.imgur.com/wzj5FRd.gif)

## jQuery 中的 Callback 回調(函式)

當事件觸發後執行的函式就是回調函式

這裡的 animate 就是一種:

```javascript=
<script>
     $("#hide").click(function () {
       $("div").animate({ opacity: 0.3 });
     });

     $("#show").click(function () {
       $("div").animate({ width: "400px" });
     });
</script>
```

# 第五章：快速理解 jQuery API (二) 「取得」與「覆寫」值

## text()取得元素標籤中的文字 / 修改文字也可以的

`text()`不加內容的用法可以取得選取元素的文字內容

在這邊同時利用 alert 彈出選取元素的文字內容

```javascript=
    <button class="btnone">getstr</button>
    <button class="btntwo">getsecstr</button>

    <p class="1">123</p>
    <p class="2">123</p>
    <p class="3">123</p>
<script>
      $(".btnone").click(function () {
        var str = $(".1").text();
        alert(str);
      });
</script>
```

點擊 getstr 後跳出 class = 1 那段落的文字內容
![](https://i.imgur.com/rCpcu42.png)

### 並且可以針對選取的 class 去選擇 first, last

抓取元素第一個最後一個等等

```javascript=
<body>
    <button class="btnone">getstr</button>
    <button class="btntwo">getsecstr</button>

    <p class="1">123456</p>
    <p class="2">123</p>
    <p class="3">123</p>
    <script>
      $(".btnone").click(function () {
        var str = $("p:first").text();
        alert(str);
      });

      $("#show").click(function () {});
    </script>
  </body>
```

點擊 getstr 的印出結果
![](https://i.imgur.com/wNqYzHQ.png)

### 針對抓取的元素可以做指定

這樣選取就可以針對修飾段落 p 中的 class = 3 的部分

```javascript=
<body>
    <button class="btnone">getstr</button>
    <button class="btntwo">getsecstr</button>

    <p class="1">123456</p>
    <p class="2">123</p>
    <p class="3">12348</p>
    <script>
      $(".btnone").click(function () {
        var str = $("p.3").text();
        alert(str);
      });

      $("#show").click(function () {});
    </script>
  </body>
```

點擊 getstr 的印出結果
![](https://i.imgur.com/t3YYetM.png)

### text()，把值放進去設定會修改文字內容

如果在 text()內部填入值的話會修改文字內容

```javascript=
<body>
    <button class="btnone">getstr</button>
    <button class="btntwo">getsecstr</button>

    <p class="1">123456</p>
    <p class="2">123</p>
    <p class="3">12348</p>
    <script>
      $(".btnone").click(function () {
        $("p.3").text("hello world");
      });
    </script>
</body>
```

在這邊操作的話會是點擊後改變文字內容成()內部的文字

![](https://i.imgur.com/ZkBBG9u.png)

## html() 取得或是修改 DOM

### html()內不填入值

取得 html 內部的值:
html()內不填入值，一樣會取得元素的值

```javascript=
<body>
    <button class="btnone">change</button>
    <button class="btntwo">reverse</button>

    <p class="1">I will change</p>
    <div></div>
    <script>
      $(".btnone").click(function () {
        var str = $(".1").html();
        alert(str);
      });
    </script>
</body>
```

按下 change 後顯示這個段落 p 內部的值
![](https://i.imgur.com/3ZtIw43.png)

取得 html tag:
html()內不填入值，但是抓取 parent 的話會直接印出 children 的 html tag+內容

```javascript=
<body>
    <button class="btnone">change</button>
    <button class="btntwo">reverse</button>

    <div>
      <p id="1">I will change</p>
    </div>
    <script>
      $(".btnone").click(function () {
        var str = $("div").html();
        alert(str);
      });
    </script>
  </body>
```

點擊 change 後印出結果會包含子層的 html tag+內容
![](https://i.imgur.com/PPIeixT.png)

### html()內部填入值

會取代掉原本的內容

```javascript=
<body>
    <button class="btnone">change</button>
    <button class="btntwo">reverse</button>

    <div></div>
    <p id="1">I will change</p>

    <script>
      $(".btnone").click(function () {
        $(".btntwo").html("<p>hello world</p>");
      });
    </script>
  </body>
```

![](https://i.imgur.com/SvvmhJg.png)

點下 change 後 reverse 會轉變成 hello world
![](https://i.imgur.com/noiha7A.png)

#### 比較奇怪的情況是

如果把內容換成 div 就不會被取代而是增加一個 children 進去如下圖

```javascript=
<script>
      $(".btnone").click(function () {
        $("div").html("<p>hello world</p>");
      });
    </script>
```

點擊 change 後 hello world 加入 div 內部
![](https://i.imgur.com/VPothxj.png)

## attr() 取得或改變元素的屬性

### 取得元素的屬性

取得 href,alt 的值

```javascript=
<body>
    <button id="btn1">getHREF</button>
    <button id="btn2">getImagealt</button>

    <p><a href="http://123123123.com">123123123</a></p>
    <img src="123.jpg" alt="cloudy sky" />
    <script>
      $("#btn1").click(function () {
        var str = $("a").attr("href");
        alert(str);
      });
      $("#btn2").click(function () {
        var str = $("img").attr("alt");
        alert(str);
      });
    </script>
</body>
```

點擊 getHREF
![](https://i.imgur.com/hSXgj0A.png)

點擊 getimagealt
![](https://i.imgur.com/Ug7xGVE.png)

### 複寫值

#### 複寫單一屬性

`attr("要被複寫的屬性名稱", "改寫的內容")`

```javascript=
<body>
    <button id="btn1">getHREF</button>
    <button id="btn2">getImagealt</button>

    <p><a href="http://123123123.com">123123123</a></p>
    <img src="123.jpg" alt="cloudy sky" />
    <script>
      $("#btn2").click(function () {
        $("img").attr("alt", "123");
      });
    </script>
</body>
```

#### 一次複寫多種屬性需要加入中括號並且要修改的屬性鍵值配對

ex.(title: "jQuery")

```javascript=
<body>
    <button id="btn1">getHREF</button>
    <button id="btn2">getImagealt</button>

    <p><a href="http://123123123.com">123123123</a></p>
    <img src="123.jpg" alt="cloudy sky" />

<script>

      $("#btn2").click(function () {
        var str = $("img").attr({
          title: "jQuery",
          alt: "jQuery Logo",
        });
        alert(str);
      });
</script>
```

image 就會被複寫新的值進去(修改 alt 以及增加 title 進去)
![](https://i.imgur.com/AmoHfW7.png)

## val() 取得或修改 form 表單的值

### val()取得值

針對輸入在#name, #comment, #city 這三個區域的值並且使用 alert 把它們抓出來

![](https://i.imgur.com/BQnlJwV.png)

```javascript=
<body>
    <label for="">姓名</label>
    <input type="text" id="name" /><br />
    <label for="">comments</label>
    <input type="text" id="comment" /><br />
    <label>city</label>
    <select id="city">
      <option value="JP">JP</option>
      <option value="USA">USA</option>
      <option value="UK">UK</option>
    </select>
    <br />

    <button id="getname">getname</button>
    <button id="getcomment">getcomment</button>
    <button id="getcity">getcity</button>
    <script>
      $("#getname").click(function () {
        var name = $("#name").val();
        alert(name);
      });
      $("#getcomment").click(function () {
        var comment = $("#comment").val();
        alert(comment);
      });
      $("#getcity").click(function () {
        var city = $("#city").val();
        alert(city);
      });
    </script>
  </body>
```

輸出結果:
![](https://i.imgur.com/Fl99mpu.png)

### val()修改內容

這邊使用$("#getname").text()取得要修改的內容後指派給變數 name

在使用 val(name)直接更換裡面的內容

```javascript=
<body>
    <label for="">國家</label>
    <input type="text" id="name" /><br />

    <button id="getname">TW</button>
    <button id="getcomment">UK</button>
    <button id="getcity">USA</button>
    <script>
      $("#getname").click(function () {
        var name = $("#getname").text();
        $("#name").val(name);
      });
      $("#getcomment").click(function () {
        var name = $("#getcomment").text();
        $("#name").val(name);
      });
      $("#getcity").click(function () {
        var name = $("#getcity").text();
        $("#name").val(name);
      });
    </script>
</body>
```

點擊事件觸發修改 value

![](https://i.imgur.com/6noHN7z.gif)

# 第六章 快速理解 jQuery API (三) DOM 的操作

## append()選取元素內部最後加入內容

在所選取的元素內部的最後方加入內容

可以是純文字或是`<p><div><h1>`

範例處我做`<h1>`示範
![](https://i.imgur.com/dXMUKkz.png)

```javascript=
<body>
    <h1>append</h1>

    <div id="div">
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur,
        quasi?
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,
        voluptatem?
      </p>
    </div>

    <script>
      $("#div").append("<div>this is how append work</div>");
    </script>
</body>
```

## prepend()選取元素內部最前加入內容

在所選取的元素內部的最前方加入內容

可以是純文字或是`<p><div><h1>`

範例處我做`<h1>`示範

![](https://i.imgur.com/3atIvqO.png)

```javascript=
  <body>
    <h1>prepend</h1>

    <div id="div">
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur,
        quasi?
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,
        voluptatem?
      </p>
    </div>

    <script>
      $("#div").prepend("<h1>this is how prepend work</h1>");
    </script>
  </body>
```

## before() 選取元素同一層最前加入內容

在所選取的元素同一層(sibling)的前方加入內容

可以在圖中觀察到我加進去的 h1 跟我選取的 div 是 sibling 也就是它們是同一層的最前方
![](https://i.imgur.com/XeFnrHE.png)

```javascript=
  <body>
    <h1>before</h1>

    <div id="div">
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur,
        quasi?
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,
        voluptatem?
      </p>
    </div>

    <script>
      $("#div").before("<h1>this is how before work</h1>");
    </script>
  </body>
```

## after()選取元素同一層最後加入內容

在所選取的元素同一層(sibling)的後方加入內容

可以在圖中觀察到我加進去的 h1 跟我選取的 div 是 sibling 也就是它們是同一層的後方
![](https://i.imgur.com/ttQq8hP.png)

```javascript=
<body>
    <h1>after</h1>

    <div id="div">
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur,
        quasi?
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,
        voluptatem?
      </p>
    </div>

    <script>
      $("#div").after("<h1>this is how after work</h1>");
    </script>
  </body>
```

## empty()清空內容(留下 tag)

清空指定元素

像我這邊移除了內容，但是 div 的部分會繼續存在
![](https://i.imgur.com/YHj4NQw.gif)

```javascript=
<body>
   <h1>empety</h1>

   <div id="div">
     <p>Lorem ipsum dolor sit amet consec</p>
     <p></p>
   </div>

   <button id="btn">empty</button>
   <script>
     $("#btn").click(function () {
       $("#div").empty();
     });
   </script>
 </body>
```

## remove() 移除元素(移除 tag)

移除指定元素

像我這邊移除了 div，他會 div 連同內容全部移除
![](https://i.imgur.com/fGuqoW9.gif)

```javascript=
<body>
    <h1>after</h1>

    <div id="div">
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Consectetur,
        quasi?
      </p>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. In,
        voluptatem?
      </p>
    </div>

    <button id="btn">remove</button>
    <script>
      $("#btn").click(function () {
        $("#div").remove();
      });
    </script>
  </body>
```

## remoteAttr() 刪除元素的屬性

刪除元素的屬性

![](https://i.imgur.com/0Q04FIJ.gif)

```javascript=
<body>
    <h1>removeAttr</h1>

    <div id="div">
      <a id="a" href="http://123123.com"></a>
    </div>

    <button id="btn">removeAttr</button>
    <script>
      $("#btn").click(function () {
        $("#a").removeAttr("href");
      });
    </script>
  </body>
```

## wrap() 可以保裹住元素

影片範例中使用了 div 以及 b,em 等 tag 去包裹元素

但是可以使用 append 相關的 API 就好這個比較不常使用

![](https://i.imgur.com/H7aeaiF.png)

![](https://i.imgur.com/kELnK6C.png)
