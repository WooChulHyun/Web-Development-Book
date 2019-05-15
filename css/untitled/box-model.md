# Box Model

### Box Model

Box consists of Content, Padding, Border, and Margin.

![](https://i.postimg.cc/1XkG5xtG/box-model.png)



### margin / padding

```markup
<style>
    .box1 {
        border: 5px solid #000;
        background: skyblue;
        padding-top: 20px;
        padding-right: 40px;
        padding-bottom: 60px;
        padding-left: 80px;
    }
    .box2 {
        border: 5px solid #000;
        background: pink;
        margin-top: 80px;
        margin-right: 60px;
        margin-bottom: 40px;
        margin-left: 20px;
    }
</style>
</head>
<body>
    <div class="box1">
        <div class="box2">
            Lorem ipsum dolor sit amet, consectetur adipisicing elit.
            Doloremque facere ut maxime nam iusto quod odio inventore
            perferendis, voluptas dolore sint corporis aperiam omnis autem,
            soluta earum nulla dolorum at.
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/43KL4mrD/padding-margin.png)

If only one value is specified, the values in all four directions are equal.

If you create two values, top and bottom \| right and left values are respectively specified.

If you create three values, top \| right, left \| bottom.

If you create four values, top \| right \| bottom \| left.

```css
.box {
    /* top right bottom left */
    margin: 10px;
}
.box {
    /* top bottom | right left */
    margin: 10px 20px;
}
.box {
    /* top | right left | bottom */
    margin: 10px 20px 30px;
}
.box {
    /* top | right | bottom | left */
    margin: 10px 20px 30px 40px;
}
```



### box-sizing

The box-sizing property can change the area of the width and height properties.

The default value for the box-sizing property is content-box. This means that the target area of the width and height properties is the content area.

If you specify the value of the box-sizing property to the border-box, you can specify the entire box model except the margin as the target area of the width and height properties.

```markup
<style>
    .div {
        box-sizing: content-box;
        width: 200px;
        height: 150px;
        padding: 30px;
        margin: 20px;
        border: 10px solid #000;
    }
    .div1 {
        box-sizing: border-box;
        width: 200px;
        height: 150px;
        padding: 30px;
        margin: 20px;
        border: 10px solid #000;
    }
</style>
</head>

<body>
    <h1>box-sizing</h1>
    <div class="div">
        <h3>content-box</h3>
    </div>
    <div class="div1">
        <h3>border-box</h3>
    </div>
</body>
```

![](https://i.postimg.cc/gkYXDG76/box-sizing.png)

In the same width, height, padding, border, margin value:

Content-box:

* width: content width\(200px\) + left / right padding\(30px + 30px = 60px\) + left / right border\(10px + 10px = 20px\) = 280px
* height: content width\(150px\) + top / bottom padding\(30px + 30px = 60px\) + top / bottom border\(10px + 10px = 20px\) = 230px

Border-box:

* width: content width\(120px\) + left / right padding\(30px + 30px = 60px\) + left / right border\(10px + 10px = 20px\) = 200px
* height: content width\(70px\) + top / bottom padding\(30px + 30px = 60px\) + top / bottom border\(10px + 10px = 20px\) = 200px

You can change the value of the box-sizing property to border-box to facilitate sizing.

```css
html {
    box-sizing: border-box;
}

*,
*::before,
*::after {
    box-sizing: border-box;
}
```



### border

For border, you can specify thickness, line shape and color. Thickness and shape are mandatory.

If you do not specify a color, the default color is the same as the color of the letter.



### border-style

The shape of the line\(border-style\) is solid \| dashed \| dotted \| ridge \| double \| groove \| inset \| outset.

```markup
<style>
    p {
        background: skyblue;
        padding: 20px;
    }
    .box1 {
        /* four sides */
        border-style: solid;
    }
    .box2 {
        /* top, bottom | right, left */
        border-style: dotted solid;
    }
    .box3 {
        /* top | right, left | bottom */
        border-style: groove inset outset;
    }
    .box4 {
        /* top | right | bottom | left */
        border-style: dashed ridge dotted double;
    }
</style>
</head>

<body>
    <p class="box1">solid</p>
    <p class="box2">dotted solid</p>
    <p class="box3">groove inset outset</p>
    <p class="box4">dashed ridge dotted double</p>
</body>
```

![](https://i.postimg.cc/rFXdFmPv/border-style.png)



### border-width

The border-width property specifies the thickness of the border. It can be specified for four directions \(top, right, left, bottom\) depending on the number of property values.

```markup
<style>
    p {
        background: skyblue;
        padding: 20px;
    }
    .box1 {
        /* four sides */
        border-style: solid;
        border-width: 3px;
    }
    .box2 {
        /* top, bottom | right, left */
        border-style: solid;
        border-width: 3px 10px;
    }
    .box3 {
        /* top | right, left | bottom */
        border-style: solid;
        border-width: 3px 10px 20px;
    }
    .box4 {
        /* top | right | bottom | left */
        border-style: solid;
        border-width: 3px 10px 20px 40px;
    }
</style>
</head>

<body>
    <p class="box1">solid / border-width: 3px</p>
    <p class="box2">solid / border-width: 3px 10px</p>
    <p class="box3">solid / border-width: 3px 10px 20px</p>
    <p class="box4">solid / border-width: 3px 10px 20px 40px</p>
</body>
```

![](https://i.postimg.cc/6qjtZMhj/border-width.png)



### border-color

The border-color property specifies the color of the border. It can be specified for four directions \(top, right, left, bottom\) depending on the number of property values.

```markup
<style>
    p {
        background: skyblue;
        padding: 20px;
    }
    .box1 {
        /* four sides */
        border-style: solid;
        border-width: 3px;
        border-color: yellow;
    }
    .box2 {
        /* top, bottom | right, left */
        border-style: solid;
        border-width: 3px 10px;
        border-color: yellow red;
    }
    .box3 {
        /* top | right, left | bottom */
        border-style: solid;
        border-width: 3px 10px 20px;
        border-color: yellow red green;
    }
    .box4 {
        /* top | right | bottom | left */
        border-style: solid;
        border-width: 3px 10px 20px 40px;
        border-color: yellow red green blue;
    }
</style>
</head>

<body>
    <p class="box1">solid / border-width: 3px / border-color: yellow</p>
    <p class="box2">
        solid / border-width: 3px 10px / border-color: yellow red
    </p>
    <p class="box3">
        solid / border-width: 3px 10px 20px / border-color: yellow red green
    </p>
    <p class="box4">
        solid / border-width: 3px 10px 20px 40px / border-color: yellow red
        green blue
    </p>
</body>
```

![](https://i.postimg.cc/9MXfqwhf/border-color.png)



### border-radius

```markup
<style>
    div {
        background: skyblue;
        padding: 20px;
        margin: 30px;
    }
    .box1 {
        width: 300px;
        height: 200px;
        border-style: solid;
        border-width: 10px;
        border-color: #000;
        border-radius: 20px;
    }
    .box2 {
        width: 300px;
        height: 200px;
        border-style: solid;
        border-width: 10px;
        border-color: #000;
        border-top-left-radius: 25px;
        border-top-right-radius: 90px;
        border-bottom-right-radius: 25px;
        border-bottom-left-radius: 90px;
    }
    .box3 {
        width: 90px;
        height: 90px;
        border-style: solid;
        border-width: 10px;
        border-color: #000;
        border-radius: 50%;
    }
</style>
</head>

<body>
    <div class="box1">
        <p>
            border-top-left-radius: 20px
        </p>
        <p>
            border-top-right-radius: 20px
        </p>
        <p>
            border-bottom-right-radius: 20px
        </p>
        <p>
            border-bottom-left-radius: 20px
        </p>
    </div>
    <div class="box2">
        <p>
            border-top-left-radius: 25px
        </p>
        <p>
            border-top-right-radius: 90px
        </p>
        <p>
            border-bottom-right-radius: 25px
        </p>
        <p>
            border-bottom-left-radius: 90px
        </p>
    </div>
    <div class="box3">
        <p>
            border-radius: 50%;
        </p>
    </div>
</body>
```

![](https://i.postimg.cc/qMYT2kS4/border-radius.png)

```markup
<style>
    div {
        background: skyblue;
        padding: 20px;
        margin: 30px;
    }
    .box1 {
        width: 300px;
        height: 200px;
        border-style: solid;
        border-width: 10px;
        border-color: #000;
        border-radius: 50px 50px 25px 25px / 25px 25px 50px 50px;
    }
    .box2 {
        width: 300px;
        height: 200px;
        border-style: solid;
        border-width: 10px;
        border-color: #000;
        border-top-left-radius: 90px 25px;
        border-top-right-radius: 25px 90px;
        border-bottom-right-radius: 90px 25px;
        border-bottom-left-radius: 25px 90px;
    }
</style>
</head>

<body>
    <div class="box1">
        <p>
            border-top-left-radius: 50px 25px
        </p>
        <p>
            border-top-right-radius: 50px 25px
        </p>
        <p>
            border-bottom-right-radius: 25px 50px
        </p>
        <p>
            border-bottom-left-radius: 25px 50px
        </p>
    </div>
    <div class="box2">
        <p>
            border-top-left-radius: 90px 25px
        </p>
        <p>
            border-top-right-radius: 25px 90px
        </p>
        <p>
            border-bottom-right-radius: 90px 25px
        </p>
        <p>
            border-bottom-left-radius: 25px 90px
        </p>
    </div>
</body>
```

![](https://i.postimg.cc/Wp5FLkF8/border-radius2.png)

