---
title: 實作練習-長得很像Microsoft登入頁面
date:
tags: [HTML, CSS, Flex]
category: HTML, CSS 作品
---

# 長得很像 Microsoft 登入頁面的專案

---

## tags: HTML CSS relate

###### tags: `HTML, CSS`

![](https://i.imgur.com/S5OzDYd.png)

[作品連結](https://chiehLiu.github.io/git-projects/Microsoft/)

**reset css 起頭**

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
```

全域按鈕設定，按鈕大小、邊框關閉、顏色、padding 文字以及 inline-block 因為 a 的預設是 inline，下方設置 hover 碰觸時觸發一點透明。

```css=
.btn {
    cursor: pointer;
    display: inline-block;
    border: 0;
    font-weight: bold;
    padding: 10px 20px;
    background: #262626;
    color: #fff;
    font-size: 15px;;
  }

  .btn:hover{
      opacity: 0.9;
  }
```

**Head**

這邊因為網站內容需要有一些 icon 所以有引入一個 link

![](https://i.imgur.com/0MrLkwy.png)

---

**body**

首先視窗右上方條狀選單 icon，讓他跟下方的區域分開，這個部分比較特別的是它是設定在視窗縮小到 700px 以及以下的時候才會顯示出來專門給其他行動裝置使用的。

![](https://i.imgur.com/IeQwMgj.png)

html:

```html
<div class="menu-btn">
  <i class="fas fa-bars fa-2x"></i>
</div>
```

css:

設定滑鼠過去會出現手，絕對定位在 body 上面，然後先不顯示因為要配合 js 在螢幕縮小到 700px 以下的時候才會呈現

```css
.menu-btn {
  cursor: pointer;
  position: absolute;
  top: 20px;
  right: 30px;
  z-index: 2;
  display: none;
}
```

css:

整個網頁的設定字體、背景顏色設定、文字設定、文字大小、行高

```css
body {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  background: #fff;
  color: #000;
  font-size: 15px;
  line-height: 1.5;
}
```

整個網頁超連結、icon 的文字顏色、去除超連結底線、消除無序清單的點點

.container 的部分設定基本的寬度以及最大的呈現象數，然後讓他們置中

```css
a{
    color: #262626;
    text-decoration: none;(去除底線)

}

ul{
    list-style: none;
}

.container{
    width: 90%; (整體寬度設定%樹讓他可以縮放)
    max-width: 1100px; (最大成象)
    margin: auto; (置中)
}
```

---

**Nav**

![](https://i.imgur.com/trubSoF.png)

html:

`<nav class="main-nav>`

css:

設定 flex 內容物都可以呈現一行出去，接著置中，讓中間有空隙，並且設定高度，padding 設定上下 20px，文字大小設定

```css
.main-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 60px;
  padding: 20px 0;
  font-size: 13px;
}
```

引入圖片檔，給予名稱 Microsoft，並且設定 class="logo"

html:

```html
<nav class="main-nav">
  <img src="https://i.ibb.co/wwLhz98/logo.png" alt="Microsoft" class="logo" />
</nav>
```

css:

設定圖片大小

```css
.main-nav .logo {
  width: 110px;
}
```

ul 的部分設定超連結以及打上文字並且設定 class="main-menu"

html:

```html
<ul class="main-menu">
  <li><a href="#">Office</a></li>
  <li><a href="#">Windows</a></li>
  <li><a href="#">Surface</a></li>
  <li><a href="#">Xbox</a></li>
  <li><a href="#">Deals</a></li>
  <li><a href="#">Support</a></li>
</ul>
```

css:

ul 設定 flex 讓他們一樣整排出去，設定左右 padding 20px，設定超連結下方的 padding 2px，設定 hover 的部分讓滑鼠過去的時候會出現底線，設定 flex:1 讓各個 flex 的大小一樣，然後往右靠一些。

```css
.main-nav ul {
  display: flex;
}

.main-nav ul li {
  padding: 0 10px;
}

.main-nav ul li a {
  padding-bottom: 2px;
}

.main-nav ul li a:hover {
  border-bottom: 2px solid #262626;
}

.main-nav ul.main-menu {
  flex: 1;
  margin-left: 20px;
}
```

下方這邊是右邊的 icon 放大鏡跟購物車

![](https://i.imgur.com/YxKwFAj.png)

html:

```html
<ul class="right-menu">
  <li>
    <a href="#">
      <i class="fas fa-search"></i>
    </a>
  </li>
  <li>
    <a href="#">
      <i class="fas fa-shopping-cart"></i>
    </a>
  </li>
</ul>
```

**showcase 區域**

呈現一個圖片的視覺區域以及一個按鈕加上文字敘述

![](https://i.imgur.com/3tLElyO.png)

他算是一個主要產品的區域故使用 header，並且帶入一些 icon 在按鈕的地方

html:

```html
<header class="showcase">
  <h2>Sruface Deals</h2>
  <p>Select Surfaces are on sale now - save while supplies last</p>
  <a href="#" class="btn"> Shop Now <i class="fas fa-chevron-right"></i> </a>
</header>
```

css:

一樣寬度設定 100%，讓他可以縮放，設定高度、引入圖片、一樣設定成 flex 但是屬性改成讓他成欄的，並且都置中然後設定一些 margin padding，flex-end 對齊底部。

接下來的設定是關於文字以及按鈕

```css
.showcase {
  width: 100%;
  height: 400px;
  background: url("https://i.ibb.co/zGSDGCL/slide1.png") no-repeat center
    center/cover;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  justify-content: flex-end;
  padding-bottom: 50px;
  margin-bottom: 20px;
}

.showcase h2,
.showcase p {
  margin-bottom: 10px;
}

.showcase .btn {
  margin-top: 20px;
}
```

**Home cards 1 的區域**

使用了 grid 來呈現多處的 margin，並且一樣帶入 icon

![](https://i.imgur.com/mHvYkq6.png)

html:

<!-- Home cards 1 -->

有四個 div 來呈現

```html
<section class="home-cards">
  <div>
    <img src="https://i.ibb.co/LZPVKq9/card1.png" alt="" />
    <h3>New Surface Pro 7</h3>
    <p>
      See how Katie Sowers, Asst. Coach for the 49ers, uses Surface Pro 7 to put
      her plans into play.
    </p>
    <a href="#">Learn More <i class="fas fa-chevron-right"></i></a>
  </div>
  <div></div>
</section>
```

css:

這邊直接使用 gird 並且讓他使用 1fr 的比例並且重複四次因此螢幕上有四個視窗之間的 gap 跟 margin-bottom 讓畫面更好看

圖片的部分一樣設定 100%讓他可以縮放並且一樣用 margin-bottom 來調整位置

這邊超連結的部分有設定 hover 來產生特效，當觸摸的時候箭頭會往前噴一點點，
然後超連結也是設定 inline-block 來讓他不要成行，設定文字顏色以及字體粗細。

```css
.home-cards {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 20px;
  margin-bottom: 40px;
}

.home-cards img {
  width: 100%;
  margin-bottom: 20px;
}

.home-cards h3 {
  margin-bottom: 5px;
}

.home-cards a {
  display: inline-block;
  padding-top: 10px;
  color: #0067b8;
  text-transform: uppercase;
  font-weight: bold;
}

.home-cards a:hover i {
  margin-left: 10px;
}
```

**Xbox**

基本上跟 showcase 區域一樣只是換個排版跟圖片

![](https://i.imgur.com/EewKYn5.png)

html:

```html
<!-- Xbox -->
<section class="xbox">
  <div class="content">
    <h2>Xbox Game Pass Ultimate</h2>
    <p>
      Xbox Game Pass Ultimate Xbox Live Gold and over 100 high-quality console
      and PC games. Play together with friends and discover your next favorite
      game.
    </p>
    <a href="#" class="btn"> Join Now <i class="fas fa-chevron-right"></i> </a>
  </div>
</section>
```

css:

這邊很簡單跟上方的 showcase 的部分處理差不多，但在文字處理的部分使用了 width:40%讓文字框縮小，段落的文字加上 margin 讓他們更好看

```css
.xbox {
  width: 100%;
  height: 350px;
  background: url("https://i.ibb.co/tBJGPD9/xbox.png") no-repeat center
    center/cover;
  margin-bottom: 20px;
}

.xbox .content {
  width: 40%;
  padding: 50px 0 0 30px;
}

.xbox p,
.carbon p {
  margin: 10px 0 20px;
}
```

**Home cards 2**

基本跟 Home card 1 一樣，一樣使用 grid

![](https://i.imgur.com/W6lMDu7.png)

四個 div 呈現

html:

```html
<section class="home-cards">
  <div>
    <img src="https://i.ibb.co/zVqhWn2/card5.png" alt="" />
    <h3>Microsoft Teams</h3>
    <p>Unleash the power of your team.</p>
    <a href="#">Shop Now <i class="fas fa-chevron-right"></i></a>
  </div>
</section>
```

css:

這邊的處理基本上參考上方的 css 即可，基本上是一樣的東西

**Carbon**

又一個主要商品呈現區跟上方 showcase 呈現方式一樣

![](https://i.imgur.com/0T9ncJf.png)

html:

```html
<section class="carbon dark">
  <div class="content">
    <h2>Commiting To Carbon Negative</h2>
    <p>
      Microsoft will be carbon negative by 2030 and by 2050 we will remove all
      carbon the company has emitted since it was founded in 1975
    </p>
    <a href="#" class="btn">
      Learn More <i class="fas fa-chevron-right"></i>
    </a>
  </div>
</section>
```

css:

這邊修飾了 carbon 的整個容器並加入圖片方式都跟之前的一樣，文字的部分跟 Xbox 區域差不多，使用 width:40%讓他縮小並加入 padding 修飾版面

```css
.carbon {
  width: 100%;
  height: 350px;
  background: url("https://i.ibb.co/72cgtsz/carbon.jpg") no-repeat center
    center/cover;
}

.carbon .content {
  width: 55%;
  padding: 100px 0 0 30px;
}
```

裝飾圖片內文以及因為這個圖片的關係不能使用全域的一些顏色設定所以抓出來在這邊設定

```css
.dark {
  color: #fff;
}

.dark .btn {
  background: #f4f4f4;
  color: #333;
}
```

**Follow**

icon 加上簡單文字排列

![](https://i.imgur.com/CZpS4i0.png)

html:

```html
<section class="follow">
  <p>Follow Microsoft</p>
  <a href="https://facebook.com">
    <img src="https://i.ibb.co/LrVMXNR/social-fb.png" alt="Facebook" />
  </a>
  <a href="https://twitter.com">
    <img src="https://i.ibb.co/vJvbLwm/social-twitter.png" alt="Twitter" />
  </a>
  <a href="https://linkedin.com">
    <img src="https://i.ibb.co/b30HMhR/social-linkedin.png" alt="Linkedin" />
  </a>
</section>
```

css:

這邊針對三個 icon 做排列美化，使用 flex 讓他們成行，置中並且設定 margin 讓他們有中間有空隙並且修飾。

```css
.follow {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  margin: 30px 0 30px;
}

.follow * {
  margin-right: 10px;
}
```

**Link**

簡單的列表，但是在 html 的部分有個小巧思，link 的 tag 跟其他所以的部分都分開，這樣製作背景色會更好看切得更順。

![](https://i.imgur.com/19MWOju.png)

html:

```html
<section class="links">
  <div class="links-inner">
    <ul>
      <li><h3>What's New</h3></li>
      <li><a href="#">Surface Pro X</a></li>
      <li><a href="#">Surface Laptop 3</a></li>
      <li><a href="#">Surface Pro 7</a></li>
      <li><a href="#">Windows 10 apps</a></li>
      <li><a href="#">Office apps</a></li>
    </ul>
  </div>
</section>
```

css:

設定背景色、文字顏色、文字大小、padding 修飾版面，

inner 的部分是設定所有的 flexbox，設定最大寬度讓他們不會跑版，以及一些 margin padding 修飾版面，再來設定 grid 的部份讓版面整齊平分版面並且置中。

```css
.links {
  background: #f2f2f2;
  color: #616161;
  font-size: 12px;
  padding: 35px 0;
}

.links-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px;
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-gap: 10px;
  align-items: flex-start;
  justify-content: center;
}

.links li {
  line-height: 2.8;
}
```

**Footer**

icon 加上一些連結文字排列

![](https://i.imgur.com/KtOiunH.png)

html:

```html
<footer class="footer">
  <div class="footer-inner">
    <div><i class="fas fa-globe fa-2x"></i> English (United States)</div>
    <ul>
      <li><a href="#">Sitemap</a></li>
      <li><a href="#">Contact Microsoft</a></li>
      <li><a href="#">Privacy & cookies</a></li>
      <li><a href="#">Terms of use</a></li>
      <li><a href="#">Trademarks</a></li>
      <li><a href="#">Safety & eco</a></li>
      <li><a href="#">About our ads</a></li>
      <li><a href="#">&copy; Microsoft 2020</a></li>
    </ul>
  </div>
</footer>
```

css:

最外框一樣先設置背景、文字顏色大小(這邊設定的跟 Link 是一樣的)當然 padding 部分不同，
inner 的部分設定 flex 讓他們成行，這邊有使用 space-between，讓他們之間產生等距的空隙，
然後這邊設定的 felx 只會讓那個 globle 的球那個 div 跟所有的 ul 成兩欄排咧，所以下面的 ul 部分需要再設定一次 flex，以及 div 的地方都需要有 flex，這邊因為希望 ul 可以做換行所以使用 wrap 來修飾。

```css
.footer {
  background: #f2f2f2;
  color: #616161;
  font-size: 12px;
  padding: 20px 0;
}

.footer-inner {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px 0 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.footer div {
  margin-bottom: 20px;
  display: flex;
  align-items: center;
}

.footer div i {
  margin-right: 10px;
}

.footer ul {
  display: flex;
  flex-wrap: wrap;
}

.footer li {
  margin-right: 30px;
  margin-bottom: 20px;
}
```

**Javascript**

這部分看不懂，不過他主要是呈現按下選單之後彈出透明視窗這個功能

![](https://i.imgur.com/2dgn78E.png)

```javascript
<script>
  document.querySelector('.menu-btn').addEventListener('click', () =>
  document.querySelector('.main-menu').classList.toggle('show'));
</script>
```
