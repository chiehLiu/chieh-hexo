---
title: 實作練習-Javascript 30 03 - Playing with CSS Variables and JS
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Javascript 30 03 - Playing with CSS Variables and JS

---

## tags: Javascript relate

###### tags: `Javascript`

跟著做 JS 30 第三個作品 調整照片:邊框大小 模糊度 邊框顏色

[跟著做出來的範例](https://chiehLiu.github.io/git-projects/03%20-%20CSS%20Variables/index-START.html)

![](https://i.imgur.com/0Ph2Ywa.png)

## 想法示意

這個練習的重點在於

- spacing 改變 padding
- blur 使用 filter 改變 blur
- base color 改變 background

這三個部分它們怎麼使用 JS 去串聯到 style 裡面做修改，甚至他們有"單位"(ex.px,rem)的情況下

## HTML:

首先可以先觀察一開始的原始檔案我就學習到一些基本的 HTML 使用:

認識 HTML <input> type Attribute

- range：滑動桿
- color：顯示顏色選擇器
- min/max: 代表最大最小值
- data-sizing:
  HTML5 中的 data-_ attribute 屬性的 _ 的部分是可以自訂的，其中的內容如果要被 JS 讀取得使用`dataset`這個物件就可以抓取瞜!

![](https://i.imgur.com/uxKEUl7.png)

本篇作品 HTML:

```javascript=
<div class="controls">
    <label for="spacing">Spacing:</label>
    <input id="spacing" type="range" name="spacing" min="10" max="200" value="10" data-sizing="px">

    <label for="blur">Blur:</label>
    <input id="blur" type="range" name="blur" min="0" max="25" value="10" data-sizing="px">

    <label for="base">Base Color</label>
    <input id="base" type="color" name="base" value="#ffc600">
  </div>
```

## CSS:

### CSS Variables

使用 CSS 變數有什麼好處呢？

- 統一整個樣式表的樣式 讓大家在原始碼中的數值統一
- 基於預定的數值做計算 因為都有了基準數值後，變數就可以整體做計算，不用一一調整

第一個步驟是宣告變數:

```css=
:root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }
```

第二個步驟是取值階段:

```css=
img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }
```

---

本篇作品 CSS:

```javascript=
    :root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }

    img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }

    .hl {
      color: var(--base);
    }



    body {
      text-align: center;
      background: #193549;
      color: white;
      font-family: 'helvetica neue', sans-serif;
      font-weight: 100;
      font-size: 50px;
    }

    .controls {
      margin-bottom: 50px;
    }

    input {
      width: 100px;
    }
```

---

## JS:

一開始必須先使用 querySelectorAll 抓取要改變的地方也就是
.controls 底下的 `<input>`HTMLtag 底下的 value

```javascript=
const inputs = document.querySelectorAll('.controls input');
```

抓去後使用 forEach 在剛剛設定的變數 inputs 上面因為做一個一個操作的時候會使用 forEach，並加入 addEventListener 做事件監聽處理"change","mousemove"讓滑鼠在點擊 slidebar 的時候會改變 CSS 的數值進而改變畫面。

兩個使用到的事件:

![](https://i.imgur.com/ukFLHgs.png)

![](https://i.imgur.com/AaIsRcf.png)

## [Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)

```javascript=
inputs.forEach(function (input) {
        input.addEventListener('change', changeHandler)
        input.addEventListener('mousemove', changeHandler)

```

接下來處理最後一件事情把抓取到的數值以及單位放入 style 裡面使用 setProperty

`style.setProperty(propertyName, value, priority);`

`dataset`這邊來選取 HTMLtag 裡面的屬性上面有提到來選取他設定的屬性或者是`''`為空

```javascript=
document.documentElement.style.setProperty('--' + this.name, this.value + (this.dataset.sizing || ''))
```

完整程式碼編排:

```javascript=
<script>
    ;(function () {
      const inputs = document.querySelectorAll('.controls input');

      function changeHandler() {

        document.documentElement.style.setProperty('--' + this.name, this.value + (this.dataset.sizing || ''))


      }
        inputs.forEach(function (input) {
        input.addEventListener('change', changeHandler)
        input.addEventListener('mousemove', changeHandler)
      })

    })()
  </script>
```

## 小補充

所有的事件都可以看這個參照~
[Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)

HTML range color

CSS 變數

dataset

setProperty 融合變數的寫法很特別

可以再多留意~
