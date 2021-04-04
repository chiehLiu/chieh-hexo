---
title: 實作練習-JavaScript BookList App
date:
tags: [HTML, CSS, Bootstrap, JavaScript]
category: Javascript作品
---

# JavaScript BookList App (可以加入或刪去物件的清單)

---

## tags: Javascript relate

###### tags: `Javascript`

[跟著做出來的範例](https://chiehLiu.github.io/git-projects/MYBOOKLIST/index.html#)

成本圖:

![](https://i.imgur.com/jMC7v71.png)

## 內容概要

- 三個 input 來做加入書本的動作，輸入內容後會在下方存入它們的資料，並且有刪除的功能，資料可以儲存在網頁上不會被重新整理刷掉
- 會跑出視窗當填寫不完整或是成功執行動作的時候
- 頁面使用簡單的 Bootrap 框架製作
- 有帶入一些 JSON,ES6-class 的元素

## HTML+boostrap:

### 前置作業

使用[fontawesome](https://fontawesome.com/)來做 icon

```htmlembedded=
<script src="https://kit.fontawesome.com/2ae9e2b502.js" crossorigin="anonymous"></script>
```

使用[bootswatch](https://bootswatch.com/yeti/)來做框架這樣就不用處理 CSS 瞜

```htmlembedded=
<linkrel="stylesheet"href="https://bootswatch.com/4/ye``ti/bootstrap.min.css">

```

使用範例:

- h1 裏面包含了 icon 的使用 fa 的部分還有`<i>`tag
- text-primary 是 bootstrap

```htmlembedded=
<h1 class="display-4">
            <i class="fa fa-book-open text-center text-primary"></i> My<span class="text-primary">Book</span>List</h1>
```

## JS

使用 class 建構 Book 這個物件

```javascript=
class Book {
    constructor(title, author, isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
    }
}
```

接下來會分成數個部分來解釋這整份 JS 內容:

- UI class:處理有關 UI 的任務(使用者會看到並且操作的地方)
- Store class:處理 storage 相關任務
- Event:在 list 裡面展示書本
- Event:加入書本
- Event:移除書本

---

### UI class

有關於 UI 的內容會有五個相關的 method 來處理:

#### displayBooks

新增的書本會放在這個區域下方

![](https://i.imgur.com/SY6qf0A.png)

```javascript=
static displayBooKs() {

        //這邊註解的內容是作者用來一開始當作資料庫使用並且呈現在display區域
        //
        // const StoredBooks = [{
        //         title: 'Book One',
        //         author: 'John Doe',
        //         isbn: '3434434',
        //     },
        //     {
        //         title: 'Book Two',
        //         author: 'Jane Doe',
        //         isbn: '45545',
        //     }
        // ];

        //const books = StoredBooks;

        const books = Store.getBooks();
        // 這個部分是Store部分建立好之後直接引用進來的函式呼叫

        books.forEach((book) => UI.addBookToList(book));
    }   //books的部分會出來陣列(array)所以可以使用forEach逐個去使用addBookTodoList這個方法，來呈現被加進來的書本資料
```

#### addBookToList

書本加入 display 區域的"方法"呈現在這部分:

```javascript=
static addBookToList(book) {
        // 在#book-list區域下方新增元素<tr>
        const list = document.querySelector('#book-list');
        const row = document.createElement('tr');


        //新增的內容如下
        row.innerHTML = `
            <td>${book.title}</td>
            <td>${book.author}</td>
            <td>${book.isbn}</td>
            <td><a href="#" class="btn btn-danger btn-sm delete">X</a></td>
        `

        list.appendChild(row);
        // 讓row黏到list下方就是靠這行，appendChild功能是在在列表中添加項目
    }
```

#### clearFields

設定好這個清空功能後在兩個狀態下會清空欄位

- 加入書本成功後會呼叫這個函式動作就會清空欄位詳見(Event: 加入書本)區域
- 重新整理頁面因為預設值為空("")

```javascript=
static clearFields() {
        document.querySelector('#title').value = '';
        document.querySelector('#author').value = '';
        document.querySelector('#isbn').value = '';

    }
```

#### showAlert

一些不熟的方法

[createElement - MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/Document/createElement)

[createTextNode - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/createTextNode)

[appendChild - w3cschool](https://www.w3schools.com/jsref/met_node_appendchild.asp)

[setTimeout - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/setTimeout)

```javascript=
static showAlert(message, className) {
        //創造一個新的div來產生警告視窗
        const div = document.createElement('div');
        // 幫剛剛創造的div加上bootstrap的屬性產生alert視窗跟顏色message以及className的內容會在下方的Event 加入刪除書本處呼叫並且輸入
        div.className = `alert alert-${className}`;
        //這邊是在撰寫加入meassage部分的程式碼使用appendChild方法加入createTextNode的文字內容
        div.appendChild(document.createTextNode(message));


        //這個部分處理alert的位置，先設定好指派變數給container以及form，在使用insertBefore安插東西在...之前的概念
        const container = document.querySelector('.container');
        const form = document.querySelector('#book-form');
        container.insertBefore(div, form)//參數(安插物,安插物後方的元素)
        //Vanish in 3 seconds
        //setTimeout計時器方法=>選取要計時的class之後輸入在時間到之後要執行的方法(remove)最後輸入計時時間(毫秒)
        setTimeout(() => document.querySelector('.alert').remove(), 3000)
    }
```

#### deleteBook

這邊兩個 parentElement 的用意在於位置的關係要砍掉的是`<td>`外面的`<tr>`
![](https://i.imgur.com/0rYVXuv.png)

[contains - w3cschool](https://www.w3schools.com/jsref/met_node_contains.asp)

[classList - MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/Element/classList)

[remove - MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement/remove)

```javascript=
static deleteBook(el) {
        // 看看元素的class有無包含delete(顯然是有的見上方圖片是X按鈕)，有則執行remove
        if (el.classList.contains('delete')) {
            el.parentElement.parentElement.remove();
        }
    }
```

---

### Store class

處理 storage 的方法的 class，(local storage 也就是 browser 除非被刪除不然資料會存在那邊)
並且它不能存 object 只能存 string

#### getBooks

其實就是 return 傳入的書本的 value 陣列

[getItem - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Storage/getItem)

在四個需要抓取書本的地方出現:

- getBooks 方法本身
- UI class displayBooks 要呈現書的地方就抓取了這邊的資料
- addBook 方法內
- removeBook 方法內

```javascript=
static getBooks() {
        let books;
        if (localStorage.getItem('books') === null) {
        //如果loacalStorage抓取books這個鍵的value為空的話值回復一個空的陣列
            books = [];
        } else {
        //如果不為空則回覆取的'books'這個鍵的value
            books = JSON.parse(localStorage.getItem('books'))
        }

        return books;
    }
```

#### addBook

它是功能是在 localStorage 裡面創造鍵與值(key and value)藉由 push 的方式把參數(book)推進去'books'這個陣列裡面

```javascript=
static addBook(book) {
    const books = Store.getBooks();
    books.push(book);
    // push 是在陣列後方加入一個或是多個元素在末端
    localStorage.setItem('books', JSON.stringify(books));
    // setItem(屬性名稱,value(這邊value只能是string所以使用JSON.stringify))
}
```

#### removebook

得先取得已經加入得書的 value，之後根據剛剛的到的資料做做判斷如果符合 isbn 則執行 splice(刪除元素)

```javascript=
static removebook(isbn) {
    //取的書本的value並且assign給books
    const books = Store.getBooks();

    books.forEach((book, index) => {
    //當書本的value傳進來之後，它的陣列index也會傳進來
        if (book.isbn === isbn) {
    //如果書本的isbn是對的話則splice(刪除)index(檢索位置),1個元素就可以完成效果摟!
            books.splice(index, 1)
        }
    });
    //這個部分是reset，因為剛剛刪除完之後再setItem一次重設它的鍵跟值
    localStorage.setItem('books', JSON.stringify(books));
}
```

### 事件監聽(addEventListener)

#### Event: 展示書本在 list 裡面

讓頁面在重整後依舊可以顯示出書本在 list 裡面

[DOMContentLoaded - MDN](https://developer.mozilla.org/zh-TW/docs/Web/Events/DOMContentLoaded)

```javascript=
document.addEventListener('DOMContentLoaded', UI.displayBooKs);
```

#### Event: 加入書本

先抓取整個 input 區域後加入事件監聽在'submit'上，然後使用取得的事件的值(e)，去跑下方判斷式(前提是內容不為空("")

[preventDefault - MDN](https://developer.mozilla.org/zh-TW/docs/Web/API/Event/preventDefault)

[submit_event - MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/submit_event)

```javascript=
// Event: 加入書本

//先抓取整個input區域後加入事件監聽在'submit'上，然後使用取得的事件的值(e)去跑下方的方法跟判斷式
document.querySelector('#book-form').addEventListener('submit', (e) => {

    //prevent actual submit
    //讓他提交後就停止動作
    e.preventDefault();

    //Get form values
    //把取得的值assign給變數給下面做資料驗證
    const title = document.querySelector('#title').value;
    const author = document.querySelector('#author').value;
    const isbn = document.querySelector('#isbn').value;


    //Valadate (資料驗證)
    if (title === '' || author === '' || isbn === '') {
        UI.showAlert('Please fill in all fields', 'danger');
    } else {

        //instantiate book因為book裡面的資料沒有static所以需要實體化(instantiate)
        const book = new Book(title, author, isbn);

        //經過資料驗證後開始呼叫各個靜態方法(static)

        //Add Book to UI
        UI.addBookToList(book);


        //Add book to store

        Store.addBook(book);

        //Show success message

        UI.showAlert('Book Added', 'success')


        //Clear fields
        UI.clearFields();
    }
})
```

#### Event: 移除書本

一樣抓取完 input 區域後設定事件監聽使用取得的值(e)，去呼叫下方的靜態方法

UI 的部分刪除完成後再刪除 Store 的部分重新整理頁面就不會再跑回來瞜

```javascript=
document.querySelector('#book-list').addEventListener('click', (e) => {

    //remove books from UI
    UI.deleteBook(e.target)

    //remove book from store 這段的目的讓刪除的書本不會再重整頁面後再度出現所以要從store裡面刪除
   //e.target的目標是delete button，使用parentElement會到<td>但是目標是要找到isbn所以要找到sibling裡面的textContent
    Store.removebook(e.target.parentElement.previousElementSibling.textContent);

    UI.showAlert('Book Removed', 'success')
})
```
