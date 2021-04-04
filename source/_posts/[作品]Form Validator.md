---
title: 實作練習-Form Validator
date:
tags: [HTML, CSS, JavaScript, jQuery]
category: Javascript作品
---

# Form Validator - 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個驗證表單

## 成品:

![](https://i.imgur.com/hePYe2K.png)

[成品網址](https://chiehliu.github.io/git-projects/Form-Validator/index.html)

## 成品功能:

1.驗證輸入內容是否符合要求(有各種不同的驗證內容)
2.submit 按下去後會送出內容 3.驗證成功顯示綠色失敗顯示紅色

## HTML

### 表格製作需要注意些一些 type 的地方:

- password-password
- email-text
- username-text

### 上 CSS 之前的 HTML:

![](https://i.imgur.com/aB6G7tM.png)

### 程式碼:

```htmlembedded=
  <body>
    <div class="container">
      <form id="form" class="form">
        <h2>Register With Us</h2>
        <div class="form-control">
          <label for="username">Username</label>
          <input type="text" id="username" placeholder="Enter username" />
          <small>Error message</small>
        </div>
        <div class="form-control">
          <label for="Email">Email</label>
          <input type="text" id="Email" placeholder="Enter Email" />
          <small>Error message</small>
        </div>
        <div class="form-control">
          <label for="Password">Password</label>
          <input type="password" id="Password" placeholder="Enter Password" />
          <small>Error message</small>
        </div>
        <div class="form-control">
          <label for="password2">Confirm Password</label>
          <input type="password" id="password2" placeholder="Enter password again"/>
          <small>Error message</small>
        </div>
        <button type="submit">Submit</button>
      </form>
    </div>
    <script src="script.js"></script>
  </body>
```

## CSS:

### 字體輸出

引入字體的部分要先點選你要的字體粗細大小後，點擊右上角綠色框框會跳出右邊視窗告訴你選了那些字體大小的選項後，點選下方紅框框處的@import 輸出成網址就可以使用瞜!
![](https://i.imgur.com/EZNXyLq.png)

### CSS 設置好的樣式

![](https://i.imgur.com/SApAb10.png)

### 程式碼

```css=
/* 字體輸出的網址部分 */
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,300;0,400;0,600;0,700;0,800;1,300;1,400;1,600;1,700;1,800&display=swap');

/* 讓margin padding boder不礙事的全域 box-sizing:border-box*/
* {
    box-sizing: border-box;
}

/*這邊設置flex讓內容好置中 如果不設置margin 0的話會有預設值要注意*/
body {
    background-color: #f9fafb;
    font-family: 'Open Sans', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
}
/*一點邊框圓潤 以及陰影設定這邊的陰影顏色近乎透明*/
.container {
    background-color: #fff;
    border-radius: 5px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
    width: 400px;
}

h2 {
    text-align: center;
    margin: 0 0 20px;
}

.form {
    padding: 30px 40px;

}
/*這邊的posotion設置relative是為了讓錯誤訊息可以做絕對定位(absolute)使用*/
.form-control {
    margin-bottom: 10px;
    padding-bottom: 20px;
    position: relative;
}

/*這邊轉換display成block才能套用可以設定長寬/margin/padding*/
.form-control label {
    color: #777;
    display: block;
    margin-bottom: 5px;
}

.form-control input {
    border: 2px solid #f0f0f0;
    border-radius: 4px;
    width: 100%;
    padding: 10px;
    font-size: 14px;
}
/*這邊的outline可以設定邊框樣式*/
.form-control input:focus {
    outline: 0;
    border-color: #777;
}

/*下方兩個success跟error的部分會在JS在判斷後加入動態並顯示外框顏色*/
.form-control.success input {
    border-color: #2ecc71;
}

.form-control.error input {
    border-color: #e74c3c;
}

.form-control small {
    color: #e74c3c;
    position: absolute;
    bottom: 0;
    left: 0;
    visibility: hidden;
    /* visibility則是讓內容隱藏 */
    /* display: none; 會讓整個內容消失*/
}

/*要再發生error情況的時候讓錯誤訊息的內容被看到*/
.form-control.error small {
    visibility: visible;
}
/*按鈕部分的設定讓邊框跟按鍵顏色一樣看起來就像無邊框一樣
 * 並且設置display成block可以設定長寬/margin/padding*/
.form button {
    cursor: pointer;
    background-color: #3498db;
    border: 2px solid #3498db;
    border-radius: 4px;
    color: #fff;
    display: block;
    font-size: 16px;
    padding: 10px;
    margin-top: 20px;
    width: 100%;
}
```

### 小補充:

[CSS 教學-關於 display:inline、block、inline-block 的差別](https://medium.com/@wendy199288/css%E6%95%99%E5%AD%B8-%E9%97%9C%E6%96%BCdisplay-inline-inline-block-block%E7%9A%84%E5%B7%AE%E5%88%A5-1034f38eda82)

## JS:

### 作者展示簡單的驗證使用 if...else

```javascript=

//抓取要操作的元素的id
const form = document.getElementById('form');
const username = document.getElementById('username');
const email = document.getElementById('email');
const password = document.getElementById('password');
const password2 = document.getElementById('password2');

// 顯示錯誤訊息出來以及紅色邊框(Show input error message)


//這邊的input指的是eventlistener那邊的各種輸入值像是
//username, email, password, password2;
//message的部分指的是showError後方第二個參數喔!!
function showError(input, message) {

    //這邊input指向的parentElement通常會是"form control"
    //這個div並指派給變數formControl
    const formControl = input.parentElement;

    //並且重新指派新的className給他加上error讓他觸發之前我們在CSS埋好的點
    //".form-control.error small"這個點
    formControl.className = 'form-control error';

    //抓取small這個元素(他原本是顯示錯誤訊息的文字視窗)
    const small = formControl.querySelector('small');
    //並加上參數messge改掉原本的預設值(這邊message有經過判斷決定是
    //username, email, password, password2而會決定填上那些內容)
    small.innerText = message;
}

// 顯示成功邊框(Show success outline)
function showSuccess(input) {

    //這部分比較直觀就是加上success上去讓他跑相關的CSS就好
    const formControl = input.parentElement;
    formControl.className = 'form-control success';
}

//檢查Email是否合理(check email is valid)
function isValidEmail(email) {

    const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(String(email).toLowerCase());

};


// 事件監聽(Event listeners)
form.addEventListener('submit', function (e) {

    //防止他一直傳送會跳掉
    e.preventDefault();


    //四個判斷式判斷輸入內容是否為空，空的話顯示使用showError函式，
    //不然就是呈現使用者輸入的內容
    if (username.value === '') {
        showError(username, 'Username is required');
    } else {
        showSuccess(username);

    }

    //email比較複雜，多了一個內容驗證，
    //如果email內容沒有通過isValidation驗證，
    //則顯示'Email is not valid'，如果內容為空則跑showError函式
    if (email.value === '') {
        showError(email, 'Email is required');
    } else if (!isValidEmail(email.value)) {
        showError(email, 'Email is not valid');
    } else {
        showSuccess(email);
    }
    if (password.value === '') {
        showError(password, 'password is required');
    } else {
        showSuccess(password);

    }
    if (password2.value === '') {
        showError(password2, 'Password2 is required');
    } else {
        showSuccess(password2);
    }

});
```

### 程式碼重構 & 並使用 function 簡化 if...else 條件式

因為事件監聽的部分太多 if..else 的使用程式碼太亂簡化成一個 funciton 加上一些 ES6 的語法來操作

```javascript=

//Check required fields
function checkRequired(inputArr) {

    //這邊因為參數的內容為了因應不要使用太多if...else所以使用array把全部內容包起，
    //因此可以使用array的方法forEach印出所有在迴圈內的內容
    inputArr.forEach(function (input) {

        //這邊的trim()確保不會被空白字元干擾
        if (input.value.trim() === '') {
            console.log(input.id);
            //ES6的語法可以使用參數在${}內接字串非常方便並用getFieldName取得字首大寫
            showError(input, `${getFieldName(input)} is required`);
        } else {
            showSuccess(input);
        }
    })
}

//這邊處理字首大寫用串接的方式處理第一個字跟其他的字
//使用charAt(0)只返回第一個字母並轉大小後，使用slice擷取第一位到最後一個字母，
//再用字串串接起來
function getFieldName(input) {
    return input.id.charAt(0).toUpperCase() + input.id.slice(1);
}

// Event listeners
form.addEventListener('submit', function (e) {
    e.preventDefault();
    //直接使用checkRequired把整個方法外包出去讓程式碼乾淨，
    //並把參數轉成陣列才能使用複數的參數以及使用array的方法
    checkRequired([username, email, password, password2]);
});
```

補充:
`charAt()`
從一個字符串中返回指定的字符。

`slice()`
原為陣列選擇之起始值至終點值（不含終點值）部分，
但是如果不輸入終點值的部分的話則擷取起始值後方全部。

### (完成版)確認內容長短 以及 Email & Password 是否吻合(完成版)

最後加入一些功能:

- 確認 password 以及 username 的長短
- email 部分的判斷式修改
- 確認 password 是否跟 password2 相符合

```javascript=
const form = document.getElementById('form');
const username = document.getElementById('username');
const email = document.getElementById('email');
const password = document.getElementById('password');
const password2 = document.getElementById('password2');

// Show input error message
function showError(input, message) {
    const formControl = input.parentElement;
    formControl.className = 'form-control error';
    const small = formControl.querySelector('small');
    small.innerText = message;
}

// Show success outline
function showSuccess(input) {
    const formControl = input.parentElement;
    formControl.className = 'form-control success';
}

// Check email is valid
function checkEmail(input) {
    const re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    if (re.test(input.value.trim())) {
        showSuccess(input);
    } else {
        showError(input, 'Email is not valid');
    }
}

//Check required fields
function checkRequired(inputArr) {
    inputArr.forEach(function (input) {
        if (input.value.trim() === '') {
            console.log(input.id);
            showError(input, `${getFieldName(input)} is required`);
        } else {
            showSuccess(input);
        }
    })
}

//確認輸入字元長度(check input length)
//蠻直觀的值直接做比大小的動作，一樣搭配Es6的方式做字串串接
function checkLength(input, min, max) {
    if (input.value.length < min) {
        showError(input, `${getFieldName(input)} must be at least ${min} characters`)
    } else if (input.value.length > max) {
        showError(input, `${getFieldName(input)} must be less than${max} characters`)
    } else {
        showSuccess(input);
    }
}

//確認兩個密碼是否吻合如果不合則顯示錯誤在password2(check passwords match)
function checkPasswordMatch(input1, input2) {
  if (input1.value !== input2.value) {
    showError(input2, "Password do not match");
    // console.log("if");
  } else {
    showSuccess(input2);
    // console.log("else");
  }
}

function getFieldName(input) {
    return input.id.charAt(0).toUpperCase() + input.id.slice(1);
}

// Event listeners
//把功能的名稱改的整齊一些
form.addEventListener('submit', function (e) {
    e.preventDefault();
    checkRequired([username, email, password, password2]);

    //注意length的參數必須有起始值以及終點值
    checkLength(username, 3, 15);
    checkLength(password, 6, 25);
    checkEmail(email);
    //這邊要輸入兩個要比較的參數
    checkPasswordMatch(password, password2);
});
```

### 補充:

`trim()`
可以消除字首字尾的空白字元，可以減少 bug 產生

# 進階練習

題目:
優化使用者體驗，讓其輸入當下就判別是否符合條件不需要等到使用 submit

解法

1.使用 keyup 事件當輸入鍵盤當下就會觸發事件

2.把 keyup 事件分開並且把判別的 function 分開，這樣一次記只會處理一個視窗而不是全部搂!

```javascript=
username.addEventListener("keyup", function (e) {
  e.preventDefault();
  checkLength(username, 3, 15);
});

email.addEventListener("keyup", function (e) {
  e.preventDefault();
  checkEmail(email);
});

password.addEventListener("keyup", function (e) {
  e.preventDefault();
  checkLength(password, 8, 16);
});

password2.addEventListener("keyup", function (e) {
  e.preventDefault();
  checkPasswordMatch(password, password2);
});
```

![](https://i.imgur.com/cQBYXGA.gif)
