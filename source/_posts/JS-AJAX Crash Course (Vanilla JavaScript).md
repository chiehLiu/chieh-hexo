---
title: JS-AJAX Crash Course (5000字)
date:
tags: Javascript
category: Javascript
---



# AJAX Crash Course (Vanilla JavaScript)

---
tags: Javascript relate
---

###### tags: `Javascript`


# AJAX是甚麼?

* Asynchronous Javascript&XML
> 不是種語言、框架、函式庫只是一種網頁工具用來傳送、接收來自客戶端的資料給伺服器用一種非同步的處理方式那就是AJAX
* 簡單來說就是處理這些發送的動作在看不到的狀況下同時不需要重新下載頁面
* 諷刺的地方是雖然命名有被使用到但是 XML相當少使用，比較多使用JSON(Javascript Object Notation)因為比較簡潔快速且受歡迎
* 單純的text也可以被使用



## 圖解AJAX
![](https://i.imgur.com/TKMLQTR.png)


### Common Request&Response

例子:
點擊網頁連結會發出一個common request 給server會回傳common response，而這個response 包含了header或者是網頁內容，基本上使用者要求什麼就回傳甚麼 

### AJAX做的事情

AJAX可做到的事情就是發送request 非同步的方式(Asynchronously)在後方，而不需要重新下載或是刷新全部頁面，而是只更新一小區域的內容，這樣的方式相對快速並且更充滿互動感


### AJAX去做request有幾種方式可以使用

1.使用原生JS語法
2.使用函式庫jQuery, Axios等等


### XmlHttpRequest

XmlHttpRequest Object (XHR)

> 是一種物件型態的API 而他是一種物件代表會有屬性、方法可以使用，而這些其實是瀏覽器的JS環境提供的所以幾乎所有現代的瀏覽器都有這些API可以使用，其中的方法用來**傳送資料往來**用戶端-伺服器端或是瀏覽器-伺服器端

* 一種物件型態的API
* 瀏覽器的JS提供的環境
* 使用方法(methods)傳送資料往來用戶端-伺服器端
* 不只使用http，其他的protocols也可以使用
* 可以使用的資料格式有XML,JSON,plain text(純文字)


### Server端回傳資料

通常回傳的資料或是以JSON或是XML格式或是純文字


### HTML Response

這部分通常可以通過DOM去更新頁面或是回傳使用者要求的資料等等，回應使用者的需求

### Different ways(libraries&other methods) to make AJAX call

* jQuery
* Axios
* Superagent
* Fetch API 瀏覽器提供的功能
* Prototype
* Node HTTP

# Let's Write Some Code


## Environment setup

[下載 XAMPP](https://www.apachefriends.org/zh_tw/download.html)

![](https://i.imgur.com/afbClYT.png)


[XAMPP設定影片](https://www.youtube.com/watch?v=6tCWiexc05U&list=PLillGF-Rfqbap2IB6ZS4BBBcYPagAjpjn&index=2&ab_channel=TraversyMedia)


### 創造資料夾擺接下來的要操作的範例

![](https://i.imgur.com/SyFwXky.png)

創造資料夾ajaxcrash
![](https://i.imgur.com/MlL1rhU.png)

使用VScode開啟這個資料夾並且創建html檔案ajax1.html

打開一個網頁連接到剛剛創建好的資料夾就可以開始跟課程瞜!
![](https://i.imgur.com/e4Q1w72.png)

設置一個sample.txt待會
待會程式會抓取使用並放入一些隨意的內文

![](https://i.imgur.com/ioDd0QK.png)

## AJAX 1 -Text File 純文字檔案AJAX提取

### onload()

當印出xhr會得到一些可以使用的方法
![](https://i.imgur.com/Yt8JHRd.png)

創建一個按鈕來抓取sample.txt的內容
![](https://i.imgur.com/SEEgr3F.png)

當成功抓取內文後，查看Netword內容
使用的方法:GET
Status Code:200 OK
Content Type:text/plain
![](https://i.imgur.com/YfTSz3F.png)


```javascript=
<body>
    <button id="button">Get Text File</button>


    <script>
        //create event listener
        document.getElementById("button").addEventListener("click", loadText);

        function loadText() {
            //創造xhr物件 create XHR object
            var xhr = new XMLHttpRequest();
            //open方法填入的參數 open - type, url/file, async
            xhr.open("GET", 'sample.txt', true);

            //當status =200時印出sample.txt的內容
            xhr.onload = function () {
                if (this.status == 200) {
                    console.log(this.responseText);
                }
            }

            //使用這個方法後才會顯示出內容在console裡面(send request)
            xhr.send();
        }

        //HTTP Status
        //200 : "OK"
        //403 : "Forbidden"
        //404 : "Not Found"
    </script>
</body>
```

在onload狀態做`console.log('readystate:', xhr.readyState);`來看看目前位置的readystate在哪個位置

會發現只有![](https://i.imgur.com/uLMFaJP.png)中間的過程都不會跑


#### 當onload出錯的時候 產生404狀態的時候也可以呈現在DOM上面

這邊如果想要練習可以藉著把sample改名就可以取得這樣的狀態摟!

![](https://i.imgur.com/LBmMEiF.png)


```javascript=
xhr.onload = function () {
                console.log('readystate:', xhr.readyState);
                if (this.status == 200) {
                    //正常狀態下顯示在DOM的處理
                    document.getElementById('text').innerHTML = this.responseText
                // 也就是404的狀態也可以呈現在HTML上面
                } else if (this.status == 404) {
                    document.getElementById('text').innerHTML = "Not Found"
                }
            }
```


### onreadystatechange()

會得出一樣的respose內容，差別在於`onreadystatechange()`在readystate必須在4的情況下也就是(4:request finished and response is ready)才會印出reponse的內容


可以使用`console.log('readystate:', xhr.readyState);`來看看目前位置的readystate在哪個位置

```javascript=
function loadText() {
            //create XHR object
            var xhr = new XMLHttpRequest();
            //open - type, url/file, async
            xhr.open("GET", 'sample.txt', true);

            // 當放在這一段的時候只會得到readystate1
            console.log('readystate:', xhr.readyState);

            // xhr.onload = function () {
            //     if (this.status == 200) {
            //         // console.log(this.responseText);
            //     }
            // }
            xhr.onreadystatechange = function () {
                console.log('readystate:', xhr.readyState);
                if (this.readyState == 4 && this.status == 200) {
                    // console.log(this.responseText);
                }
            }

            //send request
            xhr.send();
        }
```

放在條件式function之前時會顯示1

放在條件式中時會跑1234一直到也就是完成request以及respose ready內容進條件事就會跑後方的動作也就是印出responseText

![](https://i.imgur.com/CI6r4hC.png)


```javascript=
<body>
    <button id="button">Get Text File</button>


    <script>
        //create event listener
        document.getElementById("button").addEventListener("click", loadText);

        function loadText() {
            //create XHR object
            var xhr = new XMLHttpRequest();
            //open - type, url/file, async
            xhr.open("GET", 'sample.txt', true);

            xhr.onreadystatechange = function () {

                // 這邊的readyState必須是4下方的內容才會被印出
                if (this.readyState == 4 && this.status == 200) {
                    console.log(this.responseText);
                }
            }

            //send request
            xhr.send();
        }

        // readyState Values
        // 0:request not initialized
        // 1:server connection established
        // 2:request received
        // 3:processing request
        // 4:request finished and response is ready
    </script>
</body>
```

#### 兩者的區別

在於兩者的readyState

* onload - 它不會執行除非狀態是readyState:4
* onreadystatechange - 卻是readyState:2,3也會執行


### onprogress()

等待網頁載入時會跑的gif動畫時背景在做的事情

使用`console.log('readystate:', xhr.readyState);`來看看目前位置的readystate在哪個位置得出 3:processing request

![](https://i.imgur.com/EUDGFaX.png)


```javascript=
xhr.onprogress = function () {
                console.log('readyState:', xhr.readyState);
            }
```

### onerror()

當onload事件出錯時會跑這邊的函式

```javascript=
xhr.onerror = function () {
                console.log('Request Error...');
            }
```

### 把取得的response放到DOM上面

在上方的HTML先設置一個區域可以抓取的div

![](https://i.imgur.com/a6SCQQi.png)

抓好之後使用`innerHTML`修改內容變成`responseText`就可以把DOM呈現reponse的內容了

```javascript=
xhr.onload = function () {
                console.log('readystate:', xhr.readyState);
                if (this.status == 200) {
                    // console.log(this.responseText);
                    document.getElementById('text').innerHTML = this.responseText
                }
            }
```

## AJAX2 - Local JSON 本地端資料夾AJAX提取資料

前置作業:

設置ajax2.html來操作JSON
![](https://i.imgur.com/0DC8Qzo.png)

多設置兩個資料夾待會做操作使用
![](https://i.imgur.com/qrt5R5j.png)

![](https://i.imgur.com/PQBR87Z.png)

並且轉換伺服器網址到ajax2
![](https://i.imgur.com/qjvxRwM.png)

### 取得JSON格式得內容

使用下方的程式碼可以取得JSON全部的內容!

當點Get User時會產生下面的資料在console中
![](https://i.imgur.com/ebGT9GQ.png)

![](https://i.imgur.com/UlScz1z.png)


```javascript=
<body>
    <button id="button1">Get User</button>
    <button id="button2">Get Users</button>

    <h1>User</h1>
    <div id="user"></div>
    <h1>Users</h1>
    <div id="users"></div>

    <script>
        document.getElementById("button1").addEventListener("click", loadUser);

        function loadUser() {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", "user.json", true)

            xhr.onload = function () {
                if (this.status == 200) {
                    console.log(this.responseText);
                }
            }

            xhr.send();
        }
    </script>
</body>
```

### `JSON.parse`


但是如果要取得其中的id,name,email個別取得的時候必須使用`JSON.parse`

下方的範例我使用取的user的名字:Rick以字串的形式印出

```javascript=
xhr.onload = function () {
                if (this.status == 200) {
                    var user = JSON.parse(xhr.responseText);
                    console.log(user.name);
                }
            }
```

### 抓取到的JSON呈現到DOM上

這邊我使用ES6的語法做串接直接貼到innerHTML上

當點擊Get User可以做到這樣的效果
![](https://i.imgur.com/xEdYHx6.png)


```javascript=
function loadUser() {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", "user.json", true)

            xhr.onload = function () {
                if (this.status == 200) {
                    var user = JSON.parse(xhr.responseText);
                    document.getElementById("user").innerHTML =
                        `<ul><li>ID:${user.id}</li><li>name:${user.name}</li><li>email:${user.email}</li></ul>`;
                }
            }

            xhr.send();
        }
```

### 如果要取的複數JSON資料呈現到DOM上


這邊的for...in迴圈會印出物件的屬性並且使用+=把所有的內容接續印出直到把內容印完為止

![](https://i.imgur.com/xRC8VVu.png)


```javascript=
function loadUsers() {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", "users.json", true)

            xhr.onload = function () {
                if (this.status == 200) {

                    var users = JSON.parse(this.responseText);
                    var output = '';

                    for (var i in users) {
                        output +=
                            `<ul><li>ID:${users[i].id}</li><li>name:${users[i].name}</li><li>email:${users[i].email}</li></ul>`;
                    }

                    document.getElementById("users").innerHTML = output;
                }
            }

            xhr.send();
        }
```


## AJAX3 - External API AJAX提取(GitHub作範例)

處理方式基本上跟取的內部資料夾檔案的方式差不多只是在xhr.open的中間的參數改成Github API的網址，其他處理基本上都一樣

![](https://i.imgur.com/l4pEydG.png)


```javascript=
<body>
    <button id="button">Load GitHub Users</button>
    <br>
    <h1>Github Users</h1>
    <div id="users"></div>

    <script>
        document.getElementById("button").addEventListener("click", loadUsers);

        //Load Github Users

        function loadUsers() {
            var xhr = new XMLHttpRequest();
            xhr.open("GET", "https://api.github.com/users", true)

            xhr.onload = function () {

                if (this.status == 200) {
                    var users = JSON.parse(this.responseText);
                    var output = '';

                    for (var i in users) {
                        output +=
                            `<div class="user">
                            <img src="${users[i].avatar_url}" width ="70" height ="70">
                            <ul>
                            <li>ID:${users[i].id}</li>
                            <li>Login:${users[i].login}</li>
                            </ul>
                            </div>`
                    }
                    document.getElementById('users').innerHTML = output;
                }
            }
            xhr.send();
        }
    </script>
</body>
```

## AJAX4 - 使用PHP取得資料並且對比AJAX取得方式(參考閱讀PHP的部分)

### GET

使用正常PHP方式會整個reload網頁
![](https://i.imgur.com/JsuWQEJ.gif)

使用AJAX會再背景處理資料
![](https://i.imgur.com/7dtHe3H.gif)

一樣修改`xhr.open(process.php?name=${name})` 這個部分讓name的部分是input去輸入，其他AJAX部分的操作都差不多，PHP部分就不多做介紹只是舉例子示範


```javascript=
<body>
    <button id="button">Get Name</button>
    <hr>
    <h1>PHP GET FORM</h1>
    <form metod="GET" action="process.php">
        <input type="text" name="name">
        <input type="submit" value="Submit">
    </form>

    <h1>PHP AJAX GET FORM</h1>
    <form id="getForm">
        <input type="text" name="name" id="name1">
        <input type="submit" value="Submit">
    </form>

    <script>
        document.getElementById("button").addEventListener("click", getName);
        document.getElementById("getForm").addEventListener("submit", getName);

        function getName(e) {
            e.preventDefault();

            var name = document.getElementById('name1').value;

            var xhr = new XMLHttpRequest();
            xhr.open("GET", `process.php?name=${name}`, true);

            xhr.onload = function () {
                console.log(this.responseText);
            }
            xhr.send();
        }
    </script>
</body>
```

### POST

頁面呈現其實跟GET差不多但是方法內容不同，可以做參考就好

POST PHP的寫法不太好懂不過也只是要呈現出跟AJAX的差異所以這邊不多做解釋
不過POST的作用是把資料傳進伺服器

```javascript=
<body>
    <h1>PHP POST FORM</h1>
    <form method="POST" action="process.php">
        <input type="text" name="name">
        <input type="submit" value="Submit">
    </form>

    <h1>PHP AJAX POST FORM</h1>
    <form id="postForm">
        <input type="text" name="name" id="name2">
        <input type="submit" value="Submit">
    </form>


    <script>
        document.getElementById("postForm").addEventListener("submit", postName);

        function postName(e) {
            e.preventDefault();

            var name = document.getElementById('name2').value;
            var params = "name=" + name;

            var xhr = new XMLHttpRequest();
            xhr.open('POST', 'process.php', true);
            xhr.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');

            xhr.onload = function () {
                console.log(this.responseText);
            }

            xhr.send(params);
        }
    </script>
</body>
```