# MARKDOWN CHEAT SHEET

This is intended as a quick reference and showcase. For more info, see [*John Gruber's Markdown*](https://daringfireball.net/projects/markdown/) or you can watch the youtube video [*Introduction To Markdown Using Visual Studio Code by James Quick*](https://www.youtube.com/watch?v=pTCROLZLhDM) for other references.

> Using **Visual Studio** Open preview to the side (Ctrl+K+V). This helps you see the visual of your markdown.

## Table of Contents
1. [Header Elements](#1.-header-elements)
2. [Blockquote](#2.-blockquote)
3. [Spacing](#3.-spacing)
4. [Emphasis](#4.-emphasis)
5. [Dividers](#5.-dividers)
6. [Lists](#6.-lists)
7. [Links](#7.-links)
8. [Images](#8.-images)
9. [Code](#9.-code)
10. [Tables](#10.-tables)
11. [Custom HTML](#11.-custom-html)

---

## **_1. Header Elements_**

    Create Headers using pound '#' Sign. 

    # h1 
    ## h2 
    ### h3  
    #### h4 
    ##### h5

# Header 1 
## Header 2
### Header 3
#### Header 4
##### Header 5
###### Header 6

[Back to Top ↑](#table-of-contents)
-
---

## **_2. Blockquote_**

    Create blockquote using '>' 

> Sample blockquote
 
[Back to Top ↑](#table-of-contents)
-
----

## **_3. Spacing_** 

    You need to have a spacing for Line Break
        (HERE IS AND EMPTY SPACE)
    Sample Line Break

[Back to Top ↑](#table-of-contents)
-
-----
## **_4. Emphasis_**

    Create an Emphasis using '**', '_', '~'
        Emphasis, aka italics, with *asterisks* or _underscores_.
        Strong emphasis, aka bold, with **asterisks** or __underscores__.
        Combined emphasis with **asterisks and _underscores_**.
        Strikethrough uses two tildes. ~~Scratch this.~~ 

**Bold Style 1**

__Bold Style 2__

_Italics Style 1_

*Italics Style 2*

**_Bold and Italics Style_**

~~Strikethrough Stle~~

[Back to Top ↑](#table-of-contents)
-
---

## **_5. Dividers_**
    Dividers can be dashes '---' , asterisks '***' and underlines '___'.
    ---
    ***
    ___ 

[Back to Top ↑](#table-of-contents)
-
-----

## **_6. Lists_**

    Create unordered lists using '-', '*', '+'

- Dash 1
* Asterisk 2
+ PLus 3

Creating Sub-lists
- Item 1
    - Item 1.1
        - Item 1.1.1
- Item 2
    - Item 2.1

Creating Ordered Lists
1. Item 1
2. Item 2
3. Item 3
9. Even if the numbers are incorrect order it will automatically pick up the next number and order it.

[Back to Top ↑](#table-of-contents)
-
---

## **_7. Links_**

    Create a link with angle brackets '<>'
    <https://gitlab.com/botbrosai/internal/starters/brocode/tree/master>

<https://gitlab.com/botbrosai/internal/starters/brocode/tree/master>

    Create a Link surrounding text it with bracket [ ] and the link following with the parenthesis.
    [BROCODE REPOSITORY](https://gitlab.com/botbrosai/internal/starters/brocode/tree/master)

[BROCODE REPOSITORY](https://gitlab.com/botbrosai/internal/starters/brocode/tree/master)

    Create a link that can be reused.
    [key]:https://gitlab.com/botbrosai/internal/starters/brocode/tree/master
    [THIS LINK IS REUSED FOR BROCODE][key]

[key]:https://gitlab.com/botbrosai/internal/starters/brocode/tree/master

[THIS LINK IS REUSED FOR BROCODE][key]

    Create a link withing the page.
    When you create a header it will automaticatlly id it if there's spaces automatic hyphens each space. 
    "# Header" = "</h1 id='header'> Header <//h1>"

[Back to Top ↑](#table-of-contents)
-
---

## **_8. Images_**

    Create an image by defining references in the same format. Just add '!'
    ![SAMPLE PHOTOS](https://gitlab.com/botbrosai/internal/starters/brocode/tree/master/assets/image.jpg)

![SAMPLE PHOTOS](https://gitlab.com/botbrosai/internal/starters/brocode/tree/master/assets/image.jpg)

    You can also reuse pictures
    [profile]:https://gitlab.com/botbrosai/internal/starters/brocode/tree/master/assets/image.jpg
    ![James][profile]

[profile]:https://gitlab.com/botbrosai/internal/starters/brocode/tree/master/assets/image.jpg
![James][profile]

[Back to Top ↑](#table-of-contents)
-
---

## **_9. Code_**

    You can do inline code using backticks ``

Here are some item of code `<div class="code"> Code </code>`

    You can also do clocks of codes by surrounding it with 3 backticks ```

```
<body>
    <div class="code"> Code </code>
</body>
```
    You can also define the given language like javascript and html and it will automatically highlight based on languages.

```javascript
    var num = 0;
    const array = [1,2,3,4,5];
```

```html
    <div class="name"> Name </div>
```
[Back to Top ↑](#table-of-contents)
-
---

## **_10. Tables_**
    Creating tables are useful for displaying rows and columns of data.
    Column Headers are separated with pipes |
 
| Header 1 | Header 2 | Header 3 |
|---|---|---|
| Column 1 | Column 2| Column 3|
|---|---|---|
|Column 1| Column 2| Column 3|
|---|---|---| 

    Define the aliment of the texts on the tables using colons :
    -------, :-------:, -------:

| Header 1 | Header 2 | Header 3 |
|---| :---:|---:|
|  Left |  Center|  Right|

[Back to Top ↑](#table-of-contents)
-
---

## **_11. Custom HTML_**
    If you are familiar with HMTL, sice markdown gets automatically converted into HTML, you can add raw HTML directly to your MArkdown.

<style>
    .color {
        color: yellow;
    }
</style>

<div class="color"> HELLO WORLD !!! </div>

---
[Back to Top ↑](#table-of-contents)
---