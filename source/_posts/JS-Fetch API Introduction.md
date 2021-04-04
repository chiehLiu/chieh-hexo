---
title: JS-Fetch API Introduction(5000字)
date:
tags: Javascript
category: Javascript
---

# Fetch API Introduction(Vanilla JavaScript)

---
tags: Javascript relate
---

###### tags: `Javascript`


# 使用Fetch API取得plain text

## 建立一個plain text待會使用
![](https://i.imgur.com/qo8Shae.png)

## response印出的結果是目前response的一些狀態
![](https://i.imgur.com/w40HcCx.png)


```javascript=
<body>
    <button id="getText">Get Text</button>
    <div id="div"></div>
    
    <script>
      document.getElementById("getText").addEventListener("click", getText);

      function getText() {
        fetch("sample.txt").then(function (res) {
          console.log(res);
        });
      }
    </script>
</body>
```
## 確認response的text()

想要確認response的text()，卻得到還在pending的promise，同時可以看到裡面包含著value是我們要的內容，但目前還不能使用
![](https://i.imgur.com/b5iqQch.png)


```javascript=
function getText() {
        fetch("sample.txt").then(function (res) {
          console.log(res.text());
        });
      }
```

## 轉換response 成 text
因為內容是plain tex所以必須轉換response 成 text
return其值後，再使用一次`.then`即可印出值摟!

![](https://i.imgur.com/7sHhNNL.png)


```javascript=
function getText() {
        fetch("sample.txt")
          .then(function (res) {
          
          //因為內容是plain tex所以必須轉換response 成 text
            return res.text();
          })
          .then(function (data) {
            console.log(data);
          });
      }
```

## 使用箭頭函式寫一遍


```javascript=
fetch("sample.txt")
          .then((res) => res.text())
          .then((data) => console.log(data));
      }
```

## 把獲取到的plain text 貼到DOM

![](https://i.imgur.com/QBcQ8jN.png)

![](https://i.imgur.com/aKSmxFf.png)

```javascript=
fetch("sample.txt")
          .then((res) => res.text())
          .then((data) => {
            document.getElementById("div").innerHTML = data;
          });
```

## `catch()`

當reject情況發生的時候的時候，會跑catch內部的函式

印出錯誤訊息以及字串"err"
![](https://i.imgur.com/ZPQXl47.png)


```javascript=
fetch("sample.txt")
          .then((res) => res.text())
          .then((data) => {
            document.getElementById("divv").innerHTML = data;
          })
          .catch((err) => {
            console.log("err");
            console.error(err);
          });
```


# 使用Fetch API取得JSON格式的資料

## 先建立一個JSON檔案待會做取用

從這邊可以看到要操作的資料被包裹在陣列裡面
![](https://i.imgur.com/jFUOq7A.png)


## 用forEach操作陣列資料後以ES6字串串接的方式呈現

因為內容是JSON格式所以必須轉換response 成 JSON格式再使用forEach去逐個印出
forEach內部的函式是每一個印出的user該長的樣子讓他符合html的格式後再使用innerHTML貼上去outputs
![](https://i.imgur.com/Dr8rzap.png)



```javascript=
function getUsers() {
        fetch("users.json")
          .then((res) => res.json())
          .then((users) => {
            let outputs = "";
            users.forEach((user) => {
              outputs += `
              <ul>
                <li>ID:${user.id}</li>
                <li>name:${user.name}</li>
                <li>email:${user.email}</li>
                </ul>
              `;
            });
            document.getElementById("div").innerHTML = outputs;
          });
      }
```

# 使用Fetch API POST JSON格式的資料

當點擊submit按鈕時，會送出POST方法。

下面有展示一些簡易的POST寫法，之後的.then處理方式是跟GET方法是一樣的

![](https://i.imgur.com/P5SIhv4.png)


```javascript=
<body>

    <form id="addPost">
        <div>
            <input type="text" id="title" placeholder="Title"></input>
        </div>

        <div>
            <textarea type="text" id="body" placeholder="Body""></textarea>
        </div>
        <input type="submit" value="submit">
    </form>
    <div id="div"></div>
    <script>
      
      document.getElementById("addPost").addEventListener("submit", addPost);

      function addPost(e) {
          e.preventDefault();

          let title = document.getElementById("title").value;
          let body = document.getElementById("body").value;

          fetch('https://jsonplaceholder.typicode.com/posts', {
              method: 'POST',
              headers: {
                  'Accept': 'application/json, text/plain, */*',
                  'Content-Type': 'application/json'
              },
              body:JSON.stringify({title: title, body: body})
          })
          .then((res) =>res.json())
          .then((data) =>console.log(data))
      }
    </script>
  </body>
```