<style>
    .yellow-highlight {
        color: yellow;
        background: black;
        font-weight: 500;
        padding: 0 5px;
        border-radius: 10px
    }
    .red-highlight {
        color: red;
        background: #F1F1F1;
        font-weight: 500;
        padding: 0 5px;
        border-radius: 10px
    }

    .red-bg {
        background: #FFDDDD;
    }

    .title {
        color: blue;
        font-weight: 600;
    }
</style>

# Javascript Native

## Did you know?
> JavaScript was invented by Brendan Eich in 1995, and became an ECMA standard in 1997. [ECMA-262](https://www.ecma-international.org/publications/standards/Ecma-262.htm) is the official name of the standard. ECMAScript is the official name of the language.

## Introduction
* One of  many Javascript HTML methods is <i class="yellow-highlight"> getElementById() </i>.
> <p id="demo">JavaScript can change HTML content.</p> <button type="button" onclick='document.getElementById("demo").innerHTML = "Hello JavaScript!"'>Click Me!</button><p><i class="yellow-highlight">onclick='document.getElementById("demo").innerHTML = "Hello JavaScript!"'</i></p>

## <p class="title">Javascript Output </p>
> Javascript can display data in different ways:
* Writing into an HTML element. using <span class="red-highlight">innerHTML</span>
* Writing into the HTML output using <span class="red-highlight"> document.write()</span>
* Writing into an alert box, <span class="red-highlight"> using window.alert() </span>
* Writing into the browser console, using <span class="red-highlight"> console.log() </span> 

### innerHTML
```
<!DOCTYPE html>
<html>
<body>

    <p id="demo"></p>

<script>
    document.getElementById("demo").innerHTML = 5 + 6;
</script>

</body>
</html>
```

### document.write()
```
<!DOCTYPE html>
<html>
<body>

<script>
    document.write("HELLO");
</script>

</body>
</html> 
```

> Note: Using document.write() after an HTML document is loaded, will delete all existing HTML:

```
<!DOCTYPE html>
<html>
<body>

    <h1>My First Web Page</h1>
    <p>My first paragraph.</p>

    <button type="button" onclick="document.write(5 + 6)">Try it</button>

</body>
</html>
```

### window.alert()

```
<script>
    window.alert(5 + 6);
</script>
```

### console.log()

```
<script>
    console.log(5 + 6);
</script> 
```

## <p class="title">Javascript Statement</p>
> Javascript statements are composed of: **Values, Operators, Expressions, Keywords and Comments.**