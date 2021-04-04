---
title: JS-正則表達式 Regular Expression
date:
tags: Javascript
category: Javascript
---

# 正則表達式 Regular Expression

---
tags: Javascript relate
---

###### tags: `Javascript`


# JS 與 Regular Expression

## 01 正則表達式是什麼 ? JS 中如何使用 ?

* 做字串模式的判斷
* 做格式的過濾如電話、email、身分證
* 登入資料判讀、擷取
* 電子試算表資料擷取
* 單據檔案資料擷取

## 正則表達式的呈現:
![](https://i.imgur.com/7zh7HJL.png)


# Regular Expression 學習資源

[學習網站](https://regexone.com/)

## Lesson 1: An Introduction, and the ABCs

輸入符合全部text的pattern:

三個text都包含了abc

```
Task	Text	 
Match	abcdefg	To be completed
Match	abcde	To be completed
Match	abc

input: abc
```

## Lesson 1½: The 123s

輸入符合全部text的pattern，因此除了字母會符合，數字也可以:

三個text都包含123

```
Task	Text	 
Match	abc123xyz	To be completed
Match	define "123"	To be completed
Match	var g = 123;

input: 123 / \D*123\D*
```

## Lesson 2: The Dot(.)萬用字元

題目要吻合前三個text並且讓最後一個task被跳過，所以使用跳脫字元(\)在最後一個(.)之前

wildcard(通用字元)也就是Dot(.)
跳脫字元(\)

```
Task	Text	 
Match	cat.	Success
Match	896.	Success
Match	?=+.	Success
Skip	abc1

input: ...\.
```

## Lesson 3: Matching specific characters(符合特定字元)


[]內部可以放入想要抓取的字元

前三個task符合後三個跳過:

使用中括號([])包含的字元會被特別抓取出來除此之外則跳過

例如[abc]只會抓取符合單一a,b,c沒有其他的


```
Task	Text	 
Match	can	Success
Match	man	Success
Match	fan	Success
Skip	dan	To be completed
Skip	ran	To be completed
Skip	pan

input: [cmf]
```


## Lesson 4: Excluding specific characters(排除特定字元)


排除特定字元

[^abc]會符合任何字元除了a,b,c

```
Task	Text	 
Match	hog	Success
Match	dog	Success
Skip	bog

input: [^b]og
```

## Lesson 5: Character ranges(字元的範圍)

\w代表所有字母數字的集合
\W代表非字母數字的集合

使用中括號[] 以及 (-)代表range
使用[A-C]選出前三個符合下三個完全沒有ABC所以被篩掉了

```
Task	Text	 
Match	Ana	Success
Match	Bob	Success
Match	Cpc	Success
Skip	aax	To be completed
Skip	bby	To be completed
Skip	ccz

input: [A-C][n-p][a-c]
```

## Lesson 6: Catching some zzz's(擷取重複的字元)

擷取重複的字元

使用 要擷取的字元{數字}

例如下面的題目擷取z 3次 以及 5次  z{3,5}

```
Task	Text	 
Match	wazzzzzup	Success
Match	wazzzup	Success
Skip	wazup

input: waz{3,5}up
```

## Lesson 7: Mr. Kleene, Mr. Kleene

(*) 0個或是更多重複

(+) 1個或是更多重複

這兩者都可以使用在任何字元或是元字符 (Metacharacter)上面

> 在POSIX擴展正則表達式裡[1]，定義了14個元字符，它們被作為一般的字符使用時，必須要通過「轉義」（前面加一個反斜槓「\」）來去除他們本身的特殊意義，這些元字符包括：
> 
> 開和閉方括號："["和"]"
> 反斜線："\"
> 脫字符："^"
> 美元符號："$"
> 句號/點："."
> 豎線/管道符："|"
> 問號："?"
> 星號："*"
> 加號："+"
> 開和閉 花括號："{"和"}"
> 開和閉 小括號："("和")"[2][3]

下方範例可以看到:

a+ 代表 a是一個以上
b* 代表 b可以包含0以及以上
c+ 代表 c是一個以上

```
Task	Text	 
Match	aaaabcc	Success
Match	aabbbbc	Success
Match	aacc	Success
Skip	a

input: a+b*c+
```

## Lesson 8: Characters optional(?)選擇性符號

範例:

ab?c => abc or ac (b是選擇性的)


中括號124抓取前三個數字 跳過skip

並且使用?讓s變成選擇性的

最後跳脫字元?


```
Task	Text	 
Match	1 file found?	Success
Match	2 files found?	Success
Match	24 files found?	Success
Skip	No files found.

input: [124]+files? found\?
```

## Lesson 9: All this whitespace(空白符號)

* space (␣)使用space產生的空白
* tab (\t)使用tab產生的空白
* new line (\n)斷行
* carriage return (\r) 很少使用只有在character terminal
* whitespace special character (\s) 此功能包含以上全部的空白
* (\S)任何不是空格的字元


這邊我的解法是

使用數字符號
代表第一個數字 \d

使用跳脫字元加上dot \.代表順序後方的dot

接下來就是\s代表全部的空白處

最後是abc


```
Task	Text	 
Match	1.   abc	Success
Match	2.	abc	Success
Match	3.           abc	Success
Skip	4.abc	To be completed

input: \d\.\s+abc
```

## Lesson 10: Starting and ending (搜尋完整的字句)


使用 ^...$ 可以包含要搜尋的完整字句

```
Task	Text	 
Match	Mission: successful	Success
Skip	Last Mission: unsuccessful	To be completed
Skip	Next Mission: successful upon capture of target

input: ^Mission: successful$
```

## Lesson 11: Match groups (()) (限定要抓取的範圍)

使用(以及)限定要抓取的範圍

例如:

^(IMG\d+\.png)$
這樣使用會抓取所以有的 IMG數字.png

如果想要只抓取檔案名稱可以這樣寫:

^(IMG\d+)\.png$ 
用()去框在名字的地方限定抓取的範圍只能檔案名稱


```
Capture	file_record_transcript.pdf	file_record_transcript	Success
Capture	file_07241999.pdf	file_07241999	Success
Skip	testfile_fake.pdf.tmp

input: ^(file.+)\.pdf$
```

## Lesson 12: Nested groups(巢狀擷取)

巢狀擷取

一樣使用括號(())來擷取內容，可以用多層的方式擷取內容中的內容

範例:

^(IMG(\d+))\.png$
這邊會擷取IMG的數字.png然後再擷取只有數字的部分

```
Task	Text	Capture Groups	 
Capture	Jan 1987	Jan 1987 1987	Success
Capture	May 1969	May 1969 1969	Success
Capture	Aug 2011	Aug 2011 2011	Success

input: ^(\D+(\d+))$ or ^(\w+(\d+))$
```

## Lesson 13: More group work

中間多了一個字母一樣要抓取他其他的部份用括號擷取

```
Task	Text	Capture Groups	 
Capture	1280x720	1280 720	Success
Capture	1920x1600	1920 1600	Success
Capture	1024x768	1024 768	Success

input: ^((\d+)[x](\d+))$ or ^((\d+)x(\d+))$
```

## Lesson 14: It's all conditional(|)


當作or使用即可(|)


```
Task	Text	 
Match	I love cats	Success
Match	I love dogs	Success
Skip	I love logs	To be completed
Skip	I love cogs

input: I love cats|dogs
```

## Lesson 15: Other special characters(其他特殊字元)


* \d 所有數字
* \s 所有空白字元
* \w 所有數字、字母
-----
* \D 所有字母
* \S 所有非空白字元
* \W 所有非數字、字母


\b 所有單詞


這邊的練習是個練習用的沙盒可以不用擺上來可以連上去練一下使用regex

[練習網站](https://regexone.com/lesson/misc_meta_characters?)


## YA完成了~第一部分ZZ

![](https://i.imgur.com/cLWvW2l.png)


## Practice Problems


## Problem 1: Matching a decimal numbers (擷取小數)

主要是用[]解的 並且後面加上\d表示數字結尾

```
Match	3.14529	Success
Match	-255.34	Success
Match	128	Success
Match	1.9e10	Success
Match	123,340.00	Success
Skip	720p

input: ^[-\.,\de]+\d$
```


## Problem 2: Matching phone numbers

只抓前三個連號都可以辦到搂!基本上電話區碼的部分可以這樣抓

```
Task	Text	Capture Groups	 
Capture	415-555-1234	415	Success
Capture	650-555-2345	650	Success
Capture	(416)555-3456	416	Success
Capture	202 555 4567	202	Success
Capture	4035555678	403	Success
Capture	1 416 555 9292	416	Success

input: (\d{3})
```

## Problem 3: Matching emails

排除所有符號後方的字元

```
Task	Text	Capture Groups	 
Capture	tom@hogwarts.com	tom	Success
Capture	tom.riddle@hogwarts.com	tom.riddle	Success
Capture	tom.riddle+regexone@hogwarts.com	tom.riddle	Success
Capture	tom@hogwarts.eu.com	tom	Success
Capture	potter@hogwarts.com	potter	Success
Capture	harry@hogwarts.com	harry	Success
Capture	hermione+regexone@hogwarts.com	hermione	Success

input: ^([\w\.]*)
```

## Problem 4: Matching HTML

選取"<"以及後面的字母 就是tag瞜!

ex. <a or <div

```
Capture	<a>This is a link</a>	a	Success
Capture	<a href='https://regexone.com'>Link</a>	a	Success
Capture	<div class='test_style'>Test</div>	div	Success
Capture	<div>Hello <span>world</span></div>	div	Success

input: <(\w+)
```


## Problem 5: Matching specific filenames


| and $的活用

選擇jpg or png or gif $(作為結尾)
```
Skip	.bash_profile		To be completed
Skip	workspace.doc		To be completed
Capture	img0912.jpg	img0912 jpg	Success
Capture	updated_img0912.png	updated_img0912 png	Success
Skip	documentation.html		To be completed
Capture	favicon.gif	favicon gif	Success
Skip	img0912.jpg.tmp		To be completed
Skip	access.lock	

input:(\w+)\.(jpg|png|gif)$
```


## Problem 6: Trimming whitespace from start and end of line


這邊我使用一開始去掉空白之後抓取全部的文字最後抓取串接以(.)結尾的句子

```
Capture				The quick brown fox...	The quick brown fox...	Success
Capture	   jumps over the lazy dog.	jumps over the lazy dog.	Success

input: ([^\s+](.+)\.)$
```


## Problem 7: Extracting information from a log file

(\w+)\( 純文字以及跳脫字元\"("\

[\w\.]+): 這段是抓取所有文字以及有(.)加上一個(:)

(\d+)\)$ 這段是抓取括號以及數字結尾

```
Skip	W/dalvikvm( 1553): threadid=1: uncaught exception		To be completed
Skip	E/( 1553): FATAL EXCEPTION: main		To be completed
Skip	E/( 1553): java.lang.StringIndexOutOfBoundsException		To be completed
Capture	E/( 1553):   at widget.List.makeView(ListView.java:1727)	makeView ListView.java 1727	Success
Capture	E/( 1553):   at widget.List.fillDown(ListView.java:652)	fillDown ListView.java 652	Success
Capture	E/( 1553):   at widget.List.fillFrom(ListView.java:709)	fillFrom ListView.java 709	Success

input: (\w+)\(([\w\.]+):(\d+)\)$
```


## Problem 8: Parsing and extracting data from a URL

(\w+):// 這段吃所有的 ://之前的字母


://([\w\-\.]+) 使用[]內部包含字母、跳脫字元的- .


(:(\d+))?  最後幾個(:)之後的數字因為不是每個都有所以上問號讓它們變成optional


```
Task	Text	Capture Groups	 
Capture	ftp://file_server.com:21/top_secret/life_changing_plans.pdf	ftp file_server.com 21	Success
Capture	https://regexone.com/lesson/introduction#section	https regexone.com	Success
Capture	file://localhost:4040/zip_file	file localhost 4040	Success
Capture	https://s3cur3-server.com:9999/	https s3cur3-server.com 9999	Success
Capture	market://search/angry%20birds	market search	Success

input: (\w+)://([\w\-\.]+)(:(\d+))?
```

## Problem X: Infinity and beyond!


![](https://i.imgur.com/wTERooE.png)
