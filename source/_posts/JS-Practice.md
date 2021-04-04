---
title: JS-Practice (5000字)
date:
tags: Javascript
category: Javascript
---

#  JS Practice

---
tags: Javascript relate
---

###### tags: `Javascript`

# 製作一個紅綠燈

## 成品:

![](https://i.imgur.com/OlFszR9.gif)


[成品網址]()

## 成品功能:

1. 預設起始點是亮紅燈
2. 每秒換一個燈色
3. 循環順序是紅 => 黃 => 綠

# HTML

HTML很單純的顯示三個圓圈跟紅綠燈的身體
比較特殊的是color屬性

## html程式碼:

```htmlembedded=
<body>
    <div class="container">
        <div class="circle red" color="red"></div>
        <div class="circle" color="yellow"></div>
        <div class="circle" color="green"></div>
    </div>
</body>
```


# CSS:

.circle:after 處理立體感燈泡

* 使用after創造出來的block
* 把after的background-color:red 先設定出來比較好處理
* 右側用border-right做出粉紅色的邊邊來當作陰影(紅色箭頭處)
* 再使用borderj-radius後就會呈現半月形狀
* 最後去除掉background-color:red就可以得到立體感的燈泡!
![](https://i.imgur.com/qmNsp0u.png) => ![](https://i.imgur.com/qulDZo1.png) => ![](https://i.imgur.com/eECGhCM.png)





## CSS完整程式碼

```css=
 * {
    box-sizing: border-box;
}

body {
    background-color: #1abc9c;
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    margin: 0;
}

.container {
    height: 200px;
    width: 70px;
    background-color: #2c3e50;
    border-radius: 50px;
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    align-items: center;
    padding: 15px;
}

.circle {
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 50%;
    position: relative;
    height: 40px;
    width: 40px;
}

.circle:after {
    content: "";
    width: 30px;
    height: 30px;
    position: absolute;
    border-right: 4px solid rgba(255, 255, 255, 0.6);
    border-radius: 50%;
    top: 5px;
}

.circle.red {
    background-color: #c0392b;
    box-shadow: 0 0 20px 5px #c0392b;
}

.circle.yellow {
    background-color: #f1c40f;
    box-shadow: 0 0 20px 5px #f1c40f;
}

.circle.green {
    background-color: #2ecc71;
    box-shadow: 0 0 20px 5px #2ecc71;
}
```

# JS:


## 變數設置

```javascript=
const circles = document.querySelectorAll('.circle');
```

![](https://i.imgur.com/r9DR7KE.png)

```javascript=
let activeLight = 0;
```
```javascript=
const currenLight = circles[activeLight];
```

* activeLight代表circle的index
* circles[activeLight]就是顯示當前亮甚麼燈號

![](https://i.imgur.com/SgbZy1k.png)





## functions:

* `setInterval()` - 每秒執行一次更換燈號
* `changeLight()` - 因為基礎燈號一開設置在red燈，所以程式開頭先把當前的class轉回circle也就是代表熄燈，隨後增加circle的index號碼因為要讓燈號跑到下一個，接下來做if判斷式讓index跑到底時，可以繞回 0也就是回到紅燈，最後把當前的燈號currenLight的class加上 對應的div 屬性 也就是加上color內的內容，就可以切換到下一個燈號了

步驟:

1. 把當前燈號關閉(轉換class回到circle)
2. 把index號碼往前進`activeLight++;`
3. if判斷式處理當index號碼超過2時要回到0
4. 把上面index已經往前的號碼填入circle[]抓取currentLight當前亮的燈號
5. 抓好後處理他的class抓取當前燈號div的 color屬性也就是對應的顏色(red, yellow, green)

## JS完整程式碼:
```javascript=
const circles = document.querySelectorAll('.circle');
let activeLight = 0;

setInterval(changeLight, 1000);

function changeLight() {

    // 預設值是亮紅燈這行的用處在於取消red的class變回circle
    // circles[0] = red
    circles[activeLight].className = 'circle';
    activeLight++;

    if (activeLight > 2) {
        activeLight = 0;
    }

    const currenLight = circles[activeLight];
    currenLight.classList.add(currenLight.getAttribute('color'));
}
```





# 製作一個老爸笑話產生器

## 成品:

![](https://i.imgur.com/3L2rtUc.png)


[成品網址]()

## 成品功能:

1. 點擊Get Another joke就會取得一則新的笑話

# HTML

* 容器包住全部
* h3
* div 裡面處理js產生笑話
* 按鈕

## html程式碼:

```htmlembedded=
<div class="container">
        <h3>Don't laugh challenge</h3>
        <div id="joke" class="joke">
            //here goes the joke
        </div>
        <button id="get_joke" class="btn">
            Get Another Joke
        </button>
</div>
```


# CSS:

* 簡單修飾容器不多作介紹

## CSS完整程式碼

```css=
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

* {
    box-sizing: border-box;
}

body {
    background-color: #686de0;
    font-family: 'Muli', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

.container {
    background-color: #fff;
    border-radius: 10px;
    padding: 50px 20px;
    text-align: center;
    max-width: 100%;
    width: 800px;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1), 0 6px 6px rgba(0, 0, 0, 0.1);
}

h3 {
    margin: 0;
    letter-spacing: 2px;
    opacity: 0.5;
}

.joke {
    font-size: 30px;
    line-height: 40px;
    margin: 50px auto;
    max-width: 600px;
}

.btn {
    background-color: #9f68e0;
    border: 0;
    border-radius: 10px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1), 0 6px 6px rgba(0, 0, 0, 0.1);
    color: #fff;
    padding: 14px 40px;
    font-size: 16px;
    cursor: pointer;
}

.btn:active {
    transform: scale(0.98);
}

.btn:focus {
    outline: 0;
}
```

# JS:

## API

[icanhazdadjoke API位置以及使用說明](https://icanhazdadjoke.com/api)


因為我們要使用JSON格式

![](https://i.imgur.com/HdHkok2.png)



## 變數設置

```javascript=
const jokeEl = document.getElementById('joke');
```
![](https://i.imgur.com/OIMbsYD.png)

```javascript=
const get_joke = document.getElementById('get_joke');
```
![](https://i.imgur.com/oEboUWY.png)

```javascript=
const joke = await jokeRes.json();
```
fetch回來的資料裡面的joke就是要取用的部分
![](https://i.imgur.com/k2II9Tb.png)


## functions:

* `generateJoke()`

1. jokeRes 變數等待fetch回傳的資料
2. joke 變數等待jokeRes從json格式轉回來得到下圖內容並且使用joke.joke取用後

![](https://i.imgur.com/e0Crd1A.png)

3. 最後貼上jokeEl的HTML上面

## 事件監聽

```javascript=
get_joke.addEventListener('click', generateJoke);
```

點擊觸發`generateJoke()`產生笑話

## JS完整程式碼:
```javascript=
const jokeEl = document.getElementById('joke');
const get_joke = document.getElementById('get_joke');

get_joke.addEventListener('click', generateJoke);

async function generateJoke() {
    // call the icanhaz API
    const jokeRes = await fetch('https://icanhazdadjoke.com/', {
        headers: {
            'Accept': 'application/json'
        }
    });

    const joke = await jokeRes.json();

    console.log(joke);
    //set the new joke to
    jokeEl.innerHTML = joke.joke;
}
```








# 製作一個動畫旋轉圈圈

## 成品:

![](https://i.imgur.com/zpADG4D.gif)


[成品網址]()

## 成品功能:



# HTML

要幾個圈圈可以自訂

## html程式碼:

```htmlembedded=
<body>
    <div class="container">
        <div class="circle"></div>
        <div class="circle"></div>
        <div class="circle"></div>
    </div>
</body>
```


# CSS:

* body部分做全置中
* container做一開始的定位(把半圓轉到上面)
* 使用border做出直線(dashed)，之後使用`border-radius:50%`成圓形
* 這兩個屬性作出半圓來
(border-top-color: #fff;
border-right-color: #fff;)
* box-shadow讓每個圓有邊框

(沒有做box-shadow的話會長這樣全部黏在一起)
![](https://i.imgur.com/yzS5ec7.png)

(做出box-shado之後的效果)
![](https://i.imgur.com/d9zoVO0.png)

* `transform: translate(-50%, -50%)`為了讓圓形置中到圓心


## 讓半圓轉起來

下方是示範使用CSS來寫如何讓讓半圓轉起來
針對每一圈的border做處理

* 修改大小
* 修改旋轉角度，這邊很有趣因為每一圈都是以360deg的倍數所以一定會一瞬間是所有半圓都會聚集變回半圓，也算是這個特效的看點
* 很重要的部分`transform: translate(-50%, -50%)`的全置中效果一樣必須寫進來不能只寫rotate進去@keyframes裡面不然特效會跑掉

```css=
 .circle:nth-of-type(1) {
    border: 50px dashed #111;
    border-top-color: #fff;
    border-right-color: #fff;
    animation: rotateA 3s ease-in-out infinite;
}

@keyframes rotateA {
    to {
        transform: translate(-50%, -50%) rotate(360deg);
    }
}

.circle:nth-of-type(2) {
    border: 40px dashed #111;
    border-top-color: #fff;
    border-right-color: #fff;
    animation: rotateB 3s ease-in-out infinite;

}

@keyframes rotateB {
    to {
        transform: translate(-50%, -50%) rotate(720deg);
    }
}

.circle:nth-of-type(3) {
    border: 30px dashed #111;
    border-top-color: #fff;
    border-right-color: #fff;
    animation: rotateC 3s ease-in-out infinite;

}

@keyframes rotateC {
    to {
        transform: translate(-50%, -50%) rotate(1080deg);
    }
} 
```


## CSS完整程式碼

```css=
body {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

.container {
    position: relative;
    transform: rotate(135deg)
}

.circle {
    border-radius: 50%;
    border: 60px dashed #111;
    border-top-color: #fff;
    border-right-color: #fff;
    box-shadow: 0 0 0 2px #fff;
    position: absolute;
    top: 50%;
    left: 50%;
    width: 0;
    height: 0;
    transform: translate(-50%, -50%) rotate(0deg);
    animation: rotate 7s ease-in-out infinite;
}
```

# JS:


## 變數設置

```javascript=
const circles = document.querySelectorAll('.circle');
```
![](https://i.imgur.com/wqDg92e.png)

```javascript=
const style = document.createElement('style');
```
輸出在body內修飾半圓內部填入`@keyframes`

```javascript=
const deg = (idx + 1) * 360;
```
deg代表每圈的旋轉角度


## forEach:

### forEach的輸出結果:

利用forEach輸出circle的index的方式處理下面三個屬性:

* border-widht
* z-index
* animation-name

![](https://i.imgur.com/7DJvsSj.png)

### keyframes的輸出結果:

* translate的部分就固定
* 主要使用idx更改旋轉角度`const deg = (idx + 1) * 360;`

![](https://i.imgur.com/4rq2d5Q.png)


## JS完整程式碼:
```javascript=
const circles = document.querySelectorAll('.circle');
const style = document.createElement('style');
let styleInner = '';

circles.forEach((circle, idx) => {
    circle.style.borderWidth = (idx + 1) * 10 + 'px';
    circle.style.zIndex = -idx;
    circle.style.animationName = `rotate-${idx}`;

    const deg = (idx + 1) * 360;

    const style = document.createElement('style');
    styleInner += `
		@keyframes rotate-${idx} {
			to {
				transform: translate(-50%, -50%) rotate(${deg}deg);
			}
		}
	`;
});

style.innerHTML = styleInner;
document.body.appendChild(style);
```


# 製作一個進度條

## 成品:

![](https://i.imgur.com/bBORPz2.gif)


[成品網址]()

## 成品功能:

* 當頁面刷新時會更新進度條

# HTML

* 這邊的data-done是給JS做選取使用

## html程式碼:

```htmlembedded=
<div class="progress">
        <div class="progress-done" data-done="70">
            70%
        </div>
    </div>
```


# CSS:

* 漸層色的處
左邊的顏色會顯示在右邊，反之亦然
* 在JS處理
opacity顯示0
width顯示0

```css=
background: linear-gradient(to left, #f2709c(顯示在右側), #ff9472);
```

## CSS完整程式碼

```css=
@import url('https://fonts.googleapis.com/css?family=Montserrat&display=swap');

* {
    box-sizing: border-box;
}

body {
    font-family: 'Montserrat', sans-serif;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

.progress {
    height: 30px;
    width: 300px;
    background-color: #d8d8d8;
    border-radius: 20px;
}

.progress-done {
    height: 100%;
    width: 0;
    color: #fff;
    box-shadow: 0 3px 3px -5px #f2709c, 0 2px 5px #f2709c;
    background: linear-gradient(to left, #f2709c, #ff9472);
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: 1s ease;
}
```

# JS:


* 藉由html設定好的data-done由JS讀其值後動態呈現width
* 並且更改opacity為1

![](https://i.imgur.com/XNCVd6X.png)


## 變數設置

內部進度條的部分
![](https://i.imgur.com/DP46VDz.png)


## JS完整程式碼:
```javascript=
const progress = document.querySelector('.progress-done');

setTimeout(() => {
    progress.style.width = progress.getAttribute('data-done') + '%';

    progress.style.opacity = 1;
}, 500)
```


# 製作一個下雪背景

## 成品:

![](https://i.imgur.com/srk8m46.gif)


[成品網址]()

## 成品功能:

* 背景會下雪
* 雪花位置、大小、景深都隨機


# HTML

* 需要引入fontawesome
* 雪花會從JS製造

## html程式碼:

```htmlembedded=
<script src="https://kit.fontawesome.com/2ae9e2b502.js" crossorigin="anonymous"></script>
<body>
</body>
```


# CSS:

* 使用絕對定位因為會在JS設定位置
* animation使用forwards表示動畫結會停在結束的狀態
* translateY設定105vh要展示出從螢幕上方掉下來所以設定超出視窗

## CSS完整程式碼

```css=
body {
    background: #323975;
}

.fa-snowflake {
    color: #fff;
    position: absolute;
    animation: fall linear forwards;
}

@keyframes fall {
    to {
        transform: translateY(105vh);
    }
}
```

# JS:


## 變數設置

抓取創造的雪花
```javascript=
const snow_flake = document.createElement('i');
```

## functions:

`createSnowFlake()`
* 創造出i tag後加上class讓它可以吃到css的修飾
* Math.random()會產出 0~1之間的小數
* 讓雪花的位置隨機 innerwidth乘上Math.random()代表雪花出現的寬度介在0~整個瀏覽器的寬度
* 讓雪花持續時間隨機 因為我們設定setTimeout為五秒所以最少持續兩秒最多五秒
* 透明度以及雪花大小 透明度就直接random很方便; 大小的部份讓他們保持在10~20之間不要大的太誇張

## JS完整程式碼:
```javascript=
setInterval(createSnowFlake, 50);

function createSnowFlake() {
    const snow_flake = document.createElement('i');
    snow_flake.classList.add('fas');
    snow_flake.classList.add('fa-snowflake');
    snow_flake.style.left = Math.random() * window.innerWidth + `px`;
    snow_flake.style.animationDuration = Math.random() * 3 + 2 + `s`; //數字會介於2~5之間
    snow_flake.style.opacity = Math.random(); //給的數字會介於1~0之間 做景深相關的特效
    snow_flake.style.fontSize = Math.random() * 10 + 10 + `px`; //做出不同大小

    document.body.appendChild(snow_flake);

    setTimeout(() => {
        snow_flake.remove();
    }, 5000)
}
```




# 製作一個神奇寶貝圖鑑

## 成品:

![](https://i.imgur.com/zJTLZQn.png)



[成品網址]()

## 成品功能:

1. 依照圖鑑順序顯示神奇寶貝
2. 針對不同屬性呈現不同顏色
3. 有RWD效果

# HTML

基本上都是藉由JS產生所以的div

## html程式碼:

```htmlembedded=
<body>
    <h1>PokeDex</h1>
    <div id="poke_container" class="poke-container"></div>
</body>
```


# CSS:

* pokemon-contaienr
使用flex-wrap:wrap是整個排版的重點讓圖鑑可以分行排版
並且全置中

* .pokemon .img-container img
為了使用RWD使用`max-width: 90%;`也代表父母層的90%也就是120px*0.9=108



## CSS完整程式碼

```css=
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');
@import url('https://fonts.googleapis.com/css?family=Lato:300,400&display=swap');

* {
    box-sizing: border-box;
}

body {
    background: #EFEFBB;
    background: linear-gradient(to right, #D4D3DD, #EFEFBB);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    font-family: 'Lato';
    margin: 0;
}

h1 {
    letter-spacing: 3px;
}

.poke-container {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    max-width: 1200px;
}

.pokemon {

/*     這邊的背景色是因為修飾使用做好JS後可以刪除 */
    background-color: #eee;
    border-radius: 20px;
    box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
    margin: 10px;
    padding: 20px;
    text-align: center;
}

.pokemon .img-container {
    background-color: rgba(255, 255, 255, 0.6);
    border-radius: 50%;
    width: 120px;
    height: 120px;
    text-align: center;
}

.pokemon .img-container img {
    margin-top: 20px;
    max-width: 90%;
}

.pokemon .info {
    margin-top: 20px;
}

.pokemon .number {
    background-color: rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    font-size: 0.8em;
    padding: 5px 10px;
}

.pokemon .name {
    margin: 15px 0 7px;
    letter-spacing: 1px;
}
```

# JS:


## 變數設置

### 全域變數
* poke_container
![](https://i.imgur.com/0EZjDSP.png)

* pokemons_number = 150
主要使用在要逐個印出神奇寶貝的`fetchPokemons()`函式裡

* main_types
取出物件colors裡面的key值

* colors
設置不同屬性的神奇寶貝不同的顏色

### getPokemon()內部變數
* url
名字跟屬性的來源

* res
回傳回來的url 資料
* pokemon
轉檔成json使用並且傳入`createPokemonCard(pokemon);`

### createPokemonCard()內部變數

* pokemonEl
![](https://i.imgur.com/tLgjn6F.png)

* poke_types
使map逐個印出每個神奇寶貝的types名稱
![](https://i.imgur.com/xusdD57.png)

* name 
為了讓名字第一個字可以大寫所以使用name[0]抓取第一個字並且使用toUppercase()
並且串接上name.slice(1)也就是切掉第一個字母的單字就完成瞜!

* type
使用find()來回傳第一個找到的值並填入color給不同總類的神奇寶貝上不同背景色

* color
使用find()來回傳第一個找到的值並填入color給不同總類的神奇寶貝上不同背景色

* pokeInnerHTML
整個要印出在DOM上面的html架構

## functions:

* `getPokemon()`
從API擷取資下來並且傳入createPokemonCard中

* `fetchPokemons()`
逐個擷取並且印出getPokemon()得到的資料

* `createPokemonCard()`
1. 創造div並加上class
1. 取得神奇寶貝的type並且嵌入color使顏色隨屬性呈現
1. 實際HTML內的撰寫並填入相應的API內容
1. 把HTML填入pokemonEl
1. 把poke_contaienr填入最後完成pokemonEl

使用`pokemon.id.toString().padStart(3,"0")`
讓神奇寶貝編碼變成三位數
`padStart(3,"0")` 代表把內容物填充到三位數並且從0開頭(ex. 001,002,003)



## JS完整程式碼:
```javascript=
const poke_container = document.getElementById('poke_container');
const pokemons_number = 150;
const colors = {
    fire: '#FDDFDF',
    grass: '#DEFDE0',
    electric: '#FCF7DE',
    water: '#DEF3FD',
    ground: '#f4e7da',
    rock: '#d5d5d4',
    fairy: '#fceaff',
    poison: '#98d7a5',
    bug: '#f8d5a3',
    dragon: '#97b3e6',
    psychic: '#eaeda1',
    flying: '#F5F5F5',
    fighting: '#E6E0D4',
    normal: '#F5F5F5'
};

const main_types = Object.keys(colors);

// console.log(main_types);

const fetchPokemons = async () => {
    for (let i = 1; i < pokemons_number; i++) {
        await getPokemon(i);
    }
}

const getPokemon = async id => {
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
    const res = await fetch(url);
    const pokemon = await res.json();
    createPokemonCard(pokemon);
}

fetchPokemons();

function createPokemonCard(pokemon) {
    const pokemonEl = document.createElement('div');
    pokemonEl.classList.add('pokemon');

    const poke_types = pokemon.types.map(el => el.type.name);
    const name = pokemon.name[0].toUpperCase() + pokemon.name.slice(1);

    const type = main_types.find(type => poke_types.indexOf(type) > -1);
    const color = colors[type];
    pokemonEl.style.backgroundColor = color;


    const pokeInnerHTML = `
    <div class="img-container">
        <img src="https://pokeres.bastionbot.org/images/pokemon/${pokemon.id}.png" alt =${name}>
    </div>
    <div class="info">
        <span class="number">#${pokemon.id.toString().padStart(3,"0")}</span>
        <h3 class="name">${name}</h3>
        <small class="type">Type: <span>${type}</span></small>
    </div>
    `;

    pokemonEl.innerHTML = pokeInnerHTML;
    poke_container.appendChild(pokemonEl);
}
```

# 製作一個網頁瀏覽計數器

## 成品:

![](https://i.imgur.com/abnaxsW.png)


[成品網址]()

## 成品功能:

1. 當頁面重整時會更新瀏覽次數


# HTML



## html程式碼:

```htmlembedded=
<body>
    <p>This page has</p>
    <h1 id="count">0</h1>
    <p>views</p>
</body>
```


# CSS:

簡單的置中以及上色

## CSS完整程式碼

```css=
@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

* {
    box-sizing: border-box;
}

body {
    background-color: #192a56;
    color: #fff;
    font-family: 'Muli', sans-serif;
    flex-direction: column;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    margin: 0;
}

h1 {
    font-size: 50px;
    margin: 0;
}

p {
    color: rgba(255, 255, 255, 0.8);
    letter-spacing: 2px;
    margin: 0;
}
```

# JS:

[count API官網](https://countapi.xyz/)

參考這邊的參數設置要使用的API
![](https://i.imgur.com/UklBjL9.png)

第一步 先設置namespace的名稱
`https://api.countapi.xyz/create?namespace=mysite.com&value=42`

第二步 設置key以及value為0
`https://api.countapi.xyz/create?namespace=mysite.com&key=mykey&value=0`

第三步 修改狀態為update並輸入amount=1
`https://api.countapi.xyz/update/mysite.com/mykey/?amount=1`

就可以開始使用此API瞜!

## 變數設置

* countEl
![](https://i.imgur.com/6Zw9v81.png)


## functions:

`updateVisitCount()`

* 把剛剛創建的API使用fetch抓取
* 擷取api內容從JSON轉換回來並且貼上HTML

## JS完整程式碼:
```javascript=
const countEl = document.getElementById('count');

function updateVisitCount() {
    fetch('https://api.countapi.xyz/update/github/githubBlog/?amount=1')
        .then(res => res.json())
        .then(res => {
            console.log(res);
            countEl.innerHTML = res.value;
        })
}

updateVisitCount();
```


