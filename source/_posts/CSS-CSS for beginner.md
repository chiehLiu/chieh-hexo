---
title: CSS-for beginner
date:
tags: CSS
category: CSS
---

# CSS for beginner
---
tags: HTML CSS relate
---

###### tags: `HTML, CSS`
參考學習資源連結:https://www.htmldog.com/guides/css/beginner/

**CSS(Cascading Styles Sheets) is a way to style and present HTML**


Cascading 

其中一個含意是寫在下面的code會覆蓋掉上面的

![](https://i.imgur.com/kLEaN8L.png)

![](https://i.imgur.com/FEDJlV2.png)


------------


1.Inline CSS(幾乎不太用到)
An inline CSS is used to apply a unique "style" to **a single HTML element**.
**
An inline CSS **uses the style attribute of an HTML element**.

The following example sets the text color of the element to blue, and the text color of the element to red:

```
<h1 style="color:blue;">A Blue Heading</h1>

<p style="color:red;">A red paragraph.</p>
```

------
2.Internal CSS

An internal CSS is used to define a style for a **single HTML page**.

An internal CSS is **defined in the head section of an HTML page**, within a style element.

The following example sets the text color of ALL the h1 elements (on that page) to blue, and the text color of ALL the p elements to red. In addition, the page will be displayed with a "powderblue" background color: 

```
<!DOCTYPE html>
<html>
<head>
<style>
body {background-color: powderblue;}
h1   {color: blue;}
p    {color: red;}
</style>
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

------------

3.External CSS(最重要的用法)

An external style sheet is used to define the style for **many HTML pages**.

To use an external style sheet, **add a link to it in the head section of each HTML page**:

```
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

<h1>This is a heading</h1>
<p>This is a paragraph.</p>

</body>
</html>
```

# Selectors, Properties, and Values



CSS選擇器的組成


![](https://i.imgur.com/YjuuJlS.png)



Whereas HTML has tags, CSS has selectors. **Selectors are the names given to styles in internal and external style sheets**.

For each selector there are “**properties**” inside curly brackets, which simply take the form of words such as **color, font-weight or background-color**.

A **value** is given to the property following a colon (NOT an “equals” sign). Semi-colons are used to separate the properties.


```
body {
    font-size: 14px;
    color: navy;
}
```


----------------


# Lengths and Percentages

一些單位參考

px (such as font-size: 12px) is the unit for pixels.

em (such as font-size: 2em) is the unit for the calculated size of a font. So “2em”, for example, is two times the current font size.

pt (such as font-size: 12pt) is the unit for points, for measurements typically in printed media.

% (such as width: 80%) is the unit for percentages.

Other units include pc (picas), cm (centimeters), mm (millimeters) and in (inches).

When a value is zero, you do not need to state a unit. For example, if you wanted to specify no border, it would be border: 0.


------


# Colors

CSS brings 16,777,216 colors to your disposal. They can take the form of a **name**(Ex.red), an **RGB (255,0,0) value** or a **hex code**(#f0000).

The following values, to specify full-on as red-as-red-can-be, all produce the same result:

a color name - like "red"
a HEX value - like "#ff0000"
an RGB value - like "rgb(255,0,0)"

吸色工具是可以很好模仿他人顏色的工具，或是從開發者瀏覽器工具裡面去看人家的程式碼使用甚麼顏色

**color and background-color**

Colors can be applied by using color and background-color

A blue background and yellow text could look like this:


```
h1 {
    color: yellow;
    background-color: blue;
}
```

-------------


# Text


這邊的東西可以在開發者工具裡面檢視，多熟練開發者工具！

You can alter the size and shape of the text on a web page with a range of properties.

**font-family**

各種字體選擇使用它

This is the font itself, such as Times New Roman, Arial, or Verdana.

![](https://i.imgur.com/sZOTIrA.png)

字形參考網站:https://fonts.google.com/



**font-size**

Font size. Size of a font. Font? The size of it.(字體大小)

`p { font-size: 16px; }`


**font-weight**

Bold or light text.(粗體字跟淡體字)

`.chubbybaby { font-weight: bold; }`


**font-style**

Italic or oblique text.(斜體字)

`.warning { font-style: italic; }`


**text-decoration**

Underlined, overlined, and struck-through text.(底線、上斜線、刪除線)

```
.oldfangled a:hover { text-decoration: none }

.newfangled a:hover { text-decoration: underline overline line-through wavy #f99 } 
```

**text-transform**

轉換大小寫

text-transform will change the case of the text.

Converts the case of letters — to uppercase, lowercase, or capitalized.

`h1 { text-transform: uppercase; }`



# Text spacing

The **letter-spacing** and **word-spacing** properties are for **spacing between letters or words**. The value can be a length or normal.(字母以及單字間的空白)

The **line-height** property sets the height of the lines in an element, such as a paragraph, without adjusting the size of the font. It can be a number (which specifies a multiple of the font size, so “2” will be two times the font size, for example), a length, a percentage, or normal.(行高)

The **text-align** property will align the text inside an element to left, right, center, or justify.(文字置中偏左偏又等等)

The **text-indent** property will indent the first line of a paragraph, for example, to a given length or percentage. This is a style traditionally used in print, but rarely in digital media such as the web.(常用在印刷品少用在網頁，例如寫作文開頭要空幾個字下來)

------------------


# Margins and Padding

A **margin** is the space outside something, whereas **padding** is the space inside something.

* margin是指一個物件外面的空間

* padding是指一個物件內裡的空間



The four sides of an element can also be set individually. margin-top, margin-right, margin-bottom, margin-left, padding-top, padding-right, padding-bottom and padding-left are the self-explanatory properties you can use.

```
h2 {
    font-size: 1.5em;
    background-color: #ccc;
    margin: 20px;
    padding: 40px;
}
```

# The Box Model

Margins, padding and borders are all part of what’s known as the Box Model. 

The Box Model works like this: in the middle you have the content area (let’s say an image), surrounding that you have the padding, surrounding that you have the border and surrounding that you have the margin. It can be visually represented like this:

![](https://i.imgur.com/AY0cGAQ.png)

# Borders


To make a border around an element, all you need is border-style. The values can be solid, dotted, dashed, double, groove, ridge, inset and outset.

![](https://i.imgur.com/uyxOXNP.png)

```
h2 {
    border-style: dashed;
    border-width: 3px;
    border-left-width: 10px;
    border-right-width: 10px;
    border-color: red;
}
```