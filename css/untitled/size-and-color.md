# Size and Color

## Size

There are size units such as cm, mm, and inch, but typical size units used in CSS are px, em, rem, %.

px is the absolute value, em, rem and \% is the relative value.

The default font size for most browsers is 16px, 1em, 1rem, 100%.



## px

px is the pixel unit. 1px means the size of one pixel.

Pixels have relative sizes depending on the device resolution.

```markup
<style>
    .fontSize15 {
        font-size: 15px;
    }
    .fontSize30 {
        font-size: 30px;
    }
</style>
</head>

<body>
    <p class="fontSize15">font-size: 15px</p>
    <p class="fontSize30">font-size: 30px</p>
</body>
```

![](https://i.postimg.cc/0yjjQNJx/size-px.png)



## em

em is the relative unit. Sets the size relative to the inherited or default size.

```markup
<style>
    .fontSize1em {
        font-size: 1em;
    }
    .fontSize2em {
        font-size: 2em;
    }
</style>
</head>

<body>
    <p class="fontSize1em">font-size: 1em</p>
    <p class="fontSize2em">font-size: 2em</p>
</body>
```

![](https://i.postimg.cc/tCySHT44/size-em1.png)

```markup
<style>
    div {
        font-size: 2em;
    }
    .div1 {
        background: skyblue;
        padding: 30px;
    }
    .div2 {
        background: pink;
        width: 500px;
    }
</style>
</head>

<body>
    <div class="fontSize2em div1">
        font-size: 2em
        <div class="fontSize2em div2">font-size: 2em</div>
    </div>
</body>
```

![](https://i.postimg.cc/zXXQgvZP/size-em2.png)



## rem

rem is based on the size of the top-level element\(html\). The r in rem means root.

```markup
<style>
    div {
        font-size: 2rem;
    }
    .div1 {
        background: skyblue;
        padding: 30px;
    }
    .div2 {
        background: pink;
        width: 500px;
    }
</style>
</head>

<body>
    <div class="fontSize2rem div1">
        font-size: 2em
        <div class="fontSize2rem div2">font-size: 2rem</div>
    </div>
</body>
```

![](https://i.postimg.cc/WbvkWqbX/size-rem.png)



## %

% is the relative unit. Sets the size relative to the inherited or default size.

```markup
<style>
    div {
        width: 50%;
    }
    p {
        width: 50%;
        background-color: yellow;
    }
</style>
</head>
<body>
    <div>
        <p>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi,
            quas quam! In perferendis reiciendis blanditiis aliquid debitis
            ducimus quod sapiente eligendi pariatur! Sunt commodi ratione
            aspernatur tenetur! Impedit, omnis ratione?
        </p>
    </div>
    <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Nisi, quas
        quam! In perferendis reiciendis blanditiis aliquid debitis ducimus
        quod sapiente eligendi pariatur! Sunt commodi ratione aspernatur
        tenetur! Impedit, omnis ratione?
    </p>
</body>
```

![](https://i.postimg.cc/Rh3Xg6SM/size.png)



## Viewport\(vh, vw, vmin, vmax\)

### vh, vw

The vh is in hundredths of a height value. For example, if the browser height size is 900px, 1vh means 9px. Similarly, if the width of the viewport is 750px, 1vw is 7.5px.

```markup
<style>
    div {
        border: 1px solid #000;
        padding: 0;
    }
    p {
        font-size: 2rem;
        background: skyblue;
        margin: 0;
    }
    .div1 {
        height: 33vh;
        width: 50vw;
    }
</style>
</head>
<body>
    <div class="outer">
        <p class="div1">vh, vw</p>
    </div>
</body>
```

![](https://i.postimg.cc/9Qr1VgsL/size-vh-vw.png)



### vmin, vmax

If vh and vw are always affected by the width and height values of the viewport, vmin and vmax can specify the maximum and minimum values according to the width and height values.

For example, if your browser is 1100px wide and 700px high, 1vmin will be 7px and 1vmax will be 11px. When the width value becomes 800px and the height value becomes 1080px, vmin becomes 8px and vmax becomes 10.8px.

```markup
<style>
    div {
        border: 1px solid #000;
        padding: 0;
    }
    p {
        font-size: 2rem;
        background: skyblue;
        margin: 0;
    }
    .div1 {
        height: 50vmax;
        width: 30vmin;
    }
</style>
</head>
<body>
    <div class="outer">
        <p class="div1">vmin, vmax</p>
    </div>
</body>
```

![](https://i.postimg.cc/ZRb062Pm/size-vmin-vmax.png)



## Color

You can use keywords \(yellow, red, blue ...\) to specify colors. It has the advantage of being easy to use, but the number of colors that can be expressed is limited.

```markup
<body>
    <p style="background-color:red">
        Red background-color
    </p>
    <p style="background-color:green">
        Green background-color
    </p>
    <p style="background-color:yellow">
        Yellow background-color
    </p>
</body>
```

![](https://i.postimg.cc/pdZ6hpYs/bg-color.png)

In order to express more various colors, the following color expression units can be used.

| Color Units | Example |
| :--- | :--- |
| HEX \(Hexadecimal Colors\) | \#000000 |
| RGB \(Red, Green, Blue\) | rgb\(255, 255, 0\) / \(0 ~ 255\) |
| RGBA \(Red, Green, Blue, Alpha\) | rgba\(255, 255, 0, 1\) / Alpha \(0 ~ 1\) |
| HSL \(Hue, Saturation, Lightness\) | hsl\(0, 50%, 25%\) / h\(0 ~ 360\) s,l \(0 ~ 100\) |
| HSLA \(Hue, Saturation, Lightness, Alpha\) | hsla\(60, 100%, 25%, 1\) / Alpha \(0 ~ 1\) |

```markup
<style>
    #hex-red {
        background-color: #ff0000;
    }
    #hex-green {
        background-color: #00ff00;
    }
    #hex-yellow {
        background-color: #ffff00;
    }

    #rgb-red {
        background-color: rgb(255, 0, 0);
    }
    #rgb-green {
        background-color: rgb(0, 255, 0);
    }
    #rgb-yellow {
        background-color: rgb(255, 255, 0);
    }

    #rgba-red {
        background-color: rgba(255, 0, 0, 0.3);
    }
    #rgba-green {
        background-color: rgba(0, 255, 0, 0.3);
    }
    #rgba-yellow {
        background-color: rgba(255, 255, 0, 0.3);
    }

    #hsl-red {
        background-color: hsl(0, 100%, 50%);
    }
    #hsl-green {
        background-color: hsl(120, 100%, 50%);
    }
    #hsl-yellow {
        background-color: hsl(60, 100%, 50%);
    }

    #hsla-red {
        background-color: hsla(0, 100%, 50%, 0.3);
    }
    #hsla-green {
        background-color: hsla(120, 100%, 50%, 0.3);
    }
    #hsla-yellow {
        background-color: hsla(60, 100%, 50%, 0.3);
    }
</style>
</head>

<body>
    <h3>HEX colors:</h3>
    <p id="hex-red">Red</p>
    <p id="hex-green">Green</p>
    <p id="hex-yellow">Yellow</p>

    <h3>RGB colors:</h3>
    <p id="rgb-red">Red</p>
    <p id="rgb-green">Green</p>
    <p id="rgb-yellow">Yellow</p>

    <h3>RGB colors with opacity:</h3>
    <p id="rgba-red">Red</p>
    <p id="rgba-green">Green</p>
    <p id="rgba-yellow">Yellow</p>

    <h3>HSL colors:</h3>
    <p id="hsl-red">Red</p>
    <p id="hsl-green">Green</p>
    <p id="hsl-yellow">Yellow</p>

    <h3>HSL colors with opacity:</h3>
    <p id="hsla-red">Red</p>
    <p id="hsla-green">Green</p>
    <p id="hsla-yellow">Yellow</p>
</body>
```

![](https://i.postimg.cc/jdD2MfDJ/bg-color-expression.png)

