---
title: 實作練習-Restaurant Georgia - SASS project
date:
tags: [HTML, CSS, Flex, SASS]
category: HTML, CSS 作品
---

# Restaurant Georgia - SASS project

---

## tags: HTML, CSS, SASS relate

###### tags: `HTML, CSS, SASS`

# 製作一個餐廳網頁

## 成品:

![](https://i.imgur.com/2i5AGrw.jpg)

[成品網址](https://chiehliu.github.io/git-projects/restaurantGeorgia/index.html)

## 成品功能:

1.總共有五個區塊 navbar 區/ brand logo 區/ 食物照片區/ footer 區/ 漢堡選單區 2.點選漢堡可以到 navbar 區並且字樣有動畫 3.食物照片區滑過會顯示字樣/ 按鈕
4.footer 區域顯示 社群 icon 滑過會變色 5.所有按鈕都有 hover 過去變色

# HTML

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="css/main.css" />
    <link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.5.0/css/all.css"
        integrity="sha384-B4dIYHKNBt8Bc12p+WXckhzcICo0wtJAoU8YZTY5qE0Id1GSseTk6S+L3BlXeVIU" crossorigin="anonymous" />
    <link
        href="https://fonts.googleapis.com/css?family=Dancing+Script:400,700|Josefin+Sans:300,400,600,700|Nunito:300,400,600,700"
        rel="stylesheet" />
    <title>Restaurant Georgia</title>
</head>

<body>
    <!--Navbar-->
    <nav class="navbar">

        <!-- 這邊的for:check屬性讓他們可以做點擊時產生效果-->
        <!-- html的屬性hidden可以讓input看不見 -->
        <input type="checkbox" id="check" class="checkbox" hidden />
        <div class="hamburger-menu">
            <label for="check" class="menu">
                <div class="menu-line menu-line-1"></div>
                <div class="menu-line menu-line-2"></div>
                <div class="menu-line menu-line-3"></div>
            </label>
        </div>

        <div class="navbar-navigation">
            <div class="navbar-navigation-left">
                <img src="images/nav-img-1.jpeg" class="left-img left-img-1" />
                <img src="images/nav-img-2.jpeg" class="left-img left-img-2" />
                <img src="images/nav-img-3.jpeg" class="left-img left-img-3" />
            </div>

            <div class="navbar-navigation-right">
                <ul class="nav-list">
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">Home</a>
                    </li>
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">About Us</a>
                    </li>
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">Gallery</a>
                    </li>
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">Reservation</a>
                    </li>
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">Services</a>
                    </li>
                    <li class="nav-list-item">
                        <a href="#" class="nav-list-link">Contact</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
    <!--End of Navbar-->

    <!--Header-->
    <header class="header">
        <div class="brand">
            <a href="#" class="logo"><i class="fas fa-utensils"></i></a>
            <div>
                <h1 class="main-name">Georgia</h1>
                <p class="sub-name">Restaurant</p>
            </div>
        </div>

        <div class="header-banner">
            <h1 class="main-heading">Welcome</h1>
            <h3 class="sub-heading">Try Great Georgian Dishes</h3>
            <button type="button" class="main-btn">Reservation</button>
        </div>
    </header>
    <!--End of Header-->

    <!-- about us -->
    <section class="about-us">
        <div class="about-us-left">
            <img src="images/about-us-img.png" />
        </div>

        <div class="about-us-right">
            <h1 class="main-heading">About</h1>
            <h3 class="sub-heading">Introduce to Georgia Dishes</h3>
            <div class="stars">
                <i class="fa fa-star-of-life star"></i>
                <i class="fa fa-star-of-life star"></i>
                <i class="fa fa-star-of-life star"></i>
            </div>
            <p class="descriptions">
                Lorem ipsum dolor sit amet consectetur adipisicing elit. Sit tenetur
                minima, ratione iste eveniet earum molestias non, expedita esse
                quaerat, enim corporis mollitia. Totam molestiae atque maiores aliquam
                culpa, cum illo nemo enim eum nobis ipsa aliquid harum architecto aut.
                Molestiae optio reiciendis obcaecati minus minima facilis fugiat
                consectetur amet!
            </p>
            <div class="stars">
                <i class="fa fa-star-of-life star"></i>
                <i class="fa fa-star-of-life star"></i>
                <i class="fa fa-star-of-life star"></i>
            </div>
            <button type="button" class="main-btn">Read MORE</button>
        </div>
    </section>
    <!-- end of about us -->

    <!--Gallery-->
    <section class="gallery">
        <div class="cards-wrapper">
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-1.jpeg" class="card-img" />
            </div>
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-2.jpeg" class="card-img" />
            </div>
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-3.jpeg" class="card-img" />
            </div>
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-4.jpeg" class="card-img" />
            </div>
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-5.jpeg" class="card-img" />
            </div>
            <div class="card">
                <div class="card-overlay">
                    <h1 class="card-overlay-heading">Food Name</h1>
                    <p class="card-overlay-paragraph">Price: $30.00</p>
                    <button type="button" class="card-overlay-btn">Order Now</button>
                </div>
                <img src="images/gallery-img-6.jpeg" class="card-img" />
            </div>
        </div>
    </section>
    <!--End of Gallery-->

    <!-- Footer -->
    <footer class="footer">
        <div class="footer-header">
            <a href="#" class="logo"><i class="fas fa-utensils"></i></a>
            <div>
                <h1 class="main-name">Georgia</h1>
                <p class="sub-name">Restaurant</p>
            </div>
        </div>
        <div class="footer-social-media">
            <ul class="social-media">
                <li class="social-media-item">
                    <a href="#" class="social-media-link">
                        <i class="fab fa-facebook-square"></i>
                    </a>
                </li>
                <li class="social-media-item">
                    <a href="#" class="social-media-link">
                        <i class="fab fa-instagram"></i>
                    </a>
                </li>
                <li class="social-media-item">
                    <a href="#" class="social-media-link">
                        <i class="fab fa-google-plus-square"></i>
                    </a>
                </li>
                <li class="social-media-item">
                    <a href="#" class="social-media-link">
                        <i class="fab fa-youtube"></i>
                    </a>
                </li>
            </ul>
        </div>
        <div class="footer-copyright">
            <p class="footer-copyright-paragragh">
                &copy; Copyright. Restaurant "Georgia". All Rights Reserved
            </p>
        </div>
    </footer>
    <!-- End of Footer -->

</body>

</html>
```

# SCSS:

- main.scss

主要引入三個部分近來讓分工變細

- \_base.scss

把以下元素放在這邊區隔開來
顏色元素/ 字型/ @include/ @mixin / %(spaceholder)/ 全域設定

**@mixin**

1. flexLayout

```sass=
flexLayout {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

設置 flex 並且上下左右置中 3. textStyles

```sass=
textStyles ($transform: uppercase) {
    font-weight: 300;
    letter-spacing: 2px;
    text-transform: $transform;
}
```

預設參數 把字母改成大寫/主要處理在 footer, navbar, main/sub name, heading 的文字 3. centering($topValue)

```sass=
centering($topValue) {
    position: absolute;
    top: $topValue;
    left: 50%;
    transform: translate(-50%, -50%);
}
```

主要設置絕對定位以及全置中使用`transform: translate(-50%, -50%);`並且參數可以輸入跟頂端的距離，主要使用置中 header 的位置

**@extend**
%fullSpace

```sass=
%fullSpace {
    width: 100%;
    height: 100%;
}
```

使用在食物圖片區 card 的部份讓文字/圖片區塊佔滿以及漢堡區域讓線條滿版

- \_components.scss

主要處理 layout 上層的東西例如: logo/h1/p/img 等等

---

## \_components.scss 值得學習的點

`transform-origin` 這個屬性可以改變旋轉的圓心的位置也是做出 navbar 區 X 的關鍵

[`transform-origin` MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/transform-origin)

```sass=
menu-line {
            width: 100%;
            height: 4px;
            background-color: $color-primary;

            // 改變旋轉的圓心讓兩條直線變成交叉形成X
            // 這邊設計右邊也就是直線的底端固定並且作旋轉
            transform-origin: right;
            transition: all .5s .5s;
            }
```

---

這邊的 logo 部分有一些小角出現在 Logo 附近，其實是底線使用`text-decoration: none;`消除
![](https://i.imgur.com/l6gKvOG.png)

並且因為 logo 內部的 a tag 內建是 inline 屬性無法使用 width,height 所以需要轉換成 block 屬性，且因為 logo 置中的問題轉使用 flex

```sass=
.logo {
    font-size: 70px;
    color: $color-primary;
    width: 110px;
    height: 110px;
    border: 3px solid $color-primary;
    border-radius: 50%;
    margin-right: 20px;

    // 去掉logo左側的一個底線露出來一點點的部分
    text-decoration: none;

    // 這邊因為a tag內建是inline 屬性無法使用width,height所以需要轉換成block屬性，且因為logo置中的問題轉使用flex
    @include flexLayout;
    }
```

---

`object-fit`可以讓圖片顯示最不失真

[`object-fit` MDN](https://developer.mozilla.org/zh-TW/docs/Web/CSS/object-fit)

```sass=
card-img {
        @extend %fullSpace;

        // 這個屬性可以讓圖片看起來不會失去比較
        object-fit: cover;
        opacity: .5;
    }
```

- \_layout.scss

這部分主要處理整體框架的設置基本上會跟 component 一起處理畫面

## \_layout.scss 值得學習的點

`cubic-bezier`由四個點來決定動畫的速度曲線(可以用到 trasition, transform 裡面)

[`cubic-bezier` W3cschool](https://www.w3schools.com/cssref/func_cubic-bezier.asp)

```sass=
navbar-navigation-left {
            width: 50vw;
            height: 100vh;
            background-color: $color-dark;
            position: fixed;
            left: -50vw;
            transition: left .8s cubic-bezier(1, 0, 0, 1);}
```

使用 :checked 偽類 來基於 input checkbox 的狀態來判斷是否切換狀態而不需要使用 JS

[:checked 偽類 MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/:checked)

```sass=
.checkbox:checked~.navbar-navigation .navbar-navigation-left {
    left: 0;
}
```

---

`flex-wrap: wrap;` 讓 card 圖片的部分變成分行(因為 width 部分已經設定過所以分成兩行)
[`flex-wrap: wrap` MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/flex-wrap)

```sass=
.gallery {
    .cards-wrapper {
        display: flex;

        // 這邊使用wrap讓card的部分變成兩行
        flex-wrap: wrap;
    }
}
```

## SCSS 完整程式碼

main.scss

```sass=
@import "base";
@import "layout";
@import "components";
```

\_base.scss

```sass=
$color-dark:#262626;
$color-black:#000;
$color-primary:#d3ab55;
$color-secondary:#bbb;
$color-white:#fff;

$font-dancingScript: 'Dancing Script',
cursive;
$font-josefinSans: 'Josefin Sans',
sans-serif;
$font-nunito: 'Nunito',
sans-serif;

@mixin flexLayout {
    display: flex;
    justify-content: center;
    align-items: center;
}

@mixin textStyles ($transform: uppercase) {
    font-weight: 300;
    letter-spacing: 2px;
    text-transform: $transform;
}

@mixin centering($topValue) {
    position: absolute;
    top: $topValue;
    left: 50%;
    transform: translate(-50%, -50%);
}


%fullSpace {
    width: 100%;
    height: 100%;
}


* {
    margin: 0;
    padding: 0;
}

body {
    background-color: $color-dark;
}
```

\_component.scss

```sass=
$color-dark:#262626;
$color-black:#000;
$color-primary:#d3ab55;
$color-secondary:#bbb;
$color-white:#fff;

$font-dancingScript: 'Dancing Script',
cursive;
$font-josefinSans: 'Josefin Sans',
sans-serif;
$font-nunito: 'Nunito',
sans-serif;

@mixin flexLayout {
    display: flex;
    justify-content: center;
    align-items: center;
}

@mixin textStyles ($transform: uppercase) {
    font-weight: 300;
    letter-spacing: 2px;
    text-transform: $transform;
}

@mixin centering($topValue) {
    position: absolute;
    top: $topValue;
    left: 50%;
    transform: translate(-50%, -50%);
}


%fullSpace {
    width: 100%;
    height: 100%;
}


* {
    margin: 0;
    padding: 0;
}

body {
    background-color: $color-dark;
}
```

\_layout.scss

```sass=
.navbar {
    position: relative;
    z-index: 200;

    &-navigation {
        display: flex;

        &-left {
            width: 50vw;
            height: 100vh;
            background-color: $color-dark;
            position: fixed;
            left: -50vw;
            transition: left .8s cubic-bezier(1, 0, 0, 1);

            @media (max-width:800px) {
                display: none;
            }

            .left-img {
                width: 50%;
                position: absolute;

                @media (max-width:1300px) {
                    width: 55%;
                }

                @media (max-width:1000px) {
                    width: 65%;
                }
            }

            // 這邊利用定位%數不一樣的方式排列出傾斜的樣式
            .left-img-1 {
                top: 15%;
                left: 15%;
                box-shadow: 0 15px 60px rgba($color-black, .4);
                opacity: 0.7;
                border-radius: 10px;

                @media (max-width:1000px) {
                    left: 5%;
                }
            }

            .left-img-2 {
                top: 35%;
                left: 25%;
                box-shadow: 0 15px 60px rgba($color-black, .4);
                opacity: 0.7;
                border-radius: 10px;

                @media (max-width:1000px) {
                    left: 15%;
                }
            }

            .left-img-3 {
                top: 55%;
                left: 35%;
                box-shadow: 0 15px 60px rgba($color-black, .4);
                opacity: 0.7;
                border-radius: 10px;

                @media (max-width:1000px) {
                    left: 25%;
                }
            }
        }

        &-right {
            width: 50vw;
            height: 100vh;
            background-color: #1f1d1d;
            position: fixed;
            right: -50vw;
            @include flexLayout;
            transition: right .8s cubic-bezier(1, 0, 0, 1);

            @media (max-width:800px) {
                width: 100vw;
                right: -100vw;
            }
        }

        .nav-list {
            &-item {
                list-style: none;
            }

            // letter-spacing+transition放慢可以做出QQ的文字特效

            &-link {
                font-family: $font-dancingScript;
                font-size: 50px;
                @include textStyles(capitalize);
                color: $color-secondary;
                text-decoration: none;
                display: block;
                margin: 20px;
                text-align: center;
                transition: all .5s;

                &:hover {
                    color: $color-primary;
                    letter-spacing: 4px;
                }

                @media (max-width:600px) {
                    font-size: 40px;
                }
            }
        }
    }
}

.checkbox:checked~.navbar-navigation .navbar-navigation-left {
    left: 0;
}

.checkbox:checked~.navbar-navigation .navbar-navigation-right {
    right: 0;
}

// 這部分修飾讓menu按鈕旋轉後變更圖示變成X
.checkbox:checked~.hamburger-menu .menu {
    transform: rotateZ(90deg);
}

.checkbox:checked~.hamburger-menu .menu-line-1 {
    transform: rotateZ(-40deg);
}

.checkbox:checked~.hamburger-menu .menu-line-2 {
    opacity: 0;
}

.checkbox:checked~.hamburger-menu .menu-line-3 {
    transform: rotateZ(40deg);
}

.header {
    width: 100%;
    height: 100vh;
    position: relative;
    background: linear-gradient(rgba($color-black, .8), rgba($color-black, .6)), url(/images/bg.jpeg) center no-repeat;
    background-size: cover;

    .brand {

        display: flex;
        align-items: center;
        @include centering(15%);

        @media (max-width:500px) {
            @include centering(12%);
        }
    }

    &-banner {
        text-align: center;
        @include centering(50%);
    }
}

.about-us {
    height: 90vh;
    display: flex;
    align-items: center;

    @media (max-width:900px) {
        height: 70vh;
    }

    &-left {
        width: 40%;
        position: relative;
        left: -200px;

        @media(max-width: 1300px) {
            left: -150px;
        }

        @media (max-width:800px) {
            display: none;
        }

        img {
            width: 100%;
            opacity: .7;
        }
    }

    &-right {
        width: 60%;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding: 0 100px;
        box-sizing: border-box;

        @media(max-width: 1300px) {
            padding: 0 50px;
        }

        @media (max-width:800px) {
            width: 100%;
        }

        .stars {
            margin: 30px 0;

            @media (max-width:1000px) {
                margin: 15px 0;
            }
        }

        .star {
            font-size: 15px;
            color: $color-primary;
            margin-left: 10px;

            @media (max-width:1000px) {
                font-size: 12px;

            }
        }

        .descriptions {
            font-family: $font-josefinSans;
            font-size: 25px;
            font-style: italic;
            color: $color-secondary;
            text-align: justify;

            &::first-letter {
                padding-left: 50px;
            }

            @media (max-width: 1600px) {
                font-size: 18px;
            }

            @media (max-width:1000px) {
                font-size: 14px;

            }

            @media (max-width:500px) {
                font-size: 12px;
            }
        }
    }
}

.gallery {
    .cards-wrapper {
        display: flex;

        // 這邊使用wrap讓card的部分變成兩行
        flex-wrap: wrap;
    }
}

.footer {
    padding: 70px 0;
    @include flexLayout;
    flex-direction: column;

    @media (max-width:500px) {
        padding: 40px 0;
    }

    &-header {
        display: flex;
        align-items: center;
        margin-bottom: 70px;
    }

    .social-media {
        display: flex;
        width: 300px;
        justify-content: space-between;
        margin-bottom: 70px;

        @media (max-width:500px) {
            width: 200px;
            margin-bottom: 40px;
        }

        &-item {
            list-style: none;
        }

        &-link {
            text-decoration: none;
            font-size: 50px;
            color: $color-secondary;
            transition: color .7s;

            &:hover {
                color: $color-primary;
            }

            @media (max-width:1000px) {
                font-size: 35px;
            }

            @media (max-width:500px) {
                font-size: 25px;
            }
        }
    }

    &-copyright-paragragh {
        font-family: $font-josefinSans;
        font-size: 18px;
        color: $color-secondary;
        text-align: center;
        @include textStyles(capitalize);

        @media (max-width:800px) {
            width: 70%;
            margin: auto;
        }

        @media (max-width:500px) {
            font-size: 14px;
        }
    }
}
```
