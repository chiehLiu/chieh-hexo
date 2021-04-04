---
title: 實作練習-Clothes Store - SASS Project
date:
tags: [HTML, CSS, Grid, SASS]
category: HTML, CSS 作品
---

# Clothes Store - SASS Project

---

## tags: Javascript relate

###### tags: `HTML, CSS, SASS`

# 製作一個衣服購物網站

## 成品:

![](https://i.imgur.com/hEEPgbC.jpg)

[成品網址](https://chiehliu.github.io/git-projects/clothesStore/index.html)

## 成品功能:

1.有兩條 navbar 其中一條有 hover 出下拉選單 2.投影片區域每 4 秒更新，淺入淺出特效 3.商品區域 hover 出現價錢跟購買按鈕並且商品帶有透明特效 4.下方 see more 按鈕有特效處理
5.footer 區域字樣以及按鈕做 hover 變色，input 內部區域做 focus 外框變色
6.RWD 針對 1200, 1000, 760, 560px 大小作處理

# HTML

## html 程式碼:

[html.index](https://github.com/chiehLiu/git-projects/blob/clothesStore/clothesStore/index.html)

# SCSS:

下面我以資料夾做分類解析

# main.scss

## main.scss

處理全部的 import 並且按照資料夾分類處理

```sass=
@import "abstracts/variables";
@import "abstracts/mixins";
@import "base/base";

@import "layout/header";
@import "layout/navigation";
@import "layout/slideshow";
@import "layout/products";
@import "layout/footer";

@import "components/logo";
@import "components/heading";
@import "components/dropdown";
@import "components/button";
```

# base

## \_base.scss

### 全域字體大小處理

作者想要使用 10px 代替 16px 作為基礎 1rem 因為比較方便
所以 10/16=0.625 使用到趴數上面就是 62.5%

### `.container` 包裹住全體物件的容器直接設計 grid 框架上去

作者把物件都用這些 grid 出現的格線去做排列，並且把上面的元素固定在規畫好的格線內

- grid-template-columns 設定每一行的每個區塊怎麼分大小以及分幾塊
- grid-template-rows 設定每一列的每個區塊怎麼分大小以及分幾塊
- grid-row-gap 行的間距

![](https://i.imgur.com/hwQ8u4N.jpg)

- `minmax()`使用兩個參數(最大值, 最小值) 功能使內容物不跑版
- fr 代表可用空間的分塊的每一塊的的代表假設寫成 1fr,1fr,1fr 代表區塊分成三塊並且大小相同
  寫成 2fr,1fr,1fr 代表第一塊是兩倍大其他兩個大小相同
- max/min-content 代表所屬 block 的最大以及最小值下方範例使用`min-content`代表最小所以都是最小單位也就是內容物多大這個空間就多大
- 使用函式`color()`取用 map `$colors`裡面的內容

```sass=
* {
    margin: 0;
    padding: 0;
    font-family: 'Josefin Sans', sans-serif;
}

// 這邊因為作者想要使用10px代替16px作為基礎 1rem 因為比較方便
// 所以10/16=0.625 使用到趴數上面就是62.5%
html {
    font-size: 62.5%;

    @include response(md) {
        font-size: 56.25%;
        //9/16 = 56.25;
    }

    @include response(sm) {
        font-size: 50%;
        //8/16 = 56.25;
    }
}

// minmax使用兩個參數(最大值, 最小值) 功能使內容物不跑版
// fr代表可用空間的分塊的每一塊的的代表假設寫成 1fr,1fr,1fr代表區塊分成三塊並且大小相同
// 寫成 2fr,1fr,1fr代表第一塊是兩倍大其他兩個大小相同
// max/min-content 代表所屬block的最大以及最小值下方範例使用min-content代表最小所以都是最小單位
//使用函式color取用map $colors裡面的內容
.container {
    display: grid;
    grid-template-columns: minmax(6rem, 1fr) repeat(8, minmax(min-content, 16rem)) minmax(6rem, 1fr);
    grid-template-rows: repeat(4, min-content);
    grid-row-gap: 1.6rem;
    background-color: color(tertiary);
}
```

# abstracts

## \_variables.scss

設置顏色，文字的 function

```sass=
$colors: (primary:#333,
    secondary:#ffe,
    tertiary:#f2f0f1,
    quaternary:#f5b149,
);

@function color($color-name) {
    @return map-get($colors, $color-name);
}

$font-sizes:(xl:3rem,
    lg:2.5rem,
    md:2rem,
    sm:1.8rem,
    xs:1.6rem);

@function size($size) {
    @return map-get($font-sizes, $size);
}
```

## \_mixins.scss

### navigation

first-nav/second-nav 重複的地方直接擷取近來這邊:

- display
- 定位 space-around
- height
- list-style
- link 部分字體的修飾以及 hover 特效

### flexPosition($justCont: center, $alignIte:center)

預設全置中

- display: flex
- justify-content: $justCont
- align-items: $alignIte

### footerList

- 處理 footer 文字部分修飾
- hover 特效

### response

處理全部的 RWD
並且使用 if 判斷式下方舉一個做例子:

判斷的地方填入 sm,md,lg,xl 來做數字的代替，並且使用@content 來代替不同的處理內容會寫在各處要被處理的地方裡面這邊的@content 比較像個代表

```sass=
@if($breakpoint==xl) {
        @media(max-width:1200px) {
            @content;
        }
    }
```

# components

## \_buttons.scss

![](https://i.imgur.com/F2N4TI8.png)

處理 products 區域下方的 See More btn:

1. position 定位 relative
1. 寬高
1. 定位部分選擇 space-around

### hover 特效:

![](https://i.imgur.com/bidBhwR.gif)

主要處理整個背景伸長 箭頭旋轉、伸長特效

- 寬度增加
- 文字變色
- 箭頭尖端處移動
  設定三條直線的 div 並且作 Z 軸旋轉，為了因應 hover 特效則處理水平移動
- 箭柄伸長
  設定的直線做水平移動達到伸長特效

## \_dropdown.scss

使用`::after`做出 icon 效果
![](https://i.imgur.com/aizQeh8.png)

```sass=
&::after {
        font-family: 'Font Awesome 5 Free';
        content: '\f078';
        font-weight: bold;
    }
```

處理 hover 特效碰到才會出現不然一般呈現隱藏以及透明

![](https://i.imgur.com/Ub0GVKo.gif)

```sass=
&:hover .dropdown {
        visibility: visible;
        opacity: 1;
    }
```

使用`@mixin navigation`裡面的文字變色特效以及文字修飾

### 小三角形凸起處

使用`&::before`來做出右上角的尖角
![](https://i.imgur.com/O8FevAH.png)

```sass=
        border-right: 15px solid transparent;
        border-bottom: 15px solid darken(color(tertiary), 5%);
        border-left: 15px solid transparent;
```

## \_heading.scss

大標題文字修飾
![](https://i.imgur.com/4eU3ZFp.png)

使用 gird-colum/row 抓取位置後開始修飾文字

```sass=
.heading {
    grid-column: 1/-1;
    grid-row: 2 / 3;
    text-align: center;

    &-text {
        font-family: 'Great Vibes', cursive;
        font-size: size(xl)*2;
        font-weight: lighter;
        letter-spacing: 0.5rem;
    }
}
```

## \_logo.scss

![](https://i.imgur.com/tea4ivA.png)

使用 gird-colum/row 抓取位置後開始修飾圖片並且高度設定 100%做 RWD

```sass=
.logo {
    grid-column: 1/2;
    grid-row: 1/2;
    padding: 1rem;

    &-img {
        width: 10rem;
        height: 100%;
    }
}
```

# layout

## \_header.scss

在最外層的 gird 容器內再 grid 的一次並且再度劃分行、列的大小

以行舉例:
三個區塊紅 minmax(6rem, 1fr)黃(repeat)綠 minmax(6rem, 1fr)

```sass=
minmax(10rem, 1fr) repeat(7, minmax(min-content, 16rem)) minmax(10rem, 1fr);
```

![](https://i.imgur.com/W5LeISF.png)

![](https://i.imgur.com/VcwwHao.png)

```sass=
.header {
    grid-column: 1 / -1;
    grid-row: 1 / 2;
    display: grid;
    grid-template-columns: minmax(10rem, 1fr) repeat(7, minmax(min-content, 16rem)) minmax(10rem, 1fr);
    grid-template-rows: repeat(3, min-content);
    grid-gap: 2rem;
    z-index: 100;
}
```

## \_navigation.scss

使用`@mixin navigation` 修飾 navbar 文字

基本上都在操作 RWD

```sass=
.second-nav {
    grid-column: 3/8;
    grid-row: 3/4;
    @include navigation;

    @include response(lg) {
        grid-column: 2/9;
    }

    @include response(md) {
        grid-column: 1/-1;
    }
}
```

## \_slideshow.scss

幻燈片 slide 特效配上 fade in&out 每四秒跑一張
![](https://i.imgur.com/6I0c1rT.png)

- 使用 grid 抓好位置
- 設定 position:relative 待會給 description 坐定位使用
- 寬度設定 100%做 RWD 長度抓 80vh 螢幕大小
- RWD 部分更換 vh 大小很直觀

### 每張 slide 處理

- 每張 slide 長寬繼承父層
- 必須先把預設做隱藏不然會 20 秒會才跑第一個動畫
- 避免圖片失真`object-fit: cover`

```sass=
&-slide {

        // 使用定位之後會讓所有圖片疊再一起，最後一張在最上層
        position: absolute;
        top: 0;
        left: 0;
        width: inherit;
        height: inherit;

        // 這邊如果不把slide隱藏掉的話20s過後才會開始跑動畫
        visibility: hidden;
        opacity: 0;
        animation: slideshow 20s linear infinite;

        img {
            width: inherit;
            height: inherit;
            // 避免圖片失真
            object-fit: cover;
        }
    }
```

### slide 特效處理

先建立 list 後跑 each loop 可以得到這個效果出現在 main.css 裡面
![](https://i.imgur.com/7tcMPJk.png)

list:每 4 秒建立一個

each loop:
使用`nth-child()`選取指定元素並且內部參數放入動態的變數`#{}`再使用`nth()`抓取要迭代的內容`$item`的第一部分，animation-delay 的部份則抓取`$item`的第二部分也就是秒數

@keyframes 動畫名稱

製作動畫內容

```sass=
// 使用list 建立第幾個元素以及delay幾秒
$animList: 1 0s,
2 4s,
3 8s,
4 12s,
5 16s;

// 使用nth(前面擺入每個要被個別印出的的元素也就是(1 0s)(2 4s)的代表參數, 後方會擺入index從1開始算起)
@each $item in $animList {
    .slideshow-slide:nth-child(#{nth($item,1)}) {
        animation-delay: nth($item, 2);
    }
}


// 這邊製作fade in/out 的特效頭跟尾都處理隱藏以及透明達到這樣的效果
@keyframes slideshow {
    0% {
        visibility: hidden;
        opacity: 0;
    }

    2% {
        visibility: visible;
        opacity: 1;
    }

    18% {
        visibility: visible;
        opacity: 1;
    }

    20% {
        visibility: hidden;
        opacity: 0;
    }

    100% {
        visibility: hidden;
        opacity: 0;
    }
}
```

## \_products.scss

![](https://i.imgur.com/OH9RHss.png)

商品陳列區域包含一個具有 hover 特效的按鈕

商品也有 hover 特效，沒有 hover 的時候會隱藏

```sass=
&:hover .product-description {
        opacity: 1;
        visibility: visible;
    }

    &:hover .product-img {
        opacity: .5;
    }
```

![](https://i.imgur.com/MWNCkAL.gif)

商品描述欄位

基本處理一些內文背景的修飾

```sass=
 &-description {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: transparentize(color(secondary), .4);
        padding: 2rem;
        border: .1rem solid color(primary);
        border-radius: .5rem;
        color: color(primary);
        text-align: center;
        opacity: 0;
        visibility: hidden;
        transition: all 1s .5s;
        }
```

商品內文區塊的整體修飾

標題/價錢/按鈕

```sass=
&-heading {
            font-size: size(xl);}

&-price {
            font-size: size(lg);
            font-weight: 300;
            margin: 1rem 0;}

&-btn {
            font-size: size(xs);
            text-decoration: none;
            color: color(quaternary);
            display: block;
            padding: .5rem 1rem;
            border: .1rem solid color(quaternary);
            background-color: lighten(color(primary), 20%);}
```

## \_footer.scss

### 聯絡資訊

- 更多資訊欄位
- sign up 欄位
- 聯絡資訊欄位

![](https://i.imgur.com/EkIRMXd.png)

這邊很聰明的地方是針對最左最右兩邊做處理的時候直接使用`@mixin`處理重複的部分
也就是 footerList 這個部分直接統一文字修飾處理

```sass=
@mixin footerList {
    &-heading {
        font-size: size(lg);
        color: color(primary);
    }

    &-item {
        list-style: none;
        margin: 1rem 0;
    }

    &-link {
        font-size: size(xs);
        text-decoration: none;
        color: lighten(color(primary), 15%);
        transition: color .2s;

        &:hover {
            color: lighten(color(primary), 35%);
        }
    }
}
```

---

![](https://i.imgur.com/dNxmJ8o.gif)

中間針對 input 區域四個框框處理 focus 特效的`not()`只排除 submit 對其他三個處理 border 變色

```sass=

&:focus:not([type="submit"]) {
                border: .1rem solid darken(color(quaternary), 30%);
            }
```

### socialMedia

![](https://i.imgur.com/CwJM2kk.png)

建立一個(index 顏色)的 list 並且把內容使用 each loop 個別迭代進去每一個 social-icon 使用`nth-child()`來選取各個並且元素後個別填入該文字以及邊框顏色

```sass=
$socialMediaColors:1 #3b5998,
2 #b31217,
3 #dc4e41,
4 #55acee,
5 #517fa4,
6 #0077b5;

@each $color in $socialMediaColors {
    .social-icons-item:nth-child(#{nth($color,1)}) .social-icons-link {
        color: nth($color, 2);
        border: .1rem solid nth($color, 2);
    }
}
```

得出這個結果
![](https://i.imgur.com/9VKa9PL.png)

# MAIN.CSS 完整程式碼

[main.css](https://github.com/chiehLiu/git-projects/blob/clothesStore/clothesStore/css/main.css)

小補充:

[grid MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
[grid minmax() MDN](<https://developer.mozilla.org/en-US/docs/Web/CSS/minmax()>)
[grid-column MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-column)
[gap (grid-gap) MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/gap)
[order felx items MDN](https://github.com/chiehLiu/git-projects/blob/clothesStore/clothesStore/index.html)
