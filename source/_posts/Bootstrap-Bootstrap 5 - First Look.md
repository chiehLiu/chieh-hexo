---
title: Bootstrap 5-First Look
date:
tags: Bootstrap
category: Bootstrap
---


# Bootstrap 5 - First Look

---
tags: HTML CSS Bootstrap relate
---

###### tags: `HTML, CSS, Bootstrap`


# bootstrap 5 特色

## 官方文件的更新與改進

新的外觀
Customization新增更多解釋
增加v4版本 主題的頁數以及新增內容
新增npm project


## 擴充color palette

![](https://i.imgur.com/y2VfRW8.png)


## 不需要再引入jQuery
* JS的插件依舊支援
* 減少檔案大小
* 不支援IE瀏覽器


## CSS custom properties

![](https://i.imgur.com/27ThtQm.png)


## 升級Forms

* 更多自主化設定的空間
* 文件的部分新增內容
* 重新設計form controls


## 強化Grid system

* 新的格式xxl tier
* .gutter class被修改
* form layout 被新的grid system取代
* 新增vertical class
* column不再預設position:relative


## 新增icon-library


[取用位置](https://icons.getbootstrap.com/)



# 啟用bootstrap 5 


## 使用方式
 

**使用連結嵌入網址:**
缺點客製化能力比較差

[網址]([取用位置](https://icons.getbootstrap.com/))

![](https://i.imgur.com/9DaDKUc.png)


**使用npm:**

客製化能力比較好

這邊會下載到最新版本
```
npm i bootstrap@next
```

下載icon library
```
npm i bootstrap-icons
```


裝好之後我們看到這邊
![](https://i.imgur.com/I33IubM.png)

引入js的檔案
![](https://i.imgur.com/C3kwixS.png)


所有可用的icons
![](https://i.imgur.com/m779H3T.png)


引入sass的關鍵檔案
![](https://i.imgur.com/bE2CTiT.png)



## 推薦使用插件

live sass compiler

如果有使用live server(基本上一定有這個必裝)
一鍵開關watch功能

![](https://i.imgur.com/JcJHf6d.png)


![](https://i.imgur.com/RZ2grSP.png)


到vscode裡面做設定
點擊json設定檔

![](https://i.imgur.com/pawih09.png)


設定檔案存檔路徑以及不產生source map
```sass=
"liveSassCompile.settings.formats": [
    {
      "format": "compressed",
      "extensionName": ".css",
      "savePath": "/css"
    }
  ],
  "liveSassCompile.settings.generateMap": false
```



設立資料夾如下
![](https://i.imgur.com/v5SIVHu.png)

在main.scss引入bootstap.scss
![](https://i.imgur.com/mjam0ly.png)

會把所有的scss元素轉換成css使用

點擊watch Sass後就可以開始專案摟!
![](https://i.imgur.com/JcJHf6d.png)

![](https://i.imgur.com/nGAydGK.png)

# 專案內容

專案圖示
![](https://i.imgur.com/mG0HCTV.png)

簡單的製作登入頁面(無功能)

## 客製化

針對顏色 客製化

```sass=
$primary: #401f7c;
$secondary: #f4f4f4;
```

針對border 客製化

```sass=
$border-radius:0;
$border-radius-sm:0;
$border-radius-lg:0;
```
針對utilities 客製化

```sass=
// Utilities
$utilities:() !default;
$utilities:map-merge(('input-padding':(property:padding,
            class:ip,
            values:(0:0,
                1:0.3rem,
                2:0.5rem,
                3:0.7rem,
                4:0.9rem,
                5:1rem,
            ),
        )),
    $utilities);
```



## html 

### body
```htmlembedded=
<body class="d-flex text-center bg-secondary">
```

直接使用flexbox並且文字置中並設定背景顏色

```sass=
d-flex = display : flex 
text-center
bg-secondary = backgroup-color : $secondary
```
### logo

則直接取用icon-library

`src="/bs5-landingpage/scss/node_modules/bootstrap-icons/icons/bootstrap.svg"`

並且使用`mb-4`增加下方一點空間

```sass=
.mb-4 {
  margin-bottom: $spacer * 1.5 !important;
}
```

### h1
```htmlembedded=
<h1 class="h3 mb-3 font-weight-normal">Bootstrap 5 Login</h1>
```

重新設定為h3

字體設定`font-weight-normal`

也可以縮寫成 `fw-normal`


### label

`sr-only` screen-reader(幫助聽障人士使用對畫面不影響)

### input

`form-control` 不加大小的話則為預設

form-control的樣板
![](https://i.imgur.com/znnj3CG.png)

ip-3 在上方使用自訂的工具

```sass=
// Utilities
$utilities:() !default;
$utilities:map-merge(('input-padding':(property:padding,
            class:ip,
            values:(0:0,
                1:0.3rem,
                2:0.5rem,
                3:0.7rem,
                4:0.9rem,
                5:1rem,
            ),
        )),
    $utilities);
```


```htmlembedded=
<input type="email" id="inputEmail" class="form-control mb-2 ip-3" placeholder="Email Address" required
            autofocus>
```

### btn

btn樣板們
![](https://i.imgur.com/wfM8nhO.png)


```htmlembedded=
<button class="btn btn-lg btn-primary btn-block" type="submit">Login</button>
```



### 完整程式碼

```htmlembedded=
<body class="d-flex text-center bg-secondary">
    <form class="form-login"><img src="/bs5-landingpage/scss/node_modules/bootstrap-icons/icons/bootstrap.svg"
            height="72" width="72" class="mb-4">
        <h1 class="h3 mb-3 font-weight-normal">Bootstrap 5 Login</h1>
        <label for="inpuEmail" class="sr-only">Email Address</label>

        <input type="email" id="inputEmail" class="form-control mb-2 ip-3" placeholder="Email Address" required
            autofocus>
        <label for="inputPassword" class="sr-only">Password</label>
        <input type="password" id="inputPassword" class="form-control mb-2" placeholder="Password" required>

        <div class="checkbox mb-3">
            <label>
                <input type="checkbox" value="remember-me">Remember Me</input>
            </label>
        </div>
        <button class="btn btn-lg btn-primary btn-block" type="submit">Login</button>
    </form>

    <script src="scss/node_modules/bootstrap/dist/js/bootstrap.min.js"></script>
    <script src="scss/node_modules/popper.js/dist/umd/popper.min.js"></script>
</body>
```