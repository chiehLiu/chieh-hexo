---
title: Hexo 部落格架設
date:
tags: Hexo
Category: Hexo
---

# Hexo 部落格架設

環境配置

- 安裝[NVM](https://github.com/nvm-sh/nvm)
- 安裝 [Node.js](https://nodejs.org/en/)
- 安裝 [Git](https://git-scm.com/)

# NVM,Node.js

> Node Version Manager

Node 的版本控制器，因應各種不同需求所有有辦法下載不同版本的 node.js 是很重要的!

記得要在 WSL 的環境下安裝喔!
[在 windows 安裝 WSL](https://hackmd.io/csXtjcARRWmb9AS3mKC1oQ)

並且使用 VScode 開啟

## Installing and Updating

- 記得終端機環境要選 WSL

- 安裝 NVM
  `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash`

- 更新 Node.js 到最新版本

  `nvm install --lts`

# Hexo

[Hexo](https://hexo.io/zh-tw/)

## Installing and Updating

`$npm install hexo-cli -g`

`$hexo init blog`

`$cd blog` 一定要找到資料夾裝在哪邊!不然之後推不上去 Github

`$npm install`

`$hexo server`

最後一部完成之後基本上就可以得到本地端的 Blog 雛形

![](https://i.imgur.com/XSOHz0O.png)

## 使用 Hexo

這邊必須先把 Hexo 的資料夾 init 才能跟 Github 作部署

```
$ hexo init <folder>
$ cd <folder>
$ npm install
```

使用 Vscode 的資料夾會長這樣

![](https://i.imgur.com/zjxzycC.png)

- \_config.yml：網站 配置 檔案，可以在此配置大部分的設定。
- themes：主題 資料夾。Hexo 會根據主題來產生靜態檔案。

## 常用指令

`$ hexo generate` (hexo g) 產生靜態檔案，會在目錄下產生 public 資料夾。
`$ hexo server` (hexo s) 啟動伺服器，預設是 http://localhost:4000/。
`$ hexo deploy` (hexo d) 部署網站。（ 比如 github, heroku 等平台 ）

`$ hexo new [layout] <title>` 如果沒有設定 layout 的話，則會使用 \_config.yml 中的 default_layout 設定代替。

`$ hexo new “postName”` 新建文章
`$ hexo new page “pageName”` 新建頁面

所有的文章都會在 source/\_posts 裡面。一開始裡面就已經有一篇範例文章 hello-world.md 了。

常用组合

`$ hexo d -g` 產生靜態檔後部署
`$ hexo s -g` 產生靜態檔後預覽

## 更換主題

[Hexo 主題](https://hexo.io/themes/)

Element

是我選取的主題內容

- 必須先使用`git clone`
  抓到本地端的資料夾內，後方的 themes/element 是你要存放的資料夾位置跟名稱

`git clone https://github.com/artchen/hexo-theme-element.git themes/element`

- 詳讀主題作者的 Github 內容
  會有很多安裝資訊以及客製化的方法每一個主題都不太一樣，我這邊有很多必須先預裝的 plugins(插件)

This theme depends on the following Hexo plugins:

```
hexo-generator-tag
hexo-generator-feed
hexo-renderer-ejs
hexo-renderer-scss
hexo-renderer-marked
hexo-pagination
hexo-all-minifier
hexo-autoprefixer
hexo-front-matter
```

- 接著修改網站設定\_config.yml
  他原本預設是 landscape

![](https://i.imgur.com/p8oEqjl.png)

- 重新啟動 server

`$ hexo server`

- 就可以使用主題摟!
  ![](https://i.imgur.com/L3WEgGZ.png)

## 在 GitHub 上新增 GitHub Pages

重點來了，讓 Blog 上線!

1. 在 GitHub 創建一個名稱為`<username>.github.io` 的專案

![](https://i.imgur.com/JRF24hO.png)

1. 安装 deploy git 插件

`npm install hexo-deployer-git --save`

3. 在主題配置文件 \_config.yml 中修改 repository 名稱

![](https://i.imgur.com/Yf9M7VM.png)

4. 執行 hexo d 即可發佈到 GitHub 上

<username>.github.io 到真實的網頁上面輸入就可以看到剛剛推上去的 Blog 搂!
