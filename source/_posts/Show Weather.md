---
title: 實作練習-Show Weather
date:
tags: [HTML, CSS, JavaScript, jQuery, AJAX]
category: Javascript作品
---

# Show Weather - Fetch Weather API

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個顯示台灣天氣的網頁

## 成品:

![](https://i.imgur.com/Pn1V4QU.png)
[成品網址](https://chiehliu.github.io/git-projects/showweather/index.html)

## 成品功能:

1.顯示相對應天氣狀況的圖片 2.資訊更新時間為晚上六點或是早上六點
![](https://i.imgur.com/oB1zc3L.png) 3.溫度，降雨機率，天氣狀況都會隨資料更新

# 天氣 icon 來源

![](https://i.imgur.com/ohjCs54.png)

[Weather Icon](https://elements.envato.com/free/icons/weather/?_ga=2.231913695.1537833515.1612076540-1046268721.1612076540)

# 天氣 API 取得方式

先到[中央氣象局](https://opendata.cwb.gov.tw/userLogin)註冊並且取得授權碼

![](https://i.imgur.com/Zt3jZMb.png)

[中央氣象局開放資料平臺之資料擷取 API](https://opendata.cwb.gov.tw/dist/opendata-swagger.html#/%E9%A0%90%E5%A0%B1/get_v1_rest_datastore_F_C0032_001)

![](https://i.imgur.com/INfYNOq.png)

# HTML

## html 程式碼:

```htmlembedded=
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="stylesheet" href="style.css" />
    <title>Show Weather</title>
  </head>

  <body>
    <h1>Weather In Taiwan</h1>
    <div class="container"></div>

    <script src="script.js"></script>
    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
  </body>
</html>
```

# CSS:

## CSS 完整程式碼

這邊使用 grid 直接排出上下左右的排版非常方便

```css=
@import url('https://fonts.googleapis.com/css?family=Lato&display=swap');


* {
    margin: 0;
}

h1 {
    color: rgb(214, 208, 208);
}

body {
    box-sizing: border-box;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
}

.container {
    display: grid;
    grid-template-columns: 200px 200px 200px;
    justify-content: center;
    align-items: center;
}

.container .weather {
    background-color: rgb(250, 250, 250);
    border: solid 1px rgb(184, 182, 182);
    width: 110px;
    height: 200px;
    margin: 20px;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 5px 10px 10px;

}
.container .weather img {
    text-align: center;
    width: 50%;
    height: 100px;
    margin: auto 0;
}
```

# JS:

## 變數設置

![](https://i.imgur.com/xEMVVYg.png)

name -縣市的部分
POP -降雨機率
WX -天氣狀況描述
MinT -最低溫
MaxT -最高溫

## functions:

- 使用 fetch 抓取從中央氣象局取得的 API 並且使用方法 json()轉換

- 使用展開運算子並且使用 forEach 直接處理資料印出取得下方的結果
- ![](https://i.imgur.com/n8HRA1z.png)

- 個別抓取資料並且填入 DOM

- 圖片的判定是針對 POP(降雨機率去做判讀)

## JS 完整程式碼:

```javascript=
fetch(
  "https://opendata.cwb.gov.tw/api/v1/rest/datastore/F-C0032-001?Authorization=CWB-B7CE0CAC-3B18-4745-B65B-190B83AD9DCD&format=JSON&locationName=&elementName="
)
  .then(function (res) {
    return res.json();
  })
  .then(function (data) {
    const weatherData = data.records.location;

    // console.log(data.records.location);

    [...weatherData].forEach((currentValue, index) => {
      let name = weatherData[index].locationName;
      let POP =
        weatherData[index].weatherElement[1].time[2].parameter.parameterName;
      let Wx =
        weatherData[index].weatherElement[0].time[2].parameter.parameterName;
      let MinT =
        weatherData[index].weatherElement[2].time[2].parameter.parameterName;
      let MaxT =
        weatherData[index].weatherElement[4].time[2].parameter.parameterName;

      console.log(currentValue);

      let img;
      if (POP == 0) {
        img = "img/sun.svg";
      } else if (POP > 25 || POP < 40) {
        img = "img/cloud-sun.svg";
      } else if (POP > 50) {
        img = "Um.svg";
      } else {
        img = "rain.svg";
      }

      let card = document.querySelector(".container");
      card.innerHTML += `

      <div class = "weather">
          <img src="${img}" alt="">
          <p >location: ${name}</p>
          <p >tmp: ${MinT}&#8451~${MaxT}&#8451</p>
          <p >降雨機率: ${POP}%</p>
          <p >${Wx}</p>
      </div>
      `;
    });
  });

```
