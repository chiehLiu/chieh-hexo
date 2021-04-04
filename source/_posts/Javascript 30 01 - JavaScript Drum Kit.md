---
title: 實作練習-Javascript 30 01 - JavaScript Drum Kit
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Javascript 30 01 - JavaScript Drum Kit

---

## tags: Javascript relate

###### tags: `Javascript`

跟著做 JS 30 第一個作品 Drum kit

主要是用這個頁面呈現，搭配鍵盤上面的按鈕做出可以有聲音互動的頁面

[跟著做出來的範例](https://chiehLiu.github.io/git-projects/01%20-%20JavaScript%20Drum%20Kit/index-START.html)

![](https://i.imgur.com/vu8a03l.png)

## 想法示意圖

一開始從 KB 取得 keycode，接下來就可以連結到兩個部分:

- 音效 music: 按下去時候的鼓聲
- DOM style: 按下去時候的變大特效

然後從特效這邊會延伸出去一些東西:

- add class: 放大的黃圈特效
- transform: add class 之後他會做這個動畫變形
- transition: 這個跟 transform 是連動的
- remove class: 移除後恢復按下去之前的樣子

![](https://i.imgur.com/AeYB2i6.png)

## 完整程式碼

```javascript=
  <script>
    ;(function () {
      function playHandler(e) {
        const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
        if (audio) {
          audio.currentTime = 0; //連續觸發的關鍵
          audio.play();
        }
        const dom = document.querySelector(`div[data-key="${e.keyCode}"]`); // 這邊字串必須使用``這個裡面的符號才有意義
        if (dom) dom.classList.add('playing'); //這邊的add是method
      }

      function transitionendHandler(e) {
        console.log(e);

        if (e.propertyName === 'transform') {
          e.currentTarget.classList.remove('playing')
        }
      }
      window.addEventListener('keydown', playHandler)
      document.querySelectorAll('.key').forEach(function (key) {
        key.addEventListener('transitionend', transitionendHandler)
      })
    })()
  </script>
```

---

## keyboardEvent 裡面的值

印出來之後裡面會有很多 property，然後裡面有兩個比較重要的會是 key 跟 keycode

![](https://i.imgur.com/UyTv5Y4.png)

```javascript=

    window.addEventListener('keydown', playHandler);
    //這邊使用keydown是因為想讓他按著可以一直撥放
    function playHandler(e){
    console.log(e)

```

下圖可以看到那些 keycode 可以放在 HTML 裡面待會讓 JS 去做對應

![](https://i.imgur.com/nh5PLZi.png)

![](https://i.imgur.com/jrXPz2T.png)

## Play music

這邊使用了 ES6 的 template string ` (``) `所以她後面才會加${}並且裡面放的就是 keycode 讓他抓取到鍵盤按下去的物件，接下來設定 if 條件來讓他發出聲音

```javascript=
function playHandler(e) {

const audio = document.querySelector(`audio[data-key="${e.keyCode}"]`);
    //上方這段程式碼就已經找到鍵盤對應的audio區塊了
    if (audio) {
        // 這邊使用if可以讓不是keycode範圍內的鍵盤不會跳出錯誤因為會直接跳出這個條件式避免太多出錯
         audio.currentTime = 0; //連續觸發的關鍵
         audio.play();// 這邊play也是方法還有個兄弟pause()
        }
}
```

## DOM style

這樣一樣去抓取要跳出特效的 div 然後使用 if 條件去他去跑'playing'這個 class 而不是原來那個

```javascript=
const dom = document.querySelector(`div[data-key="${e.keyCode}"]`);
// 這邊因為要出現的是那個物件的特效所以選取的是div
        if (dom) dom.classList.add('playing');

        //這邊的add是method 通常會一起用的還有remove跟toggle
```

上面那行程式碼只做了讓他放大且變黃的特效，接下來要來處理放開之後變回原狀(class 要收掉)

![](https://i.imgur.com/u1uBXEA.png)

![](https://i.imgur.com/QAWHIzq.png)

一開始先選取所有的.key 的部分加入監聽之後使用`transitionend`並加入函式`transitionendHandler`

```javascript=


document.querySelectorAll('.key').forEach(function (key) {
key.addEventListener('transitionend', transitionendHandler)
        // transitionend是事件event
      })

function transitionendHandler(e) {
    if (e.propertyName === 'transform') {
        //propertyName 這個是property
          e.currentTarget.classList.remove('playing')
        }
      }
```

下方這些東西是當 transition 效果結束之後會回傳的內容，在這裡我們就拿 propertyName = transform 這個來當指標，當 transform 出來（也就是 transition 結束，transitionend 被觸發時），把 .playing 這個 class 移除。

```javascript=
//可以用這串驗證一下
function transitionendHandler(e) {
        console.log(e);
```

![](https://i.imgur.com/pMkgNqy.png)

## 小補充

- data-\* attribute 屬性:可自定義名稱
- keycode:每個鍵盤按鍵都有對應的 keycode
- es6 語法:箭頭函式、模板字串符(變數${})
