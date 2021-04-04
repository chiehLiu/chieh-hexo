---
title: 實作練習-Infinite Scroll Posts
date:
tags: [HTML, CSS, JavaScript]
category: Javascript作品
---

# Infinite Scroll Posts- 20 Web Projects With Vanilla Javascript

---

## tags: Javascript relate

###### tags: `Javascript`

# 製作一個無限往下滑動的表格(範例是 blog)

## 成品:

![](https://i.imgur.com/IOjfucS.png)

[成品網址](https://chiehliu.github.io/git-projects/Infinite%20scroll/index.html)

## 成品功能:

1.在最上方 Filter posts 可以篩選貼文的內容 2.可以一直往下滑不需要換頁

# HTML

## 上 CSS 之前的 HTML:

![](https://i.imgur.com/87hnrNp.png)

## html 程式碼:

```htmlembedded=
<body>
    <h1>My Blog</h1>

    <div class="filter-container">
      <input
        type="text"
        id="filter"
        class="filter"
        placeholder="Filter posts..."
      />
    </div>
    <div id="post-container">
      <!-- 這邊先做兩個比較好修飾CSS -->
      <div class="post">
        <div class="number">1</div>
        <div class="post-info">
          <h2 class="post-title">Post One</h2>
          <p class="post-body">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quasi
            nobis facere explicabo natus amet autem iusto dolore quam sapiente
            est!
          </p>
        </div>
      </div>
      <div class="post">
        <div class="number">2</div>
        <div class="post-info">
          <h2 class="post-title">Post Two</h2>
          <p class="post-body">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Quasi
            nobis facere explicabo natus amet autem iusto dolore quam sapiente
            est!
          </p>
        </div>
      </div>
    </div>

    <div class="loader">
      <div class="circle"></div>
      <div class="circle"></div>
      <div class="circle"></div>
    </div>

    <script src="script.js"></script>
  </body>
```

# CSS:

## CSS 設置好的樣式

![](https://i.imgur.com/IOjfucS.png)

## CSS 完整程式碼

```css=
 @import url('https:fonts.googleapis.com/css?family=Roboto&display=swap');

* {
    box-sizing: border-box;
}


/* 下面拉比較多padding出來跑無限卷軸 */
body {
    background-color: #296ca8;
    color: #fff;
    font-family: 'Roboto', sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
    padding-bottom: 100px;
}

h1 {
    margin-bottom: 0;
    text-align: center;
}

.filter-container {
    margin-top: 20px;
    width: 80vw;
    max-width: 800px;
}

.filter {
    width: 100%;
    padding: 12px;
}

/* post本身包括標題數字內文 */
.post {
    position: relative;
    background-color: #4992d3;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
    border-radius: 3px;
    padding: 20px;
    margin: 40px 0;
    display: flex;
    width: 80vw;
    max-width: 800px;
}

.post .post-title {
    margin: 0;
}cl3

.post .post-body {
    margin: 15px 0 0;
    line-height: 1.3;
}

.post .post-info {
    margin-left: 20px;
}

.post .number {
    position: absolute;
    top: -15px;
    left: -15px;
    font-size: 15px;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #fff;
    color: #296ca8;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 7px 10px;
}

/* 裝球球的容器用來讓球球flex以及固定位置使用fixed */
.loader {

    /*這邊球球要設置CSS的時候記得把透明度這條先註解不然看不到 */
    opacity: 0;
    display: flex;
    position: fixed;
    bottom: 50px;
    transition: opacity 0.3s ease-in;
}

/* 透過JS顯示這段CSS就可以秀出球球了 */
.loader.show {
    opacity: 1;
}

/* 設置球球的造型以及動畫設定 */
.circle {
    background-color: #fff;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    margin: 5px;
    animation: bounce 0.5s ease-in infinite;
}

/* 讓球球的動畫變慢出現不規律的的狀態才是作者要的 */
.circle:nth-of-type(2) {
    animation-delay: 0.1s;
}

.circle:nth-of-type(3) {
    animation-delay: 0.2s;
}
/* 這邊動畫很單純就是Y軸移動，在一半的時間的時往下10px時間跑完時回到0 */
@keyframes bounce {

    0%,
    100% {
        transform: translateY(0);
    }

    50% {
        transform: translateY(-10px);
    }
}
```

小補充:

無

# JS:

## 變數設置

- postsContainer
  抓整條 post 區域
  ![](https://i.imgur.com/EFeb4jQ.png)

- loading
  抓取跑 loading 的球球
  ![](https://i.imgur.com/3Iu8fBb.png)

- filter
  篩選文字區域
  ![](https://i.imgur.com/zGeIXdk.png)

- limit, page
  用來處理更新頁面的每頁 posts 數量以及預設設置第一頁會一直顯示

```javascript=
const postsContainer = document.getElementById('posts-container');
const loading = document.querySelector('.loader');
const filter = document.getElementById('filter');

// 全域變數設置
let limit = 5; //每頁最多5篇文章(要設定到4或是5才會有辦法有scroll出現，不過這邊要看使用者的瀏覽器大小決定)
let page = 1; //default會是第一頁
```

## Functions

- `async function getPosts()`
  getPosts 使用 async 的方式 fetch API 注意記得轉換 JSON 格式

- `async function showPosts()`
  這邊因為要等待(await)getPosts 抓取好資料之後再貼上 showPosts 所以這樣使用

---

- `showLoading()`
  秀出球球以及使用 setTimeout 消除球球並且生成新的 posts

- `filterPosts(e)`
  把所有的 posts 使用 forEach 後個別印出
  再使用 indexOf 來判斷文字是否存在 body 以及 title 裡面

```javascript=
//fetch posts from API
async function getPosts() {
    const res = await fetch(
        `https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`
    );

    const data = await res.json();

    return data;
}

//把取得得posts推到DOM上面也就是post區域(show posts in DOM)
//取得資料後做forEach並且貼上去postsContainer區

//(await)等待getPosts處理好之後 下面的forEach才會開始動作
//這樣的情況下就可以在更新好新的post後把他們加上class以及處理html tag內容
async function showPosts() {
    const posts = await getPosts();

    posts.forEach(post => {
        const postEl = document.createElement('div');
        postEl.classList.add('post');
        postEl.innerHTML = `
        <div class="number">${post.id}</div>
        <div class="post-info">
          <h2 class="post-title">${post.title}</h2>
          <p class="post-body">${post.body}</p>
        </div>
      `;
        // 把處理的新的div貼到postsContainer
        postsContainer.appendChild(postEl);
    });
}

//show loader & fetch more posts
function showLoading() {
    loading.classList.add('show');

    // 這邊注意setTime的持續時間位置不要寫錯
    //一秒之後移除show class就可以把球球去掉
    setTimeout(() => {
        loading.classList.remove('show');

        // 這邊計時0.3秒後會讓page部分+1也就是會在往下生成下一頁五個posts會產生
        setTimeout(() => {
            page++;
            showPosts();
        }, 300);
    }, 1000);
}

//篩選input輸入的內容(filter posts by input)
function filterPosts(e) {

    //要驗證的內容轉大寫比較方便
    const term = e.target.value.toUpperCase();
    const posts = document.querySelectorAll('.post');

    // 一樣為了驗證title,body全部轉大寫
    posts.forEach(post => {
        const title = post.querySelector('.post-title').innerText.toUpperCase();
        const body = post.querySelector('.post-body').innerText.toUpperCase();

        // 判斷式使用indexOf判斷書入的內容term是否在title以及body裡面找不找的到，大於-1表示有找到則顯示原本的flex元素沒有則顯示none
        if (title.indexOf(term) > -1 || body.indexOf(term) > -1) {
            post.style.display = 'flex';
        } else {
            post.style.display = 'none';
        }
    });
}

//在post-container區域貼上取得的posts(show initial posts)
showPosts();
```

## 事件監聽

- 監聽卷軸(scroll) 當捲動卷軸時觸發事件
- 監聽 filter 區域 當 input 區域輸入文字時觸發事件

```javascript=
//event listener

window.addEventListener('scroll', () => {

    //這邊因為作者不想一直打document.documentElement這段所以做解構
    //把這三個方法從其中拿出來直接做變數指派
    const {
        scrollTop,
        scrollHeight,
        clientHeight
    } = document.documentElement;

    //scrollTop是顯示從最上方到滑到的位置的距離
    //scrollHeight是posts的height
    //clientHeight回傳元素內部高度

    //一般來說scrollHeight = scrollTop + clientHeight
    // 所以當往下滑的距離超過原本卷軸也就是srollHeight 5的時候會觸發產生新的posts
    //不一定要放五放一也可以
    console.log(document.documentElement.scrollTop);
    if (scrollTop + clientHeight >= scrollHeight - 5) {
        showLoading();
    }
});

// 當filter被輸入內容就會觸發filterPosts function
filter.addEventListener('input', filterPosts);
```

小補充:

這三個部分出現在無限卷軸的條件裡面:

- [clientHeight 647](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/clientHeight)
  代表目前的 div 的高度

- [scrollTOP 701](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/scrollTop)
  代表轉動 scroll 從頂部往下拉了多少

- [scrollHeight 1348](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/scrollHeight)
  代表 scroll 目前總高度

所以判斷式裡面只要 scrollTOP+clientHeight>=scrollHeight 意思是

一般來說 scrollHeight = scrollTop + clientHeight

所以當往下滑的距離()超過原本卷軸也就是 srollHeight 5(不一定要 5 只要超過就好)的時候會觸發產生新的 posts

這張圖片代表 scrollTOP 也就是你能拉多少距離加上所有 post 的 div 的高度= 下滑距離
![](https://i.imgur.com/78UoPzd.png)

[Async 筆記連結](https://hackmd.io/toOFnYhGTjKZXVf5X8LatA?both)

## JS 完整程式碼

```javascript=
const postsContainer = document.getElementById('posts-container');
const loading = document.querySelector('.loader');
const filter = document.getElementById('filter');

// 全域變數設置
let limit = 5; //每頁最多5篇文章(要設定到4或是5才會有辦法有scroll出現，不過這邊要看使用者的瀏覽器大小決定)
let page = 1; //default會是第一頁

//fetch posts from API
async function getPosts() {
    const res = await fetch(
        `https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`
    );

    const data = await res.json();

    return data;
}

//把取得得posts推到DOM上面也就是post區域(show posts in DOM)

//取得資料後做forEach並且貼上去postsContainer區
async function showPosts() {
    const posts = await getPosts();

    posts.forEach(post => {
        const postEl = document.createElement('div');
        postEl.classList.add('post');
        postEl.innerHTML = `
        <div class="number">${post.id}</div>
        <div class="post-info">
          <h2 class="post-title">${post.title}</h2>
          <p class="post-body">${post.body}</p>
        </div>
      `;

        postsContainer.appendChild(postEl);
    });
}

//show loader & fetch more posts
function showLoading() {
    loading.classList.add('show');

    // 這邊注意setTime的持續時間位置不要寫錯
    //一秒之後移除show class就可以把球球去掉
    setTimeout(() => {
        loading.classList.remove('show');

        // 這邊計時0.3秒後會讓page部分+1也就是會在往下生成下一頁五個posts會產生
        setTimeout(() => {
            page++;
            showPosts();
        }, 300);
    }, 1000);
}

//篩選input輸入的內容(filter posts by input)
function filterPosts(e) {

    //要驗證的內容轉大寫比較方便
    const term = e.target.value.toUpperCase();
    const posts = document.querySelectorAll('.post');

    // 一樣為了驗證title,body全部轉大寫
    posts.forEach(post => {
        const title = post.querySelector('.post-title').innerText.toUpperCase();
        const body = post.querySelector('.post-body').innerText.toUpperCase();

        // 判斷式使用indexOf判斷書入的內容term是否在title以及body裡面找不找的到，大於-1表示有找到則顯示原本的flex元素沒有則顯示none
        if (title.indexOf(term) > -1 || body.indexOf(term) > -1) {
            post.style.display = 'flex';
        } else {
            post.style.display = 'none';
        }
    });
}


//在post-container區域貼上取得的posts(show initial posts)
showPosts();


//event listener

window.addEventListener('scroll', () => {

    //這邊因為作者不想一直打document.documentElement這段所以做解構
    //把這三個方法從其中拿出來直接做變數指派
    const {
        scrollTop,
        scrollHeight,
        clientHeight
    } = document.documentElement;

    //scrollTop是顯示從最上方到滑到的位置的距離
    //scrollHeight是posts的height
    //clientHeight回傳元素內部高度

    //一般來說scrollHeight = scrollTop + clientHeight
    // 所以當往下滑的距離超過原本卷軸也就是srollHeight 5的時候會觸發產生新的posts
    //不一定要放五放一也可以
    console.log(document.documentElement.scrollTop);
    if (scrollTop + clientHeight >= scrollHeight - 5) {
        showLoading();
    }
});

// 當filter被輸入內容就會觸發filterPosts function
filter.addEventListener('input', filterPosts);
```
