---
title: JS-Async JS Crash Course
date:
tags: Javascript
category: Javascript
---


# Async JS Crash Course 

---
tags: Javascript relate
---

###### tags: `Javascript`




# 使用範例來理解Async JS在什麼情況下適合作用:

* 取得post貼上DOM延遲一秒鐘
* 創造新的post花了兩秒鐘

這樣會發生什麼情況?

![](https://i.imgur.com/lW6aV3a.png)

DOM會先PO post上去不等新的post創造好，所以永遠更新不到新的post


```javascript=
const posts = [{
        title: 'Post One',
        body: 'This is post one'
    },
    {
        title: 'Post Two',
        body: 'This is post two'
    },
];


// 把取得的post貼到DOM上面 延遲一秒鐘
function getPost() {
    setTimeout(() => {
        let output = '';
        posts.forEach((post, index) => {
            output += `<li>${post.title}</li>`;
        });
        document.body.innerHTML = output;
    }, 1000);
}

//創造一個新的post丟上去花了兩秒鐘
function createPost(post) {
    setTimeout(() => {
        posts.push(post);
    }, 2000);
}

getPost();

createPost({
    title: 'Post Three',
    body: 'This is post Three'
});
```

# 使用callback:

使用callback代表getPosts，這樣一來就會在創造好新的post之後才會觸發getPosts整個過程會在兩秒內完成

需要注意callback的寫法在呼叫函式的部分撰寫的callback不需要加上()要特別留意
```javascript=
//創造一個新的post丟上去花了兩秒鐘
//這邊的callback就代表了getPosts所以必須等創造好了新的post之後
// getPost才會觸發也才會把取的的物件推上去DOM所以就可以顯示新的post搂!
function createPost(post, callback) {
    setTimeout(() => {
        posts.push(post);
        callback();
    }, 2000);
}

createPost({
    title: 'Post Three',
    body: 'This is post Three'
}, getPosts)
```

# 使用promise:

* promise解決會呼叫resolve
* promise錯誤則呼叫reject

promise成功則會使用then()內部的函式順利的印出新的post
![](https://i.imgur.com/Vc1kOWO.png)

promise失敗(改寫error變數成true)則會顯示錯誤訊息在console裡面
也可以使用`catch`方法抓取錯誤的內容
![](https://i.imgur.com/s18nYiL.png)


```javascript=
function createPost(post, ) {

    //如果promise解決會呼叫resolve
    //如果promise錯誤則呼叫reject
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            posts.push(post);

// 解釋promise內部的兩個參數的判斷是如何運作
            const error = false;

            if (!error) {
                resolve();
            } else {
                reject('Error: something went wrong');
            }

        }, 2000);
    });
}

createPost({
        title: 'Post Three',
        body: 'This is post three'
    }).then(getPosts).catch(err => console.log(err));
```

## 示範promise.all

常常promise會不只一個，一個一個接then太累了，所以可以使用promise.all一次抓住一同使用.then就好瞜!

```javascript=
const promise1 = Promise.resolve('hello world');
const promise2 = 10;
const promise3 = new Promise((resolve, reject) => setTimeout(resolve, 2000, 'Goodbye'));

Promise.all([promise1, promise2, promise3]).then(values => console.log(values));
```

最後.then的印出結果
![](https://i.imgur.com/9yQSz0L.png)


## 示範fetch API 相關的promise寫法

使用fetch抓取資料的話必須轉化格式所以在指派給變數的階段就要先.then轉換格式

這樣才可以在promise.all的階段被真正抓取到資料

```javascript=
//使用兩個.then因為要轉換JSON格式
const promise4 = fetch('https://jsonplaceholder.typicode.com/users').then(res => res.json());

Promise.all([promise1, promise2, promise3, promise4]).then(values => console.log(values));
```
最後.then的印出結果
![](https://i.imgur.com/8fI5g5T.png)


## 使用async:

`await` 等待一個同步的過程或動作去完成後才去執行其他動作

等待createPost處理完內部的函式createPost後也就是創造新的post後，才會往getPosts去執行這樣就會顯示摟!

```javascript=
function createPost(post, ) {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            posts.push(post);

            const error = false;

            if (!error) {
                resolve();
            } else {
                reject('Error: something went wrong');
            }

        }, 2000);
    });
}

// 等待createPost處理完成後，才會往getPosts去執行
async function init() {
    await createPost({
        title: 'Post Three',
        body: 'This is post three'
    });

    getPosts();
}

init();
```

## 示範fetch API 相關的async寫法

不只用.then一切都更乾淨好讀

一樣fetch都需要資料轉換，但是這邊從新指派一個變數處理比較特別

```javascript=
async function fetchUsers() {
    const res = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await res.json();

    console.log(data);
}

fetchUsers();
```

fetch的資料印出:
![](https://i.imgur.com/Xc4q0xs.png)
