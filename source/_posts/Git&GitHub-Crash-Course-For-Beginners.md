---
layout: p
title: Git & GitHub Crash Course For Beginners
date: 2021-02-22 22:05:23
tags: Git
category: Git
---

# Git & GitHub Crash Course For Beginners

---

## tags: git relate

###### tags: `git`

# GIT 是甚麼

- VCS(Version Control System)追蹤電腦檔案的改變
- 分散式版本控制(去中央化版本控制) Distributed version control

  > 代表專案的開發者們不需要在同一個網路環境下完成

- 2005 年被 Linus Torvalds 創造也是 Linux 的創造者
- JAVA PYTHON Static html node.js c#....都能使用它，它只是單純儲存檔案
- 隨時都能回朔檔案只要有其他時期儲存的 commits
- 有使用者端以及遠端的存在

# GIT 的概念

- 追蹤 code 的歷史紀錄
- 為你的檔案做簡潔的紀錄
- commit 就是"簡潔的紀錄"並且可以在任意時候完成
- 可以造訪那些 commit 在任意時候
- 在 commit 之前可以有一個前置階段

# 安裝 GIT

Mac

http://git-scm.com/download/mac

Windows

http://git-scm.com/download/win

# 指令

## 基本指令

`git init` // 啟動一個本地端的 Git 檔案夾

- 當要操作任何檔案之前都要做這個動作

`git add<file>` // 加入檔案到 Index 裡面

`git add .` // 加入全部檔案到 Index 裡面

`git rm --cashed <file>` // 刪除 git add 的狀態

`git status` // 確認檔案狀況從整個工作樹中(Working Tree)

- 這裡是 commit 之前的一個前置階段

`git commit -m"file"` // commit

`git push` // 把檔案推到遠端的檔案夾(如 Github)

`git pull` // 從遠端把最新的檔案抓下來

`git clone` // 把遠端的檔案複製下來目前本機端要使用的檔案夾內

`git rm --cashed <file>` //

# 實際專案操作

首先設立一個資料夾並且選 git bash here
![](https://i.imgur.com/2wufyAV.png)

就可以看到會直接連結到這個資料夾的位置
![](https://i.imgur.com/ut0UI5H.png)

`touch` index.html, app.js
![](https://i.imgur.com/urCbII6.png)

`git init` 啟用這個資料夾
![](https://i.imgur.com/HhoZRia.png)
會多一個.git 資料夾出現
![](https://i.imgur.com/3AxGzqP.png)

## git 自機版本存檔操作

建立一個檔案 hello.txt

`git status` 查看狀態

會有剛剛加入的文件名稱並且顯示紅字

![](https://i.imgur.com/jOWrDeS.jpg)

---

這時候使用 `git add .` 加入資料夾內所有的檔案加入追蹤

通常輸入成功會沒有東西出現就是好事，有出錯的話會有錯誤訊息顯示

再次輸入 `git status` 查看狀態

這個時候會顯示剛剛加入的文件名稱並且變成綠色

![](https://i.imgur.com/lpZRx4r.jpg)

---

接著輸入 `git commit -m "add new file hello.txt"` 存檔的概念(版本紀錄)

![](https://i.imgur.com/MCrXkbm.jpg)

再次輸入 `git status` 確認內容

![](https://i.imgur.com/zQitUFx.jpg)

到這個階段剛剛的新的文件存上去存檔的地方摟!

## 註冊 github 以及把檔案推上去

https://github.com/

接下來就是正常的註冊流程，推薦先不要開啟二階段認證會造成比較多麻煩

下一步就是要開啟新的 Repository，它就是在 Github 上最主要的運作單位

在 your repositories 的頁面下找到 NEW 新增後會進入

![](https://i.imgur.com/cmLoaj6.png)

通常填完 Repository 之後 點擊 Create Repository

### 上傳本機端的資料上傳到雲端

這個時候要先從 CMD 確認說有無連結雲端:

![](https://i.imgur.com/96pTucw.png)

這時候看到的空白代表雲端是沒有關聯的遠端空間，所以下一步我們就開始做連結

![](https://i.imgur.com/2Bo6Unw.png)

ps. 大部分會用 origin 做遠端的名字是個習慣，但其實可以自己取都行

下一步到剛剛 your repositories 上面尋找上面尋找這裡點下 HTTPS 後複製這段網址並貼回去上面

![](https://i.imgur.com/zItM0W7.png)

![](https://i.imgur.com/A1G0ffL.png)

如果是第一次連結它會需要你做一些認證輸入帳號密碼名稱等等

這個時候再查詢一次做 git remote -v 這個時候會顯示這個

![](https://i.imgur.com/6NU4JaK.png)

fetch 以及 push 左邊那串網址代表我們上傳以及我們下載檔案的雲端網址非常重要

### git push 把檔案推上雲端

當我們要把檔案存到雲端上面的時候我們會使用這個指令，

`git push origin(雲端名稱) master(分支名稱)`

![](https://i.imgur.com/TVqeZLG.png)

推上去檔案之後雲端就會有連接到的檔案

![](https://i.imgur.com/pX2Xi8X.png)

在這個介面下就可以看到每次建立的 commit 紀錄非常方便！

## 安裝 SourceTree

下載網址

https://sourcetreeapp.com/

因為 Windows 不像 Mac 系統可以使用 stree . 這個指令叫出程式

可以從 File 的地方開啟待會要作業的檔案的資料夾

![](https://i.imgur.com/AgB5S10.png)

就可以從這邊看到剛剛檔案的編輯紀錄

![](https://i.imgur.com/ESeQnMN.png)

# git 的工作流程圖

![](https://i.imgur.com/StCQLji.png)

![](https://i.imgur.com/LcfUBpn.png)

# 其他學習資源

https://gitbook.tw/

https://ihower.tw/git/index.html

https://github.com/doggy8088/Learn-Git-in-30-days?fbclid=IwAR2tU7V7kmvVJJgZVJpyHu8ACiJPk7vifaQCKULHKCUrp7OUJwT8HeQy_j4

https://backlog.com/git-tutorial/tw/intro/intro1_1.html
