---
title: 實作練習-Youtube Search Engine
date: 
tags: [HTML, CSS, JavaScript, jQuery, AJAX]
category: Javascript作品
---

# Youtube Search Engine - youtube API

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個 Youtube 影片搜尋網頁

## 成品:

![](https://i.imgur.com/A8eMNIt.png)

[成品網址](https://chiehliu.github.io/git-projects/YoutubeSearchEngine/index.html)

## 成品功能:

1. 搜尋欄位可以輸入內容並且有 Search 按鈕
1. 把找到符合輸入內容的影片五篇呈現在下方
1. 下一頁的按鈕如果還有更多需要內容呈現
1. 上一頁的按鈕可以回到前五篇的內容
1. 點擊超連結(圖片以及標題)會在當前頁面直接跳出影片視窗並且有關閉按鈕(iframe)

# HTML

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>YouTube Search Engine</title>
    <link rel="stylesheet" href="style.css" />

    <!-- 來自fansybox官網 -->
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.css"
    />
  </head>

  <body>
    <nav class="navbar">
      <h1>
        <a href="https://www.youtube.com/"><span>YouTube</span></a> Search
        Engine
      </h1>
    </nav>

    <div class="container">
      <section class="search">
        <input id="inputval" type="text" placeholder="Search..." />
        <button id="btngetval" class="search-btn btn">Search</button>
      </section>

      <div class="results"></div>
      <div class="buttons"></div>
    </div>

    <!-- 這邊的年份等下做JS動態處理年年更新 -->
    <footer class="footer">
      <p>Copyright © <span id="year"></span>, All Rights Reserved</p>
    </footer>

    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script src="script.js"></script>

    <!-- 取得年分 -->
    <script>
      $("#year").text(new Date().getFullYear());
    </script>

    <!-- 來自fancybox官網 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.js"></script>

    <!-- 來自fancybox官方文件 -->
    <script>
      $("[data-fancybox]").fancybox({
        toolbar: false,
        smallBtn: true,
        iframe: {
          preload: false,
        },
      });
    </script>
  </body>
</html>

```

# CSS:

## CSS 完整程式碼

```css=
@import url("https://fonts.googleapis.com/css2?family=Lato:ital,wght@0,100;0,300;0,400;0,700;0,900;1,100;1,300;1,400;1,700;1,900&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  display: flex;
  flex-direction: column;
  justify-content: end;
  align-items: center;
  /* 這邊設置高度讓他滿版 */
  height: 100vh;
  background-color: #1d1d1d;
  color: #dedede;
  font-family: "Lato", sans-serif;
  margin: 0;
  position: relative;
  width: 100%;
}

* span {
  color: #06c5a9;
  position: relative;
}

nav h1 {
  font-weight: bold;
}

a {
  color: #06c5a9;
  text-decoration: none;
}

.navbar {
  margin: 20px;
}

section {
  display: flex;
  margin: 10px 0 10px 0;
}

.container {
  padding: 60px;
  margin: 40px;
  max-width: 700px;
  box-shadow: 0 3px 10px rgba(255, 255, 255, 1);
  background-color: rgb(0, 0, 0);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: stretch;
  border-radius: 5px;
  height: auto;
  width: auto;
}

.container .search {
  display: flex;
  justify-content: center;
}

section input {
  outline: none;
  box-shadow: 0 3px 10px rgba(255, 255, 255, 1);
  border-radius: 5px;
}

img {
  position: relative;
  margin: 10px;
  margin-right: 20px;
  width: 148px;
  height: 113px;
  padding: 3px;
  border-radius: 5px;
  border: solid 1px rgb(58, 57, 57);
  box-shadow: 0 3px 10px rgba(255, 255, 255, 1);
}

* p {
  overflow: auto;
}

.text {
  padding: 3px;
  margin: 10px;
}

section .text {
  font-size: 16px;

  /* 全部強制斷行 */
  word-break: break-all;
}

/* 全域的按鈕長相 */
* .btn {
  padding: 5px;
  margin: 5px;
  font-size: 14px;
  border-radius: 5px;
  background: #444451;
  outline: none;
  color: #dedede;
  box-shadow: 0 3px 10px rgba(255, 255, 255, 0.7);
}

.page {
  margin-bottom: 30px;
}

footer {
  color: #31312f;
}

footer span {
  color: #31312f;
}


```

小補充:

無

# JS:

## 取得 Youtube API 可以操作使用的 url

[參考網址: Youtube Data API - Search Engine](https://orow.github.io/2019/03/17/Youtube-Data-API/)

可以從這邊設定你想要添加的屬性並且操作看看會取得的網址內容且不會消耗配額
[Data API 官方文件 - Try this API](https://developers.google.com/youtube/v3/docs/search/list)

針對這個專案我選用:
part: snippet(這個基本上就是我們需要的)

這邊不要勾 google oauth2.0
![](https://i.imgur.com/391HfLY.png)

基本上就可以符合這個專案的需求瞜!
![](https://i.imgur.com/ImoLbAV.png)

## url 回傳資料操作

需要操作的屬性標註在下方圖片中把他們貼到 DOM 就可以搂!

![](https://i.imgur.com/EH4BHYn.png)

## 變數設置

- nextPageToken - 是換頁最重要的內容必須嵌入網址中
- prevPageToken - 同上
- q - 所有 function 都必須抓取搜尋欄的內容並且必須一致
- output - 把 DOM 的內容貼進去再去做`append()`,`html()`
- DOM 的變數設置 - 處理資料並且針對屬性去做抓取的動作

## functions:

- getVideoData(q) -功能:呈現搜尋內容

使用`.ajax()`的 GET 方法取得 url 回傳的資料(url 部分必須嵌入參數讓其可以動態改變)

注意:

1. datatype:必須填入 json
1. 網址後方的 id key 要記得填入

```javascript=
$.ajax({
    type: "GET",
    url: `
    https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelType=any&order=relevance&q=${q}&type=video&videoCaption=any&videoEmbeddable=any&videoLicense=any&videoType=any&prettyPrint=true&key=AIzaSyDNdqNoZCYqxEJ0nHKh3BWO7Yxc7fLLH2I`,
    dataType: "json",
```

下一步在`.ajax()`屬性`sucess`中把回傳的資料處理並且`forEach`上去 DOM 上面

最後處理按鈕:

所有的頁面回傳資料都會包含上、下一頁的 token(如果有的話，沒有會回傳 undefined)，

---

- nextPage() - 功能:呈現下一頁內容

跟`getVideoData(q)`功能幾乎一樣，但是因為是下一頁所以必須以動態的方式抓取 token 以及 q，
頁面的 token 已經被傳入按鈕中，所以使用`.data()`的方式抓取資料(下方有補充資料)並且傳入 url 中，並且一樣會產出頁面 token(因為一樣得輸出上下頁按鈕)並且輸入到`getBtn(nextPageToken, prevPageToken)`讓下一頁可以吃到 token

```javascript=
$.ajax({
    type: "GET",
    url: `
    https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelType=any&order=relevance&pageToken=${nextPageToken}&q=${q}&type=video&videoCaption=any&videoEmbeddable=any&videoLicense=any&videoType=any&prettyPrint=true&key=AIzaSyDNdqNoZCYqxEJ0nHKh3BWO7Yxc7fLLH2I`,
    dataType: "json",
```

- prevPage() - 功能:呈現上一頁內容

功能內容同上，只需要更改參數名稱

- getBtn(nextPageToken, prevPageToken) - 功能:製造按鈕

1. 按鈕傳遞上一頁/下一頁的 token
1. 使用判斷是來決定呈現什麼按鈕
1. 一樣必須定義 q 是搜尋欄輸入的內容
1. 使用`onclick`把換頁以及搜尋參數傳入`nextPage()`,`prevPage()` function 內

## 事件監聽

功能:取得 input 的值並且輸入 getVideoData(q)內

```javascript=
// 功能:取得input的值並且輸入getVideoData(q)內
$("#btngetval").click(function (e) {
  e.preventDefault();
  let q = $("#inputval").val();
  getVideoData(q);
});
```

## iframe 使用

### html 引入 iframe

[iframe 引用網址](https://cdnjs.com/libraries/fancybox)
[iframe 官方文件](http://fancyapps.com/fancybox/3/docs/#iframe)

最上方引入 iframe 的 CSS 設定一定在官網可以找到

```htmlembedded=
<!-- 來自fansybox官網 -->
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.css"
    />
```

直接擺入 html 最下方來引入(跟 jQuery 或是 js 檔案引入位置相同)

```htmlembedded=
 <!-- 來自fancybox官網 -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/fancybox/3.5.7/jquery.fancybox.min.js"></script>

<!-- 來自fancybox官方文件 -->
<script>
  $("[data-fancybox]").fancybox({
    toolbar: false,
    smallBtn: true,
    iframe: {
      preload: false,
    },
  });
</script>
```

### 針對頁面超連結的部份

最後面的部份是 videoId 可以在 id 內找到(這邊是 sucess 後回傳的資料)
![](https://i.imgur.com/mBBBWyj.png)

使用這串就可以把它們嵌入 iframe 內
`https://www.youtube.com/embed/${vid.id.videoId}`

並且按照這個模式操作 iframe 的區塊

```javascript=
<a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"></a>
```

## 小補充

[.data() - 官方文件](https://api.jquery.com/data/)

[.ajax() - 官方文件](https://api.jquery.com/jQuery.ajax/)

## JS 完整程式碼:

```javascript=
// 功能:取得input的值並且輸入getVideoData(q)內
$("#btngetval").click(function (e) {
  e.preventDefault();
  let q = $("#inputval").val();
  getVideoData(q);
});

// 功能:呈現搜尋內容

// 把輸入的資料來搜尋影片使用$.ajax()
// 網址中的參數是輸入的內容成功載入資料後會跑func sucess
// 處理得到的資料並且forEach到DOM上面
// 取出當前網址的下一頁/上一頁的token並且賦予變數並且傳到getBtn裡面
// 把取得到頁面token以及DOM內容分別貼上HTML
// iframe 的使用格式得參照官網 頗複雜
function getVideoData(q) {
  $.ajax({
    type: "GET",
    url: `
    https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelType=any&order=relevance&q=${q}&type=video&videoCaption=any&videoEmbeddable=any&videoLicense=any&videoType=any&prettyPrint=true&key=AIzaSyDNdqNoZCYqxEJ0nHKh3BWO7Yxc7fLLH2I`,
    dataType: "json",
    success: function (res) {
      let videos = res.items;
      let nextPageToken = res.nextPageToken;
      let prevPageToken = res.prevPageToken;
      let output = "";

      [...videos].forEach(function (vid) {
        output += `<section class="video-area">
                <div class="img">
                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><img src="${vid.snippet.thumbnails.default.url}"
                  /></a>
                </div>

                <div class="text">
                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><h3>${vid.snippet.title}</h3></a
                  ><small>By <span> ${vid.snippet.channelTitle} </span> on ${vid.snippet.publishedAt}</small>
                  <p>${vid.snippet.description}</p>
                </div>
              </section>
              `;

        //貼上搜尋到的結果
        $(".results").html(output);

        // // 加入下一頁按鈕
        let btn = getBtn(nextPageToken, prevPageToken);
        $(".buttons").html(btn);
      });
    },
  });
}

// 功能:呈現下一頁內容

// 功能跟getVideoData()類似
// 從getBtn()取得當前的q以及nextPageToken來跑下一個頁面的資料出來
// 清空最初的搜尋內容並且forEach下一頁的內容上去DOM
// 一樣得取出當前網址的下一頁/上一頁的token並且賦予變數並且傳到getBtn裡面(因為每個下一頁都可能會有上一頁/下一頁)
function nextPage() {
  let nextPageToken = $("#next-button").data("token");
  let q = $("#next-button").data("query");

  q = $("#inputval").val();

  // 清空內容
  $(".results").html("");
  $(".buttons").html("");

  $.ajax({
    type: "GET",
    url: `
    https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelType=any&order=relevance&pageToken=${nextPageToken}&q=${q}&type=video&videoCaption=any&videoEmbeddable=any&videoLicense=any&videoType=any&prettyPrint=true&key=AIzaSyDNdqNoZCYqxEJ0nHKh3BWO7Yxc7fLLH2I`,
    dataType: "json",
    success: function (data) {
      let nextPageToken = data.nextPageToken;
      let prevPageToken = data.prevPageToken;

      // Log Data
      let res = data.items;
      let output = "";

      [...res].forEach(function (vid) {
        output += `<section class="video-area">
                <div class="img">

                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><img src="${vid.snippet.thumbnails.default.url}"
                  /></a>
                </div>

                <div class="text">
                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><h3>${vid.snippet.title}</h3></a
                  ><small>By <span> ${vid.snippet.channelTitle} </span> on ${vid.snippet.publishedAt}</small>
                  <p>${vid.snippet.description}</p>
                </div>
              </section>
              `;

        let btn = getBtn(nextPageToken, prevPageToken);

        //貼上下一頁的搜尋結果
        $(".results").html(output);

        // Display Buttons
        $(".buttons").html(btn);
      });
    },
  });
}


// 功能:呈現上一頁內容

// 基本上跟netxPage()功能一樣指示修改參數名稱
function prevPage() {
  let prevPageToken = $("#prev-button").data("token");
  let q = $("#next-button").data("query");

  q = $("#inputval").val();

  // 清空內容
  $(".results").html("");
  $(".buttons").html("");

  $.ajax({
    type: "GET",
    url: `
    https://youtube.googleapis.com/youtube/v3/search?part=snippet&channelType=any&order=relevance&pageToken=${prevPageToken}&q=${q}&type=video&videoCaption=any&videoEmbeddable=any&videoLicense=any&videoType=any&prettyPrint=true&key=AIzaSyDNdqNoZCYqxEJ0nHKh3BWO7Yxc7fLLH2I`,
    dataType: "json",
    success: function (data) {
      let nextPageToken = data.nextPageToken;
      let prevPageToken = data.prevPageToken;
      let res = data.items;
      let output = "";

      [...res].forEach(function (vid) {
        output += `<section class="video-area">
                <div class="img">

                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><img src="${vid.snippet.thumbnails.default.url}"
                  /></a>
                </div>

                <div class="text">
                  <a data-fancybox data-type="iframe" data-src="https://www.youtube.com/embed/${vid.id.videoId}" href="javascript:;"
                    ><h3>${vid.snippet.title}</h3></a
                  ><small>By <span> ${vid.snippet.channelTitle} </span> on ${vid.snippet.publishedAt}</small>
                  <p>${vid.snippet.description}</p>
                </div>
              </section>
              `;

        let btn = getBtn(nextPageToken, prevPageToken);

        //貼上上一頁的搜尋結果
        $(".results").html(output);

        //貼上按鈕
        $(".buttons").html(btn);
      });
    },
  });
}


// 功能:製造按鈕

// 按鈕傳遞上一頁/下一頁的token
// 使用判斷是來決定呈現什麼按鈕
// 一樣必須定義q是搜尋欄輸入的內容
// 使用onclick把換頁以及搜尋參數傳入nextPage(),prevPage() function內
function getBtn(nextPageToken, prevPageToken) {
  let q = $("#inputval").val();

  // 如果沒有下一頁則按鈕不顯示
  if (nextPageToken === undefined) {
    $(".buttons").html();
    return;
    // 如果沒有上一頁的token則只顯示下一頁
  } else if (prevPageToken === undefined) {
    $(".buttons").html(
      `<div class="button-container"><button id="next-button" class="btn paging-button" data-token="${nextPageToken}" data-query="${q}" onclick="nextPage();">Next Page</button></div>`
    );
    return;
    //其他都顯示
  } else {
    $(".buttons").html(
      `<div class="button-container"><button id="prev-button" class="btn paging-button" data-token="${prevPageToken}" data-query="${q}" onclick="prevPage();">Prev Page</button></div>
    <div class="button-container"><button id="next-button" class="btn paging-button" data-token="${nextPageToken}" data-query="${q}" onclick="nextPage();">Next Page</button></div> `
    );
  }
}

```
