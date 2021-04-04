---
title: 實作練習-Mars Weather - SASS project
date:
tags: [HTML, CSS, Grid, SASS]
category: HTML, CSS 作品
---

# Mars Weather - SASS project

---

## tags: HTML, CSS, SASS relate

###### tags: `HTML, CSS, SASS`

# 製作一個火星天氣觀測網頁

## 成品:

![](https://i.imgur.com/XEPEoF7.jpg)

[成品網址](https://chiehliu.github.io/git-projects/MarsWeatherApp/index.html)

## 成品功能:

1. cel/fah 的按鈕可以做切換
2. 下方的七天天氣可以點擊按鈕開關

# HTML

## html 程式碼:

# SCSS

## 全域設定

- 全域設定 border-box 這樣做 margin, padding, border 比較方便
- 設定所有的顏色、文字大小以及粗細
- .sr-only 主要給聽障人士使用(這邊用來隱藏元素)
- body, h1, a 都是比較常見的設定

```sass=
*,
*::before,
*::after {
    box-sizing: border-box;
}

:root {
    --fw-light: 300;
    --fw-normal: 400;
    --fw-semi: 500;
    --fw-bold: 700;
    --fs-h1: 1.5rem;
    --fs-h2: 2.25rem;
    --fs-body: 1rem;
    --fs-xl: 4.5rem;
    --clr-light: #fff;
    --clr-gray: #989898;
    --clr-dark: #444;
    --clr-accent: #D06D6D;
    --clr-accent-dark: #613131;
}

.sr-only:not(:focus):not(:active) {
    clip: rect(0 0 0 0);
    clip-path: inset(50%);
    height: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap;
    width: 1px;
}

body {
    margin: 0;
    font-family: 'Montserrat', sans-serif;
    line-height: 1.6;
    background-image: url(https://raw.githubusercontent.com/kevin-powell/Mars-Weather-App/master/img/mars.jpg);
    background-size: cover;
    height: 100vh;
    overflow: hidden;
    color: var(--clr-light);
}

h1,
h2,
h3 {
    line-height: 1;
}

a {
    color: var(--clr-accent);

    &:hover {
        color: var(--clr-accent-dark);
    }
}
```

## .mars-current-weather

![](https://i.imgur.com/gYmJTHU.png)

- 做 grid 以及分三個欄位(等長)等下做使用
- 設定 max-width 避免拉太長跑版
- 背景做透明

```sass=
.mars-current-weather {
    background: rgba(0, 0, 0, .7);
    padding: 2em;
    max-width: 1000px;
    margin: 4em 0 0 4em;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-gap: 2em;
}
```

### .main-title

![](https://i.imgur.com/nX7kr8L.png)

- 抓取 grid 的欄位 1~-1 讓 main-title 可以延續整個面板長度
- 全轉成大寫
- 字母間距 2px(作者喜好)

```sass=
.main-title {
    font-size: var(--fs-h1);
    font-weight: var(--fw-light);
    text-transform: uppercase;
    color: var(--clr-accent);
    letter-spacing: 2px;
    grid-column: 1/-1;
}
```

### .section-title

綠色框框處
![](https://i.imgur.com/lRzFp5Z.png)

```sass=
.section-title {
    font-size: var(--fs-h2);
    font-weight: var(--fw-bold);
    margin: 0;
}
```

讓日期部分最大最顯眼

```sass=
.section-title--date {
    font-size: var(--fs-xl);
}
```

### .reading

綠色框框處
![](https://i.imgur.com/bwK3ooy.png)

```sass=
.reading {
    font-size: var(--fs-h1);
    margin: 0;
    color: var(--clr-gray);
}
```

### .date

內容包含天次以及日期
![](https://i.imgur.com/6swOmfN.png)

整個視窗的抓取位置在第一到第二欄位

```sass=
.date {
    grid-column: 1/2;

    &__day {
        font-size: var(--fs-h2);
        margin: 0;
        color: var(--clr-gray);
        font-weight: var(--fw-light);
    }
}
```

### .temp

![](https://i.imgur.com/1aNYy25.png)

- 抓取位置在第二到第三格
- 處理左右兩邊的格線

```sass=
.temp {

    // 像這邊的var設置在temp裡面所以並不能給外面使用
    --border: solid .25em var(--clr-accent-dark);
    grid-column: 2/3;
    border-left: var(--border);
    border-right: var(--border);
    padding: 0 2em;
}
```

### .wind

![](https://i.imgur.com/KgNXJMV.png)

第二次 grid 為了排列圓盤以及標題風速
![](https://i.imgur.com/TSATGVa.png)

第三次 grid 為了排列指針
![](https://i.imgur.com/OEpfQMh.png)

#### 整個.wind 區塊

- 抓取位置在第三到第四格
- 在進行第二次 gird 為了讓內容物作排列

#### 圓盤區域

- 進行第三次 grid 為了排列裡面的指針並且使用`place-items: center;`全置中
- 圓盤的部份跨越了兩個 row 所以使用`grid-row: 1/span 2;`

#### 指針區域

- 指針的部份使用 clip-path: polygon 裁剪出三角形
- 使用 transform 做好定位並且指向 0 度的方向
- transform-origin 讓三角形的旋轉是以底部的中心點轉才不會偏調

```sass=
.wind {
    grid-column: 3/4;
    display: grid;
    grid-template-columns: repeat(2, 1fr);

    // 這一步是為了讓Wind標題與風速之間的間距縮小讓行距大小跟內容一樣
    grid-template-rows: min-content 1fr;

    //往上對齊
    align-self: start;

    //幫它們做好排列位置
    .section-title,
    .reading {
        grid-column: 2/3;
    }

    //圓圈的部分修飾
    &__direction {
        --size: 6rem;
        width: var(--size);
        height: var(--size);
        background-color: rgba(255, 255, 255, .5);
        border-radius: 50%;
        display: grid;
        place-items: center;
        grid-row: 1/span 2;
    }

    &__arrow {
        --direction: 0deg;
        --size: 1rem;
        height: calc(var(--size)*3);
        width: var(--size);
        background: var(--clr-accent-dark);
        clip-path: polygon(50% 0, 0% 100%, 100% 100%);
        transform: translateY(-50%) rotate(var(--direction));
        transform-origin: bottom center;
    }
}
```

### .info

![](https://i.imgur.com/2BG9XHx.png)

- 抓取位置

```sass=
.info {
    grid-column: 1/3;
}
```

### .unit

可調整式按鈕藉由 SCSS 全部製作出來!
![](https://i.imgur.com/s3HT8kN.png)

#### 整個外框

![](https://i.imgur.com/TEn4KgA.png)

- 先放置到位置`grid-column: 3/4;`
- 使用 place-self:end 會把物件放到最右邊最下方
- 要把 unit 內部元素弄成一橫排直接 flex
- 做一點透明度以及 hover 時會有特效

#### input 區域的 checkbox

隱藏前的樣子
![](https://i.imgur.com/DMfjeRx.png)

- 引入的 sr-only 的內容隱藏 checkbox

#### unit\_\_toggle

- 中間的橢圓形外框修飾

#### unit\_\_toggle::after

- 中間的圓球的部分點擊兩側的溫度則會移動，左側自動填滿 margin 所以球會移動到最右邊
- ![](https://i.imgur.com/8FZWj2V.png) 因為這個 checked 關係球會預設在 °C
- 使用`margin-left:auto;`會讓球往右邊跑因為左邊 auto 直接填滿
- 使用`margin-left: 3px;`會讓球回到左側因為 3px 就是原本預設的 margin

偽類選擇器`:checked`只會使用在任何選中狀態下的`radio(<input type="radio">)，checkbox (<input type="checkbox">) 或("select") `元素中的 option HTML 元素("option")。

```sass=
:checked~.unit__toggle::after {
        margin-left: 3px;
    }
```

```sass=
.unit {
    grid-column: 3/4;

    // place-self是align-self and justify-self的縮寫
    // 使用end會把物件放到最右邊最下方
    place-self: end;
    color: var(--clr-light);
    display: flex;
    opacity: .7;
    transition: opacity 275ms linear;

    &:hover {
        opacity: 1;
    }

    label {
        cursor: pointer;
    }

    // 要隱藏input區域那個圓形checkbox
    // 一樣使用sr-only的屬性貼在這邊使用
    input {
        clip: rect(0 0 0 0);
        // 這個clip-path主要會把input的checkbox裁減掉
        clip-path: inset(50%);
        height: 1px;
        overflow: hidden;
        position: absolute;
        white-space: nowrap;
        width: 1px;
    }

    // 中間按鈕的部分修飾
    &__toggle {
        cursor: pointer;
        width: 4em;
        border: 2px solid var(--clr-light);
        background: transparent;
        padding: 0;
        // vmax = vh,vw的最大值
        border-radius: 100vmax;
        margin: 0 1em;

        // 中間圓點修飾
        &::after {
            content: '';
            display: block;
            background: var(--clr-light);
            border-radius: 50%;
            height: 1rem;
            margin: 3px;
            width: 1rem;
            // 左側自動填滿margin所以球會移動到最右邊
            margin-left: auto;
        }
    }

    // 偽類選擇器:checked只會使用在任何選中狀態下的radio(<input type="radio">)，checkbox (<input type="checkbox">) 或("select") 元素中的option HTML元素("option")。
    // 當選中checked時則底下的after修飾也就是圓點的部分會移動回左邊只有margin:3px的狀態
    :checked~.unit__toggle::after {
        margin-left: 3px;
    }
}
```

## .previous-weather

![](https://i.imgur.com/7cAFRnC.png)

- 把整個區塊往下拉
- 下拉做動畫`transition: transform 350ms ease;`

### .previous-weather

```sass=
.previous-weather {
    background: var(--clr-light);
    color: var(--clr-dark);
    position: absolute;
    bottom: 0;
    width: 100%;

    // 把previous-weather欄位往下60%
    transform: translateY(60%);
    transition: transform 350ms ease;
    padding: 3em;
}
```

### .show-previous-weather

![](https://i.imgur.com/3KYFK2x.png)

- 設定定位上面`transform: translate(-50%, calc(-100% - 3rem));`因為整個 previou-weather 視窗 padding 是 3rem 這邊必須扣掉不然會超出去
- line-height 跟其他地方一樣都設定 1
- clip-path: polygon 一樣使用裁減功能成三角形
- 特別的地方是 font-family 必須使用繼承 inherit 才吃的到

#### .span

- span 的部份做箭頭旋轉特效但這邊還沒轉顯示正常的 0 度

```sass=
.show-previous-weather {
    cursor: pointer;
    position: absolute;
    background: var(--clr-light);
    left: 50%;
    width: 10rem;

    // 這邊因為在previous-weather上加入padding會使箭頭區域跑掉所以加上clac而外加上3rem來確保位置不會跑掉
    transform: translate(-50%, calc(-100% - 3rem));
    text-align: center;
    font-size: var(--fs-h2);
    line-height: 1;
    clip-path: polygon(50% 0, 0 100%, 100% 100%);
    color: var(--clr-gray);
    border: 0;
    font-family: inherit;

    &:hover,
    &:focus {
        color: var(--clr-dark);
    }

    span {
        display: block;
        transform: rotate(0);
        transition: transform 300ms ease;
    }
}
```

### .previous-days, .previous-weather\_\_title, .previous-day

下方的整區
![](https://i.imgur.com/s2nuu2M.png)

- flex 直接讓他們成行排列並且 space-between 讓中間空隙一樣
- title 置中
- 針對文字，按鈕做修飾

```sass=
.previous-days {
    display: flex;
    justify-content: space-between;
}

.previous-weather__title {
    text-align: center;
}

.previous-day {
    opacity: 0;

    &>* {
        margin: 0;
    }

    &__date {
        font-size: .9rem;
        color: var(--clr-gray);
    }

    &__more-info {
        border: 0;
        border-radius: 100vmax;
        background: var(--clr-dark);
        color: var(--clr-light);
        text-transform: uppercase;
        padding: .3em 1em;
        cursor: pointer;
        margin-top: 1em;

        &:hover {
            background: var(--clr-gray)
        }
    }
}
```

### .show-weather.previous-weather

這邊針對加上.show-weather 的.previous-weather 做處理也就是整個視窗移上來的時候

#### span

- 當視窗移動上來的時候 span 裡面的箭頭會轉 180 度
- Y 軸也要調整不然會跑版

#### .previous-weather\_\_title, .previous-day

- 做透明變成不透明特效並且製作 slideUpIn 特效
- 使用 forwards 讓特效結束後停在原地不繼續執行
- 把標題移動到左邊

#### 使用@each

- 個別印出不同的 delay 時間做出這個特效

![](https://i.imgur.com/oUpYZDj.gif)

- 使用 sass list 建立包含(index delay 時間)
- 使用 each 個別印出 list 內部所有元素
- 使用#{}選取動態的變數丟入 nth-child()內
- 使用 nth()選取 list 內部的第一位以及第二位分別貼上 nth-child,animation-delay

```sass=
$slidTime: 1 100ms,
    2 125ms,
    3 150ms,
    4 175ms,
    5 200ms,
    6 225ms,
    7 250ms;

    @each $slide in $slidTime {
        .previous-day:nth-child(#{nth($slide,1)}) {
            animation-delay: #{nth($slide,2)};
        }
    }
```

#### @keyframes

- 設定透明以及標題移動特效

```sass=
.show-weather.previous-weather {
    transform: translateY(0);

    .show-previous-weather span {
        display: block;
        transform: rotate(180deg) translateY(-6px);
    }

    .previous-weather__title,
    .previous-day {
        opacity: 1;
        animation: slideUpIn 750ms forwards;
    }

    .previous-weather__title {
        text-align: left;
    }

    // 讓previous-day的資料有一個一個上來的特效
    $slidTime: 1 100ms,
    2 125ms,
    3 150ms,
    4 175ms,
    5 200ms,
    6 225ms,
    7 250ms;

    @each $slide in $slidTime {
        .previous-day:nth-child(#{nth($slide,1)}) {
            animation-delay: #{nth($slide,2)};
        }
    }
}

@keyframes slideUpIn {
    0% {
        opacity: 0;
        transform: translateY(50%);
    }

    100% {
        opacity: 1;
        transform: translateY(0%);
    }
}
```
