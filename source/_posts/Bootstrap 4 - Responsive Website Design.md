---
title: Bootstrap 4-Responsive Website Design
date:
tags: Bootstrap
category: Bootstrap
---

# Bootstrap 4 - Responsive Website Design

---
tags: HTML CSS Bootstrap relate
---

###### tags: `HTML, CSS, Bootstrap`


# 製作一個 使用Bootstrap的網站

## 成品:

![](https://i.imgur.com/8X5zcSP.png)


[成品網址](https://chiehliu.github.io/git-projects/Bootstrap%202020%20Starter%20Files/index.html)

## 成品功能:

1. 點擊漢堡會有下拉是選單跳出(並且可以開關)
2. 中間有大圖呈現slide 效果並且點擊或是等待都可以讓slide移動
3. 呈現一個三欄位/兩欄位的文章區塊
4. 中間有圖片固定的區域並且點擊按鈕會有跳出視窗
5. 插頭符號也可以跳出區塊顯示圖片
6. jumbotron 區域展示顏色變化以及一段文字及按鈕
7. 最後是footer區域顯示social icon

# 介紹使用到的Bootstrap 4 元素

## margin, padding

範例

使用 mr-lg-3
代表margin-right: 1rem並且breakpoint在lg

![](https://i.imgur.com/KgbVswT.png)



## Navigation 區域

* container
這邊使用的是預設的版本，所有會有四個breadkpoint(觸發RWD的點)，並且置中

* col-12
使用的是bootstrap內部的gird系統，主要分為12格，這邊這樣使用會有滿版的效果

* text-right
讓文字往右，其中也有搭配RWD的作法，ex.使用text-lg-right 可以讓文字在lg的breadkpoint時取消文字定位

* navbar
使用navbar系列的功能必須先使用這個關鍵字包覆住

* bg-light
讓背景呈現淺色

* navbar-light
讓文字配合淺色背景

* navbar-expand-lg
讓navbar RWD的關鍵，不使用的話會預設滿版

* navbar-brand
使用在公司名稱的部分或是logo


* 下拉式選單標準作法
button是漢堡的部分
collapse navbar-collapse的部分是會被隱藏的選單部分

![](https://i.imgur.com/BAAEHJn.png)


```htmlembedded=
<button class="navbar-toggler">
        
        <span class="navbar-toggler-icon" type="button" data-toggle="collapse" data-target="#navbarResponsive"></span>
</button>

<div class="collapse navbar-collapse" id="navbarResponsive">
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
```

* ml-auto
使物件靠右

* nav-item nav-link
在navbar中的物件使用


### 使用到的CSS

為了要蓋掉bootstrap原生的顏色要使用 `!important`

```css=
.nav-link {
  /* 加上驚嘆號去取代bootstrap內建的顏色 */
  color: #5b5555 !important;
}

.nav-link.active,
.nav-link:hover {
  color: #4981b3 !important;
}
```

## Carousel 區域

* 必須安裝 util.js. 這包boostrap的內容才可以使用

使用範例

data-interval的部分是 換張投影片的間隔時間(ms毫秒)
```htmlembedded=
<div id="carousel" class="carousel slide" data-ride="carousel" data-interval="6500">
```

* carousel-inner
針對投影片區域的圖片區域做包裹的動作

* carousel-item
主要放在carousel-inner裡面，內部設置投影片的內容(圖片文字等等)，並且有active的item為預設值

* carousel-caption
使用在幻燈片如果需要標題時可以嵌入

* carousel-control-prev(next)
選取#carousel後嵌入範例即可使用
上一張/下一張 功能並且搭配fontawesome的箭頭作範例

```htmlembedded=
<a href="#carousel" class="carousel-control-prev" role="button" data-slide="prev">
      <span class="fas fa-chevron-left fa-2x"></span>
</a>
```

## Emoji Navbar 區域

這兩個區域點擊會觸發下面四個圖片的縮放

![](https://i.imgur.com/DKVx8Sa.png)

![](https://i.imgur.com/48hoY2E.png)

主要使用了

* a tag的部分
href部分抓取#emoji也就是要出現部分的id，並且使用`data-toggle="collapse"`

* 下方圖片toggle處 使用 class = collapse 以及設置id = emoji

這部分比較特別的地方是插頭的部分在css選取器上，比較特別要去google inspect裡面看才知道


## fixed img 內部的跳出視窗功能

點擊下方藍色跟紅色按鈕會出現的圖片
![](https://i.imgur.com/eaIbItx.png)

使用modal做到跳出視窗的效果
* 針對按鈕的部分加入
`data-toggle="modal" data-target="#modal1"`

* 跳出圖片的部分
設置被抓取的`id = modal1`
並在內容處設置 `modal-dialog`


## Jumbotron 區域

一個簡單並且滿版的區域並且對內部文字按鈕有基本裝飾跟定位

* Jumbotron

![](https://i.imgur.com/14tTA2B.png)


# html程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta
      name="viewport"
      content="width=device-width, initial-scale=1.0, viewport-fit=cover"
    />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>HTML5 Website with Bootstrap | Responsive Website Design</title>
    <link rel="shortcut icon" href="img/favicon.ico" />
    <!-- Bootstrap 4.5 CSS -->
    <link rel="stylesheet" href="css/bootstrap.min.css" />
    <!-- Style CSS -->
    <link rel="stylesheet" href="css/style.css" />
    <!-- Google Fonts -->
    <link
      href="https://fonts.googleapis.com/css?family=Montserrat:300,400,500,600,700&display=swap"
      rel="stylesheet"
    />
  </head>

  <body>
    <!-- Top Bar -->
    <div class="top-bar">
      <div class="container">
        <!-- 這邊col-12代表延續整個頁面 -->
        <div class="col-12 text-right">
          <!-- 因為bootstrap的關係 a 的文字會直接顯示藍色 -->
          <p><a href="tel:+999123888"> Call us at 1 (800) HTML - CSS</a></p>
        </div>
      </div>
    </div>
    <!-- End Top Bar -->

    <!-- Navigation -->
    <nav class="navbar bg-light navbar-light navbar-expand-large">
      <div class="container">
        <a href="index.html" class="navbar-brand"
          ><img src="img/logo.png" alt="logo" title="logo"
        /></a>
        <button class="navbar-toggler">
          <!-- 加入bootstarp js library讓漢堡選單可以使用 -->
          <span
            class="navbar-toggler-icon"
            type="button"
            data-toggle="collapse"
            data-target="#navbarResponsive"
          ></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarResponsive">
          <ul class="navbar-nav ml-auto">
            <li class="nav-item">
              <a href="index.html" class="nav-link active">Home</a>
            </li>
            <li class="nav-item"><a href="" class="nav-link">About</a></li>
            <li class="nav-item"><a href="" class="nav-link">Services</a></li>
            <li class="nav-item"><a href="" class="nav-link">Projects</a></li>
            <li class="nav-item"><a href="" class="nav-link">Contact Us</a></li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- End Navigation -->

    <!-- Image Carousel -->
    <!-- 加入bootstarp js library讓slide可以動 -->
    <div
      id="carousel"
      class="carousel slide"
      data-ride="carousel"
      data-interval="6500"
    >
      <!-- Carousel Content -->
      <div class="carousel-inner">
        <div class="carousel-item active">
          <!-- 這邊使用w-100會讓圖片吃到其父母層的100%寬度 -->
          <img src="img/carousel/1.jpg" alt="" class="w-100" />
          <div class="carousel-caption">
            <div class="container">
              <div class="row justify-content-center">
                <div class="col-8 bg-custom d-none d-md-block py-3 px-0">
                  <h1>Bootstrap</h1>
                  <div class="border-top border-primay w-50 mx-auto my-3"></div>
                  <h3 class="pb-3">Complete Website Design</h3>
                  <a href="#" class="btn btn-danger btn-lg mr-2">View Demo</a>
                  <a href="#" class="btn btn-primary btn-lg ml-2">Start Now</a>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="carousel-item">
          <img src="img/carousel/2.jpg" alt="" class="w-100" />
          <div class="carousel-caption">
            <div class="container">
              <div class="row justify-content-end text-right">
                <div class="col-5 bg-custom d-none d-lg-block py-3 px-0 pr-3">
                  <!-- lead會使用font-weight=300 -->
                  <p class="lead pb-3">
                    Lorem ipsum dolor sit amet consectetur.
                  </p>
                  <a href="#" class="btn btn-danger btn-lg mr-2">See PHone</a>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="carousel-item">
          <img src="img/carousel/3.jpg" alt="" class="w-100" />
          <div class="carousel-caption">
            <div class="container">
              <div class="row justify-content-center text-left">
                <div class="col-7 bg-custom d-none d-lg-block py-3 px-0 pl-3">
                  <h3 class="pb-3">Lorem, ipsum dolor.</h3>
                  <p class="lead">
                    Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                  </p>
                  <a href="#" class="btn btn-primary btn-lg ml-2">Start Now</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- End Carousel Content -->

      <!-- Previous & Next Buttons -->
      <a
        href="#carousel"
        class="carousel-control-prev"
        role="button"
        data-slide="prev"
      >
        <span class="fas fa-chevron-left fa-2x"></span>
      </a>

      <a
        href="#carousel"
        class="carousel-control-next"
        role="button"
        data-slide="next"
      >
        <span class="fas fa-chevron-right fa-2x"></span>
      </a>
      <!-- End Previous & Next Buttons -->
    </div>
    <!-- End Image Carousel -->

    <!-- Main Page Heading -->
    <div class="col-12 text-center mt-5">
      <h1 class="text-dark pt-4">Built With Ease</h1>
      <div class="border-top border-primay w-25 mx-auto my-3"></div>
      <p class="lead">Lorem ipsum, dolor sit amet consectetur adipisicing.</p>
    </div>

    <!-- Three Column Section -->
    <div class="container">
      <div class="row my-5">
        <div class="col-md-4 my-4">
          <img src="img/1.jpg" alt="" class="w-100" />
          <h4 class="my-4">Lorem, ipsum.</h4>
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit.
            Aspernatur, iure!
          </p>

          <a href="#" class="btn btn-outline-dark btn-md">Our Story</a>
        </div>

        <div class="col-md-4 my-4">
          <img src="img/2.jpg" alt="" class="w-100" />
          <h4 class="my-4">Lorem, ipsum.</h4>
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit.
            Aspernatur, iure!
          </p>
          <a href="#" class="btn btn-outline-dark btn-md">Our Story</a>
        </div>

        <div class="col-md-4 my-4">
          <img src="img/3.jpg" alt="" class="w-100" />
          <h4 class="my-4">Lorem, ipsum.</h4>
          <p>
            Lorem ipsum dolor, sit amet consectetur adipisicing elit.
            Aspernatur, iure!
          </p>
          <a href="#" class="btn btn-outline-dark btn-md">Our Story</a>
        </div>
      </div>
    </div>
    <!-- End Three Column Section -->

    <!-- Emoji Navbar First -->
    <a
      class="navbar bg-primary sticky-top emoji"
      href="#emoju"
      role="button"
      data-toggle="collapse"
    ></a>

    <!-- Start Fixed Background IMG -->
    <div class="fixed-background">
      <div class="row text-light py-5">
        <div class="col-12 text-center">
          <h1>Advance to Next Level</h1>
          <h3>..see what's on the other side</h3>
          <!-- 這邊使用modal library可以達到跳出視窗的效果 -->
          <button
            type="button"
            data-toggle="modal"
            data-target="#modal1"
            class="btn btn-primary btn-lg mr-2"
          >
            Blue pill
          </button>
          <button
            type="button"
            data-toggle="modal"
            data-target="#modal1"
            class="btn btn-danger btn-lg ml-2"
          >
            Red pill
          </button>
        </div>
      </div>
      <div class="fixed-wrap">
        <div class="fixed"></div>
      </div>
    </div>
    <!-- End Fixed Background IMG -->

    <!-- Emoji Navbar Second -->
    <a
      class="navbar bg-primary sticky-top emoji"
      href="#emoji"
      role="button"
      data-toggle="collapse"
      ><i class="fas fa-plug"></i
    ></a>
    <div class="collapse" id="emoji">
      <div class="container">
        <div class="row">
          <div class="col-sm-6 col-md-3">
            <img src="img/emoji/panda.gif" alt="" class="w-100" />
          </div>
          <div class="col-sm-6 col-md-3">
            <img src="img/emoji/poo.gif" alt="" class="w-100" />
          </div>
          <div class="col-sm-6 col-md-3">
            <img src="img/emoji/unicorn.gif" alt="" class="w-100" />
          </div>
          <div class="col-sm-6 col-md-3">
            <img src="img/emoji/chicken.gif" alt="" class="w-100" />
          </div>
        </div>
      </div>
    </div>
    <!-- Modal Popup -->
    <!-- modal連接處 -->
    <div class="modal fade" id="modal1">
      <div class="modal-dialog">
        <img src="img/emoji/poo.gif" alt="" class="w-100" />
      </div>
    </div>
    <!-- Start Two Column Section -->
    <div class="container my-5">
      <div class="row py-4">
        <div class="col-lg-4 mb-4 my-lg-auto">
          <h1 class="text-dark font-weight=bold mb-3">We've Expecting YOu</h1>
          <p class="mb-4">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Sapiente
            tenetur minus illum excepturi beatae neque at numquam a nam
            voluptas!
          </p>
          <a href="#" target="_blank" class="btn btn-outline-dark btn-lg"
            >The Agency THeme</a
          >
        </div>

        <div class="col-lg-8">
          <img src="img/code.jpg" alt="" class="w-100" />
        </div>
      </div>
    </div>
    <!-- End Two Column Section -->

    <!-- Start Jumbotron -->
    <div class="jumbotron py-5 mb-0">
      <div class="container">
        <div class="row">
          <div class="col-md-7 col-lg-8 col-xl-9 my-auto">
            <h4>Lorem ipsum dolor sit amet.</h4>
          </div>

          <div class="col-md-5 col-lg-4 col-xl-3 pt-4 pt-md-0">
            <a href="#" class="btn btn-primary btn-lg">Contact US</a>
          </div>
        </div>
      </div>
    </div>
    <!-- End Jumbotron -->

    <!-- Start Footer -->
    <footer>
      <div class="container">
        <div class="row text-light text-center py-4 justify-content-center">
          <div class="col-sm-10 col-md-8 col-lg-6">
            <img src="img/logo-white.png" alt="" />
            <p>
              Lorem ipsum dolor sit amet consectetur adipisicing elit. Iusto
              laudantium culpa voluptates repellat! Hic rerum error facilis
              sequi natus voluptates enim tenetur. Provident iusto laborum minus
              aliquam, eum placeat?
            </p>
            <ul class="social pt-3 m-auto">
              <li>
                <a href="#"><i class="fab fa-facebook"></i></a>
              </li>
              <li>
                <a href="#"><i class="fab fa-twitter"></i></a>
              </li>
              <li>
                <a href="#"><i class="fab fa-instagram"></i></a>
              </li>
              <li>
                <a href="#"><i class="fab fa-youtube"></i></a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </footer>
    <!-- End Footer -->

    <!-- Start Socket -->
    <div class="socket text-light text-center py-3">
      <p>&copy; <a href="#">123.com</a></p>
    </div>
    <!-- End Socket -->

    <!-- Script Source Files -->
    <!-- jQuery -->
    <script src="js/jquery-3.5.1.min.js"></script>
    <!-- Bootstrap 4.5 JS -->
    <script src="js/bootstrap.min.js"></script>
    <!-- Popper JS -->
    <script src="js/popper.min.js"></script>
    <!-- Font Awesome -->
    <script src="js/all.min.js"></script>
    <!-- End Script Source Files -->
  </body>
</html>

```


# CSS:

## CSS完整程式碼

[CSS 原始碼](https://github.com/chiehLiu/git-projects/blob/bootstrap-practice-1/Bootstrap%202020%20Starter%20Files/css/style.css)