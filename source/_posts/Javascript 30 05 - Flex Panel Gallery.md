---
title: 實作練習-Javascript 30 05 - Flex Panel Gallery
date:
tags: [HTML, CSS, Flex, JavaScript]
category: Javascript作品
---

# Javascript 30 05 - Flex Panel Gallery

---

## tags: Javascript relate

###### tags: `Javascript`

跟著做 JS 30 第四個作品 FLEX 排版/CSS class 切換/transition 動畫事件的處理

![](https://i.imgur.com/Nj77C3V.png)

[跟著做出來的範例](https://chiehLiu.github.io/git-projects/05%20-%20Flex%20Panel%20Gallery/index-START.html)

## 想法示意

- 運用 CSS flex 做各種置中排版
- 點擊每個格子，會整體視窗放大，然後跳出文字出現的動畫

### HTML:

```htmlembedded=
<div class="panels">
    <div class="panel panel1">
      <p>Hey</p>
      <p>Let's</p>
      <p>Dance</p>
    </div>
    <div class="panel panel2">
      <p>Give</p>
      <p>Take</p>
      <p>Receive</p>
    </div>
    <div class="panel panel3">
      <p>Experience</p>
      <p>It</p>
      <p>Today</p>
    </div>
    <div class="panel panel4">
      <p>Give</p>
      <p>All</p>
      <p>You can</p>
    </div>
    <div class="panel panel5">
      <p>Life</p>
      <p>In</p>
      <p>Motion</p>
    </div>
  </div>
```

## CSS:

這個部分主要會針對數個地方直接使用 flex 去做排版以及置中

```css=
.panel {
      //這邊是把最外面的五個大視窗做flex並且做同樣的一等分
      flex: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      background: #6B0F9C;
      .
      .以下省略
      .
      .
```

比較重要的地方並且搭配 JS 做使用的是這個部分

- "open" 是點擊視窗後文字以及視窗都放大的效果
- "\*" 這個部分是觸發之前的`<p>`的狀態:往螢幕上下移動
- "open-active" 是觸發後`<p>`的狀態:回到原位

```css=
.panel>*:first-child {
     transform: translateY(-100%);
   }

   .panel.open-active>*:first-child {
     transform: translateY(0);
   }

   .panel>*:last-child {
     transform: translateY(100%);
   }

   .panel.open-active>*:last-child {
     transform: translateY(0);
   }

   .panel p:nth-child(2) {
     font-size: 4em;
   }

   .panel.open {
     font-size: 40px;
     flex: 3;
     /* 手風琴張開特效配上 .panel 裡面的transition可以很方便做到 */

   }
```

## JS:

一開始會先製作比較簡單的點擊後放大視窗以及文字:

1. 直接使用`querySeletorAll`抓取`.panel`作為變數`panels`的值
2. 對`panel`做事件監聽使用"click"點擊後觸發後方函式`clickHandler`
3. 撰寫`clickHandler`函式，會開或關 open 這個 class，這時點擊視窗以及文字就會放大了
4. 接下來處理文字特效，對`panel`增加一個事件"transitionend"來關閉 transform 特效並且使用函式 transitionendHandler
5. 撰寫 transitionendHandler 函式，因為要先找出影響動畫的 propertyName 可以先 console.log(e)看一下得出是 flex-grow 這個屬性，所以使用判斷式如果是包含 flex 的 propertyName 的話則開或關 open-active 這個 class

### 小補充:

- Safari transitionend event.propertyName === flex
- Chrome + FF transitionend event.propertyName === flex-grow
- querySelectorAll 選取後得到的是一個 NodeList 他不具陣列的所有功能所以使用 forEach

```javascript=
<script>
    ;
    (function () {
      const panels = document.querySelectorAll('.panel');
      //抓出來的東西不是陣列所以只能用forEach

      function clickHandler() {
        this.classList.toggle("open");
      }

      function transitionHandler(e) {
        console.log(e);
        if (e.propertyName.indexOf('flex') !== -1) {
          this.classList.toggle('open-active');
        }
      }

      panels.forEach(panel => {
        panel.addEventListener("click", `clickHandler
clickHandler
clickHandler`);
        panel.addEventListener("transitionend", transitionHandler);
      })

    })()
  </script>
```
