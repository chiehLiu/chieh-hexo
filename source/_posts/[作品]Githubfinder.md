---
title: 實作練習-Githubfinder
date:
tags: [HTML, CSS, JavaScript, jQuery, AJAX]
category: Javascript作品
---

# Githubfinder - github API

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個 github user 尋找器

## 成品:

![](https://i.imgur.com/7tIuxp8.png)

[成品網址](https://chiehliu.github.io/git-projects/githubfinder/index2.html)

## 成品功能:

1.會呈現表面上的各種資訊 大頭貼/profile 連結/Repo 數量/追蹤者數量/公司/Blog/地點/何時加入等 2.跳顯示警告，如果沒找到資訊 3.顯示最新的 Repo 在下方(最多五筆)
4.Repo 以及 Profile 會是有超連結的

# HTML

## html 程式碼:

```htmlembedded=
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://bootswatch.com/4/litera/bootstrap.min.css">
    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <title>GitHub Finder</title>
</head>

<body>
    <nav class="navbar navbar-dark bg-primary mb-3">
        <div class="container">
            <a href="#" class="navbar-brand">GitHub Finder</a>
        </div>
    </nav>
    <div class="container searchContainer">
        <div class="search card card-body">
            <h1>Search GitHub Users</h1>
            <p class="lead">Enter a username to fetch a user profile and repos</p>
            <div id="alert"></div>
            <input type="text" id="searchUser" class="form-control" placeholder="GitHub Username...">
        </div>
        <br>
        <div id="profile">


            <h3 class="page-heading mb-3">Latest Repos</h3>
            <div id="repos"></div>
        </div>
        <div id="123"></div>
    </div>

    <footer class="mt-5 p-3 text-center bg-light">
        GitHub Finder ©
    </footer>

    <!-- <script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"
        integrity="sha384-KJ3o2DKtIkvYIK3UENzmM7KCkRr/rE9/Qpg6aAZGJwFDMVNA/GpGFF93hXpG5KkN" crossorigin="anonymous"> -->
    </script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.12.3/umd/popper.min.js"
        integrity="sha384-vFJXuSJphROIrBnz7yo7oB41mKfc8JzQZiCq4NCceLEaO4IHwicKwpJf9c9IpFgh" crossorigin="anonymous">
    </script>
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta.2/js/bootstrap.min.js"
        integrity="sha384-alpBpkh1PFOepccYVYDB4do5UnbKysX5WZXm3XxPqe5iKTfUKjNkCk9SaVuEZflJ" crossorigin="anonymous">
    </script>

    <script src="script.js"></script>
    <!-- <script src="github.js"></script>
    <script src="ui.js"></script>
    <script src="app.js"></script> -->

</body>

</html>
```

# CSS:

本篇使用 bootstrap

# JS:

本篇最大阻礙一直在阻擋存取 API 非常麻煩!

> {"message":"API rate limit exceeded for 36.225.127.59. (But here's the good news: Authenticated requests get a higher rate limit. Check out the documentation for more details.)","documentation_url":"https://docs.github.com/rest/overview/resources-in-the-rest-api#rate-limiting"}

## 主要的 ajax 屬性參考

[jQuery.ajax](https://api.jquery.com/jQuery.ajax/)

## functions:

- getInputValue() -把從 input 取得的內容丟進去 AJAX 內部取得 user 資料
- getUserData() - 使用 jQuery AJAX 取得 profile 區域的資料
- getRepoData() - 使用 jQuery AJAX 取得 Repo 區域的資料並且把它們推到 DOM 上
- pushElToProfile() -把取得 profile 區域的資料推到 DOM 上

### getInputValue()

單純使用 keyup 事件把 input 的值推進去 getUserData,getRepoData 去做 AJAX

### getUserData()

取得要操作的 url 使用變數的方式改變 username 為 input 去抓取 API 資料，

當成功後處理抓取到的陣列並指派給空的 obj 把它們的屬性一一取出並且指派，並且在此呼叫`pushElToProfile()`並且把指派的變數放入

### getRepoData()

跟上方抓取使用者資料很像，但是這邊不指派給變數而是直接把取得的 API 資料(是陣列形式)做 forEach 處理當傳輸成功時直接把屬性推入 DOM 裡面，因為一次要印出五筆資料必須這樣操作。

當資料傳輸失敗則會跑判斷是判斷 status 是甚麼，給予因應的 msg，並且設置三秒後會移除

### pushElToProfile()

把剛剛指派的 obj 的屬性推上去 DOM

## JS 完整程式碼:

```javascript=
//取得input的值並且使用這個值抓取使用者資料
function getInputValue() {
    const searchUser = $("#searchUser");

    searchUser.keyup(function () {
        getUserData($(this).val());
        getRepoData($(this).val());
    });
}

getInputValue();

// 把取得的input作為變數放到url內去搜尋每個輸入的使用者
function getUserData() {
    let username = $("#searchUser").val();
    let url = `https://api.github.com/users/${username}`;
    $.ajax({
        type: "GET",
        url: url,
        dataType: "json",
        success: function (res) {
            let obj = {};
            obj.avatar_url = res.avatar_url || "no data";
            obj.profile_url = res.html_url || "no data";
            obj.public_gists = res.public_gists || "no data";
            obj.public_repos = res.public_repos || "no data";
            obj.followers = res.followers || "no data";
            obj.following = res.following || "no data";
            obj.company = res.company || "no data";
            obj.location = res.location || "no data";
            obj.blog = res.blog || "no data";
            obj.create_at = res.created_at || "no data";
            // console.log(obj);
            pushElToProfile(obj);
        },
    });
}

function getRepoData() {
    let username = $("#searchUser").val();
    let url = `https://api.github.com/users/${username}/repos?per_page=5&sort=created: asc `;
    $.ajax({
        type: "GET",
        url: url,
        dataType: "json",

        // 錯誤發生的時候跑這個func
        error: function (jqXHR, exception) {
            var msg = "";
            if (jqXHR.status === 0) {
                msg = "Not connect.\n Verify Network.";
            } else if (jqXHR.status == 404) {
                msg = `<div class = "alert alert-danger">Requested page not found.</div>`;
            } else if (jqXHR.status == 500) {
                msg = "Internal Server Error [500].";
            } else if (exception === "parsererror") {
                msg = "Requested JSON parse failed.";
            } else if (exception === "timeout") {
                msg = "Time out error.";
            } else if (exception === "abort") {
                msg = "Ajax request aborted.";
            }
            $("#alert").html(msg);

            setTimeout(() => {
                $("#123").html("");
                $("#alert").html("");
                $("profile").html("");
            }, 3000);
        },

        // 把得到的陣列資料直接做forEach處理並且直接+=到設置為空的output上面最後再把處理好的output貼到html上面
        success: function (res) {
            let output = "";

            res.forEach(function (re) {
                output += `
        <div class="card card-body mb-2">
          <div class="row">
            <div class="col-md-6">
              <a href="${re.profile}" target="_blank">${re.name}</a>
            </div>
            <div class="col-md-6">
            <span class="badge badge-primary">Stars: ${re.stargazers_count}</span>
            <span class="badge badge-secondary">Watchers: ${re.watchers_count}</span>
            <span class="badge badge-success">Forks: ${re.forks_count}</span>
            </div>
          </div>
        </div>
      `;
            });

            // 把剛剛做好的output貼上去html位置<div id="123">
            $("#123").html(output);
        },
    });
}

//profile區域比較單純只要貼上變數即可
function pushElToProfile(obj) {
    let profile = `<div id="profile">
            <div class="card card-body mb-3">
                <div class="row">
                    <div class="col-md-3">
                        <img class="img-fluid mb-2" src="${obj.avatar_url}">
                        <a href="${obj.profile_url}" target="_blank" class="btn btn-primary btn-block mb-4">View
                            Profile</a>
                    </div>
                    <div class="col-md-9">
                        <span class="badge badge-primary">Public Repos: ${obj.public_repos}</span>
                        <span class="badge badge-secondary">Public Gists: ${obj.public_gists}</span>
                        <span class="badge badge-success">Followers: ${obj.followers}</span>
                        <span class="badge badge-info">Following: ${obj.following}</span>
                        <br><br>
                        <ul class="list-group">
                            <li class="list-group-item">Company: ${obj.company}</li>
                            <li class="list-group-item">Website/Blog: ${obj.blog}</li>
                            <li class="list-group-item">Location: ${obj.location}</li>
                            <li class="list-group-item">Member Since: ${obj.create_at}</li>
                        </ul>
                    </div>
                </div>
            </div>`;

    $("#profile").html(profile);
}

```
