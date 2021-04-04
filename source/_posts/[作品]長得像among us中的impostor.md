---
title: 實作練習-長得像among us中的impostor
date:
tags: [HTML, CSS]
category: HTML, CSS 作品
---

# 長得像 among us 中的 impostor 的專案

---

## tags: HTML CSS relate

###### tags: `HTML, CSS`

![](https://i.imgur.com/JFvM6Qd.png)

[作品連結](https://chiehLiu.github.io/git-projects/among/)

專案內容如下:

會利用一大堆的 border-radius 來操作各種圓弧的表面，以及各種定位方式來定位各個部位(腳 背包 眼鏡等等)。

這個網址是 border-radius 各種角度計算，當你拉好形狀之後把數值 Po 回來就可以瞜！

Fancy Border Radius Tool:
https://9elements.github.io/fancy-border-radius/full-control.html

---

**head**

無特別之處

```htmlembedded=
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <title>Among us</title>
</head>
```

---

**body**

html:

用 impostor 包裹住整體，接下來就用部位名稱去命名各個部位

class="body"
class="glass-bowl"
class="legs"

等等

```htmlembedded=
<body>

  <div class="impostor">
    <div class="floor-shadow"></div>
    <div class="backpack">
      <div class="shadow"></div>
    </div>
    <div class="body">
      <div class="fill"></div>
      <div class="shadow"></div>
    </div>
    <div class="glass-bowl">
      <div class="reflection-blue"></div>
      <div class="reflection-white"></div>
    </div>
    <div class="legs">
      <div class="leg-left"></div>
      <div class="leg-right"></div>
    </div>
  </div>


</body>
```

css:

先把整個畫面設置成 flex，並且全部置中滿版

```css=
body {
      /* 這個部分設定之後會讓整個body內的物件完全置中 */
        display: flex;
        align-items: center;
        justify-content: center;
        height: 100vh;
  }
```

這邊是讓各個部位做定位

```css=
.impostor {
        /* 這邊是設定讓body跟一些配件像是背包安全帽
        四肢等等做定位使用 */

    position: relative;
  }
```

這邊處理身體的外框，雛型就出來了~

![](https://i.imgur.com/k861nUq.png)

下圖是還沒有使用 overflow:hideen 前的樣子
![](https://i.imgur.com/yLhrvIX.png)

```css=
.impostor .body {

        position: relative;
        width: 300px;
        height: 420px;
        /* 這個部分是他做出圓弧狀最重要的點 */
        /* 四個數值表示四個角順時針走 從最左上角開始 */
        border-radius: 35% 45% 0 0;
        border: 30px solid #000;
            /* 這邊使用overflow是因為紅色填充物超出外框了讓超出的部分隱藏 */
        overflow: hidden;
  }
```

這邊是要填進去身體的顏色寬度高都 100%因為要填滿身體

```css=
.impostor .fill{
        /* 這邊就會定位在父層也就是 .imposter .body上面 */
        position: absolute;
        width: 100%;
        height: 100%;
        /* 這邊是陰影的顏色 */
        background: #7B0236;
  }
```

這邊填入身體上方比較亮的紅色，因為底部有一小部分是陰影處所以高度使用 90%

下圖綠色框框處

![](https://i.imgur.com/ywemmqs.png)

```css=
.impostor .body .shadow{
        position: absolute;
        width: 100%;
        height: 90%;
        background: #c70a01;
        border-radius: 0% 10% 25% 40% /
        20% 0% 100% 100%;
  }
```

---

開始處理鏡片外框，因為要凸出去身體所以定位的 right 用負數，然後去除一些凸出去的部分一樣使用
overflow:hidden，最後加上一點旋轉。

![](https://i.imgur.com/ON52djQ.png)

```css=
.impostor .glass-bowl{
      position: absolute;
      width: 200px;
      height: 130px;
      background: #4a646d;
      right: -20px;
      top: 90px;
      border: 30px solid #000;
      border-radius: 25% 45% 40% 40% / 50%;
      overflow: hidden;
      /* 讓鏡片旋轉一點點 */
      transform: rotate(-4deg);
}
```

處理鏡片反光部分藍色

```css=
.impostor .glass-bowl .reflection-blue{
      position: absolute;
      right: 0;
      width: 90%;
      height: 70px;
      background:#94c0db;
      border-radius: 10% 10% 100% 100% / 100% 100%
      50% 100%;
}
```

處理鏡片反光部分白色

```css=
.impostor .glass-bowl .reflection-white{
      position: absolute;
      right: 10%;
      top: 10px;
      width: 50%;
      height: 40px;
      background:#fff;
      border-radius: 30% 70% 30% 30% / 30% 70%
      30% 60%;
}
```

---

**legs 的處理**

設定 flex 前的樣子

![](https://i.imgur.com/k5gFwxZ.png)

設定之後的樣子

![](https://i.imgur.com/LvmlSGY.png)

```css=
.legs{
      display: flex;
      /* 這邊最大的範圍就是body所以space between會在兩條腿之間產生一樣的空隙 */
      justify-content: space-between;
      /* 這邊的transform Y的意思是移動Y軸 */
      transform: translateY(-30px );
}
```

左腿的部分比較單純簡單設定長寬，接下來設定外框即可

![](https://i.imgur.com/2W1bwGr.png)

```css=
.impostor .legs .leg-left{
      width: 110px;
      height: 130px;
      background: #7B0236;
      border-left: 30px solid #000;
      border-right: 30px solid #000;
      border-bottom: 30px solid #000;
      border-radius: 0 0 40% 40%;
}
```

右腿比較複雜，因為這邊會跟胯下的陰影處有關聯，不過就多個定位也還好

```css=
.impostor .legs .leg-right{
      /* 這邊是為了定位給胯下處使用當它的父層 */
      position: relative;
      width: 90px;
      height: 105px;
      background: #7B0236;
      border-left: 30px solid #000;
      border-right: 30px solid #000;
      border-bottom: 30px solid #000;
      border-radius: 0 0 40% 40%;
}

        /*胯下陰影處這邊使用偽類做疊層*/

.impostor .legs .leg-right:before{
      content: '';
      position: absolute;
      top: 0;
      left: -50px;
      width: 100px;
      height: 30px;
      background: #000;
      border-radius: 0 0 100% 0;
}

```

---

**backpack 的部分**

一樣有陰影跟亮紅色的部分，並且都是定位在 body 上面

![](https://i.imgur.com/EEZPgpF.png)

```css=
.impostor .backpack{
      position: absolute;
      height: 280px;
      width: 80px;
      background: #c70a01;
      border: 30px solid #000;
      left: -90px;
      top: 130px;
      border-radius: 40% 0 0 40%/ 15%;

}
```

背包陰影處理
很方便直接高度跟寬直接用比例的方式去呈現因為她的 div 父層就是他要蓋過去的地方，
這邊的 overflow:hidden 用來讓稜角變成圓弧
![](https://i.imgur.com/kRR8oyh.png)
![](https://i.imgur.com/vaA6Jdq.png)

```css=
.impostor .backpack .shadow{
      position: absolute;
      width: 100%;
      height: 85%;
      background: #7B0236;
      bottom: 0;
      overflow: hidden;
      border-radius: 40% 0 0 0/ 10% 0 0 0;
}
```

地板處陰影處理一樣定位在身體上面，設定顏色跟圓弧就比較直觀~

```css=
.impostor .floor-shadow{
      position: absolute;
      bottom: 10px;
      left: -15%;
      width: 470px;
      height: 100px;
      background: #535858;
      border-radius: 50%;

}
```
