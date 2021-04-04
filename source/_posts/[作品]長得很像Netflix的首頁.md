---
title: 實作練習-長得很像Netflix的首頁
date:
tags: [HTML, CSS, Flex]
category: HTML, CSS 作品
---

# 長得很像 Netflix 的首頁

---

## tags: HTML CSS relate

###### tags: `HTML, CSS`

![](https://i.imgur.com/03o0USl.jpg)

[作品連結](https://chiehLiu.github.io/git-projects/NETFLIX/)

這個專案一樣有用到一點 js，不過我就專注在練習切版。

全域設定:

```css=
    /*簡單的全域顏色變數*/
:root {
    --primary-color: #e50914;
    --dark-color: #141414;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

    /*字體清晰度設定-這邊設定的是平滑無鋸齒*/
body {
    font-family: 'Arial', sans-serif;
    -webkit-font-smoothing: antialiased;
    background: #000;
    color: #999;
}

ul {
    list-style: none;
}

h1,
h2,
h3,
h4 {
    color: #fff;
}

a {
    color: #fff;
    text-decoration: none;
}

p {
    margin: 0.5rem 0;
}

img {
    width: 100%;
}
```

---

**功能性設定**

tab 區域的 items

```css=
/* Container */

/* 這個地方可以讓tabs跟著視窗縮放以及讓他們置中並且修飾他們 */
.container {
    max-width: 70%;
    margin: auto;
    overflow: hidden;
    padding: 0 2rem;
}
```

各種文字的基本樣式

```css=
/* Text Styles 這邊是text的功能鍵區域 設定他們的大小顏色並可以任意丟進去需要的地方 */
.text-xl {
    font-size: 2rem;
}

.text-lg {
    font-size: 1.8rem;
    margin-bottom: 1rem;
}

.text-md {
    margin-bottom: 1.5rem;
    font-size: 1.2rem;
}

.text-center {
    text-align: center;
}

.text-dark {
    color: #999;
}
```

所有的按鈕的基本樣式

```css=
/* Buttons */
.btn {
    display: inline-block;
    background: var(--primary-color);
    color: #fff;
    padding: 0.4rem 1.3rem;
    font-size: 1rem;
    text-align: center;
    border: none;
    cursor: pointer;
    margin-right: 0.5rem;
    transition: opacity 0.2s ease-in;
    outline: none;
    box-shadow: 0 1px 0 rgba(0, 0, 0, 0.45);
    border-radius: 2px;
}
```

**head:**

這邊中間的 script 的部分是引入 icon

```htmlembedded=
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <script src="https://kit.fontawesome.com/b6d6d6c74b.js" crossorigin="anonymous">
    </script>
    <link rel="stylesheet" href="css/style.css">
    <title>Netflix - Watch TV Shows Online, Watch Movies Online</title>
</head>
```

---

**body:**

要處理的部分有四點:

1.兩個紅色框框區塊

2.背景圖片

3.使用偽元素上陰影

4.調整所有文字以及按鈕部分

![](https://i.imgur.com/SKBO3HF.jpg)

有最上方 Netflix 跟 Sign in 處，用 header 來處理

html:

```htmlembedded=
<header class="showcase">
        <div class="showcase-top">
            <img src="https://i.ibb.co/r5krrdz/logo.png" alt="" />
            <a href="#" class="btn btn-rounded">Sign In</a>
        </div>
        <div class="showcase-content">
            <h1>See what's next</h1>
            <p>Watch anywhere. Cancel Anytime</p>
            <a href="#" class="btn btn-xl">Watch Free For 30 Days <i class="fas fa-chevron-right btn-icon"></i></a>
        </div>
    </header>
```

css:

這裡設定的是整片視窗的圖片大小以及設定定位給其他的物件

```css=
.showcase {
    width: 100%;
    height: 93vh;
    /* 這邊先設定相對定位因為等下會設定其他絕對定位在這個父層上面 */
    position: relative;
    background: url('https://i.ibb.co/vXqDmnh/background.jpg') no-repeat center center/cover;
}
```

這邊使用偽元素來疊層上去陰影

```css=
.showcase::after {
    /* content是偽元素必備的屬性內容可以為空也可以填入文字顯示 */
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    /* zindex代表覆蓋的順序 */
    z-index: 1;
    /* 這邊的rgba的a的部分代表透明度0%代表透明100%代表不透明 */
    background: rgba(0, 0, 0, 60%);
    /* box-shadow處理陰影 因為有兩側所以設定了兩組，左邊那組設定負的px*/
    box-shadow: inset 120px 100px 250px #000000, inset -120px -100px 250px #000000;
}
```

這邊主要控制的是 Netflix 那一整條的區域並設定高度

```css
.showcase-top {
  position: relative;
  /* zindex代表覆蓋的順序 */
  z-index: 2;
  height: 90px;
}
```

這邊就是針對 Netflix 圖片 logo 的部分調整定位 大小

```css
.showcase-top img {
  width: 170px;
  /* 向這邊它就定位在showcase-top上面 */
  position: absolute;
  /* 這邊比較複雜，因為logo的部分也有長度所以當設定好定位的時候logo的長度會凸出去，
    所以這個時候就可以使用transform: translate(-50%, -50%)，讓logo長度的50%左右跟上下回來就會置中瞜! */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

這邊處理 link 的部分也就是 Sign In 的部位

```css
.showcase-top a {
  /* 按鈕必須移動位置所以設定absolute */
  position: absolute;
  top: 50%;
  right: 0;
  /*這邊一樣因應按鈕本身就有寬度所以使用transform: translate(-50%, -50%)上下往回50%就可以置中了*/
  transform: translate(-50%, -50%);
}
```

這邊是中間的紅框文案內容區域+一個大按鈕

```css
.showcase-content {
  position: relative;
  /* zindex代表覆蓋的順序必須蓋過陰影 */
  z-index: 2;
  width: 65%;
  margin: auto;
  /* 這邊就很直觀直接Flex下去 */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  margin-top: 9rem;
}
```

針對內文調整

```css
.showcase-content h1 {
  font-weight: 700;
  font-size: 5.2rem;
  line-height: 1.1;
  margin: 0 0 2rem;
}

.showcase-content p {
  text-transform: uppercase;
  color: #fff;
  font-weight: 400;
  font-size: 1.9rem;
  line-height: 1.25;
  margin: 0 0 2rem;
}
```

---

**tab 區域**

重點部分:

1.3 個 icon 處理

2.紅色跟深灰色底線處理

3.bgc 的顏色比較淡要改

![](https://i.imgur.com/hhmabCE.png)

html:

這部分有牽涉到一些 js，我會注重再切版的部分。

```htmlembedded=
<section class="tabs">
        <div class="container">
            <div id="tab-1" class="tab-item tab-border">
                <i class="fas fa-door-open fa-3x"></i>
                <p class="hide-sm">Cancel at any time</p>
            </div>
            <div id="tab-2" class="tab-item">
                <i class="fas fa-tablet-alt fa-3x"></i>
                <p class="hide-sm">Watch anywhere</p>
            </div>
            <div id="tab-3" class="tab-item">
                <i class="fas fa-tags fa-3x"></i>
                <p class="hide-sm">Pick your price</p>
            </div>
        </div>
    </section>
```

css:

設定整個 tab 區域的背景色跟 padding，加上深灰色底線

```css
.tabs {
  background: var(--dark-color);
  padding-top: 1rem;
  border-bottom: 3px solid #3d3d3d;
  border-right: none;
}
```

這個 container 包住三個 item，所以直接 grid 設定下去很直觀

```css
.tabs .container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 1rem;
  align-items: center;
  justify-content: center;
  text-align: center;
}
```

首先 p 區域是文字區域的大小跟位置微調

設置 container 下面所有的 items 讓它們都有 padding 上下

設置 hover 碰觸時出現手指指標以及呈現白色

每個 icon 下方的紅色 border

```css
.tabs p {
  font-size: 1.2rem;
  padding-top: 0.5rem;
}

.tabs .container > div {
  padding: 1.5rem 0;
}

.tabs .container > div:hover {
  color: #fff;
  cursor: pointer;
}

.tab-border {
  border-bottom: var(--primary-color) 4px solid;
}
```

**Tab Content**

區域一

![](https://i.imgur.com/okXOvSL.png)

比較直觀就直接一個 div 解決

html:

```htmlembedded=
<section class="tab-content">
        <div class="container">
            <!-- Tab Content 1 -->
            <div id="tab-1-content" class="tab-content-item show">
                <div class="tab-1-content-inner">
                    <div>
                        <p class="text-lg">
                            If you decide Netflix isn't for you - no problem. No commitment.
                            Cancel online anytime.
                        </p>
                        <a href="#" class="btn btn-lg">Watch Free For 30 Days</a>
                    </div>
                    <img src="https://i.ibb.co/J2xDJV7/tab-content-1.png" alt="" />
                </div>
            </div>
```

css:

這邊也是直接 grid 把區塊平分，設定 gap 後全部置中

```css=

/*最上方的tab-content是包裹整個tab區塊的全域設定*/
.tab-content {
    padding: 3rem 0;
    background: #000;
    color: #fff;
}

#tab-1-content .tab-1-content-inner {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 2rem;
    align-items: center;
    justify-content: center;
}
```

**tab 區域二**

這邊要設置兩大部分:

1.content-top
這個部分是上方的文字以及按鈕

2.content-bottom
下方三個 items 以及文案

![](https://i.imgur.com/qYiieuD.png)

html:

```htmlembedded=
<!-- Tab Content 2 -->
           <div id="tab-2-content" class="tab-content-item">
               <div class="tab-2-content-top">
                   <p class="text-lg">
                       Watch TV shows and movies anytime, anywhere — personalized for
                       you.
                   </p>
                   <a href="#" class="btn btn-lg">Watch Free For 30 Days</a>
               </div>
               <div class="tab-2-content-bottom">
                   <div>
                       <img src="https://i.ibb.co/DpdN7Gn/tab-content-2-1.png" alt="" />
                       <p class="text-md">
                           Watch on your TV
                       </p>
                       <p class="text-dark">
                           Smart TVs, PlayStation, Xbox, Chromecast, Apple TV, Blu-ray
                           players and more.
                       </p>
                   </div>
                   <div>
                       <img src="https://i.ibb.co/R3r1SPX/tab-content-2-2.png" alt="" />
                       <p class="text-md">
                           Watch instantly or download for later
                       </p>
                       <p class="text-dark">
                           Available on phone and tablet, wherever you go.
                       </p>
                   </div>
                   <div>
                       <img src="https://i.ibb.co/gDhnwWn/tab-content-2-3.png" alt="" />
                       <p class="text-md">
                           Use any computer
                       </p>
                       <p class="text-dark">
                           Watch right on Netflix.com.
                       </p>
                   </div>
               </div>
           </div>
```

css:

這邊處理全部都直接 grid，設置好版面比例之後就直接置中很直觀

```css=
#tab-2-content .tab-2-content-top {
    display: grid;
    grid-template-columns: 2fr 1fr;
    grid-gap: 1rem;
    justify-content: center;
    align-items: center;
}

#tab-2-content .tab-2-content-bottom {
    margin-top: 2rem;
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-gap: 2rem;
    justify-content: center;
    align-items: center;
    text-align: center;
}
```

**tab 區域三 table**

這邊來製作表單:

上方大標題以及紅色按鈕使用兩個全域型 class 來設定，class="text-center",class="text-lg"
這兩個 class 內部自訂文字顏色大小並且置中

![](https://i.imgur.com/XX0YThW.png)

表頭(thead)

![](https://i.imgur.com/4QghtMb.png)

表身體(tbody)

![](https://i.imgur.com/wv4Jf17.png)

html:

```htmlembedded=
<!-- Tab Content 3 -->
            <div id="tab-3-content" class="tab-content-item">
                <div class="text-center">
                    <p class="text-lg">
                        Choose one plan and watch everything on Netflix.
                    </p>
                    <a href="#" class="btn btn-lg">Watch Free For 30 Days</a>
                </div>

                <table class="table">
                    <thead>
                        <tr>
                            <th></th>
                            <th>Basic</th>
                            <th>Standard</th>
                            <th>Premium</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>Monthly price after free month ends on 6/19/19</td>
                            <td>$8.99</td>
                            <td>$12.99</td>
                            <td>$15.99</td>
                        </tr>
                        <tr>
                            <td>HD Available</td>
                            <td><i class="fas fa-times"></i></td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                        <tr>
                            <td>Ultra HD Available</td>
                            <td><i class="fas fa-times"></i></td>
                            <td><i class="fas fa-times"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                        <tr>
                            <td>Screens you can watch on at the same time</td>
                            <td>1</td>
                            <td>2</td>
                            <td>4</td>
                        </tr>
                        <tr>
                            <td>Watch on your laptop, TV, phone and tablet</td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                        <tr>
                            <td>Unlimited movies and TV shows</td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                        <tr>
                            <td>Cancel anytime</td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                        <tr>
                            <td>First month free</td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                            <td><i class="fas fa-check"></i></td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </section>
```

css:

class="table"包裹住全部的表格，並且讓格線崩塌

.table thead th 讓 Basic Standard Premium 大寫並調整它們的 padding

.table tbody 這邊都是他的預設屬性(我查資料已經不適用於 HTML5)

接下來兩個設定是為了讓他們做變色框的設定也很直觀

```css=
.table {
    width: 100%;
    margin-top: 2rem;
    /*讓所有格線崩塌*/
    border-collapse: collapse;
    /*表格間的距離*/
    border-spacing: 0;
}

.table thead th {
    text-transform: uppercase;
    padding: 0.8rem;
}

.table tbody {
    display: table-row-group;
    vertical-align: middle;
    border-color: inherit;
}

.table tbody tr td {
    color: #999;
    padding: 0.8rem 1.2rem;
    text-align: center;
}

.table tbody tr td:first-child {
    text-align: left;
}

.table tbody tr:nth-child(odd) {
    background: #222;
}
```

**Footer**

兩個部分組成:

上方一個段落 p

footer-cols

![](https://i.imgur.com/afinGiM.png)

html:

```htmlembedded=
<footer class="footer">
        <p>Questions? Call 1-866-579-7172</p>
        <div class="footer-cols">
            <ul>
                <li><a href="#">FAQ</a></li>
                <li><a href="#">Investor Relations</a></li>
                <li><a href="#">Ways To Watch</a></li>
                <li><a href="#">Corporate Information</a></li>
                <li><a href="#">Netflix Originals</a></li>
            </ul>
            <ul>
                <li><a href="#">Help Center</a></li>
                <li><a href="#">Jobs</a></li>
                <li><a href="#">Terms Of Use</a></li>
                <li><a href="#">Contact Us</a></li>
            </ul>
            <ul>
                <li><a href="#">Account</a></li>
                <li><a href="#">Redeem Gift Cards</a></li>
                <li><a href="#">Privacy</a></li>
                <li><a href="#">Speed Test</a></li>
            </ul>
            <ul>
                <li><a href="#">Media Center</a></li>
                <li><a href="#">Buy Gift Cards</a></li>
                <li><a href="#">Cookie Preferences</a></li>
                <li><a href="#">Legal Notices</a></li>
            </ul>
        </div>

    </footer>
```

css:

整個 footer 區域為了比上方的 containter 大一些，所以多設置了 max-width，並且上下加點 margin 並且置中，在使用 overflow 的方式讓它出現卷軸。

footer-cols 的部分一樣使用 grid 讓他們四個成一排

```css=
.footer {
    /* 這邊因為希望比container大所以沒有使用container而是額外使用max-width */
    max-width: 70%;
    margin: 1rem auto;
    overflow: auto;
}

.footer,
.footer a {
    color: #999;
    font-size: 0.9rem;
}

.footer p {
    margin-bottom: 1.5rem;
}

.footer .footer-cols {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 2rem;
}

.footer li {
    line-height: 1.9;
}
```

---

**@media**

這邊解釋網頁縮放的設定:

當畫面小於 960px 得時候下方條件生效，除了一些東西縮小之外，有文字隱藏，logo 位置調整，

四排的物件縮排便成兩排

當畫面小於 700px 時還有另一部份的條件會生效，陰影的部分會變小，兩排的物件變成一排，以及一些微條

```css=
@media (max-width: 960px) {

    .showcase {
        height: 70vh;
    }

    .hide-sm {
        display: none;
    }

    .showcase-top img {
        top: 30%;
        left: 5%;
        transform: translate(0);
    }

    .showcase-content h1 {
        font-size: 3.7rem;
        line-height: 1;
    }

    .showcase-content p {
        font-size: 1.5rem;
    }

    .footer .footer-cols {
        grid-template-columns: repeat(2, 1fr);
    }

    .btn-xl {
        font-size: 1.5rem;
        padding: 1.4rem 2rem;
        text-transform: uppercase;
    }

    .text-xl {
        font-size: 1.5rem;
    }

    .text-lg {
        font-size: 1.3rem;
        margin-bottom: 1rem;
    }

    .text-md {
        margin-bottom: 1rem;
        font-size: 1.2rem;
    }
}

@media (max-width: 700px) {
    .showcase::after {
        background: rgba(0, 0, 0, 0.6);
        box-shadow: inset 80px 80px 150px #000000, inset -80px -80px 150px #000000;
    }

    .showcase-content h1 {
        font-size: 2.5rem;
        line-height: 1;
    }

    .showcase-content p {
        font-size: 1rem;
    }

    #tab-1-content .tab-1-content-inner {
        grid-template-columns: 1fr;
        text-align: center;
    }

    #tab-2-content .tab-2-content-top {
        display: block;
        text-align: center;
    }

    #tab-2-content .tab-2-content-bottom {
        margin-top: 2rem;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 2rem;
        text-align: center;
    }

    .btn-xl {
        font-size: 1rem;
        padding: 1.2rem 1.6rem;
        text-transform: uppercase;
    }
}

@media(max-height: 600px) {
    .showcase-content {
        margin-top: 3rem;
    }
}
```
