# FONT / TEXT Style

### font-size

Specifies the font family for text

```markup
<style>
    .fontSize30 {
        font-size: 30px;
    }
    .fontSize2_5x {
        font-size: 2.5em;
    }
    .fontSize3x {
        font-size: 3rem;
    }
    .fontSize150ps {
        font-size: 200%;
    }
    .fontSizeLarge {
        font-size: large;
    }
</style>
</head>

<body>
    <p class="fontSize30">font-size: 30px</p>
    <p class="fontSize2_5x">font-size: 2.5em</p>
    <p class="fontSize3x">font-size: 3rem</p>
    <p class="fontSize150ps">font-size: 170%</p>
    <p class="fontSizeLarge">font-size: large</p>
</body>
```

![](https://i.postimg.cc/k4CrRVZH/font-size.png)



### font-family

Specifies the font. It does not apply if the font is not installed on your computer.

Multiple fonts can be specified at the same time. If the first specified font is not installed on the client computer, the next specified font is applied. Therefore, it is common to specify a generic-family font \(Serif, Sans-serif, Mono space\) that is installed in most OSs at the last.

```markup
<style>
    .serif {
        font-family: "Times New Roman", Times, serif;
    }

    .sans-serif {
        font-family: Arial, Helvetica, sans-serif;
    }

    .monospace {
        font-family: "Courier New", Courier, monospace;
    }
</style>
</head>

<body>
    <h1>font-family</h1>
    <p class="serif">Times New Roman font.</p>
    <p class="sans-serif">Arial font.</p>
    <p class="monospace">Courier New font.</p>
</body>
```

![](https://i.postimg.cc/Y2GzTbyp/font-family.png)



### font-style

It is usually used to make italicized.



```markup
<style>
    .italicized {
        font-style: italic;
    }
</style>
</head>

<body>
    <h1>font-style</h1>
    <p>Normal font</p>
    <p class="italicized">Italicized font</p>
</body>
```

![](https://i.postimg.cc/gJB487S7/font-style.png)



### font-weight

Specifies the font thickness.

```markup
<style>
     /*
      font-weight
      100 ~ 900 or normal / bold / lighter / bolder
    */
    .bold {
        font-weight: bold;
    }
    .font-weight900 {
        font-weight: 900;
    }
    .font-weight200 {
        font-weight: 200;
    }
</style>
</head>

<body>
    <h1>font-weight</h1>
    <h2 class="bold">bold</h2>
    <h2 class="font-weight900">font-weight 900</h2>
    <h2 class="font-weight200">font-weight 200</h2>
</body>
```

![](https://i.postimg.cc/HkxNcQkj/font-weight.png)



### text-decoration

You can remove the link underline using the text-decoration property. Or you can add underline, overline, and line-through to the text.

```markup
<style>
    .underline {
        text-decoration: underline;
    }
    .line-through {
        text-decoration: line-through;
    }
    .overline {
        text-decoration: overline;
    }
</style>
</head>

<body>
    <h1>text-decoration</h1>
    <h2 class="underline">underline</h2>
    <h2 class="line-through">line-through</h2>
    <h2 class="overline">overline</h2>
</body>
```

![](https://i.postimg.cc/TYq9dhj1/text-decoration.png)



### letter-spacing

Specifies the spacing between characters.

```markup
<style>
    .letter-spacing3px {
        letter-spacing: 3px;
    }
    .letter-spacing-2px {
        letter-spacing: -2px;
    }
</style>
</head>

<body>
    <p>Lorem ipsum dolor sit amet consectetur adipisicing.</p>

    <p class="letter-spacing3px">
        Lorem ipsum dolor sit amet consectetur adipisicing.
    </p>

    <p class="letter-spacing-2px">
        Lorem ipsum dolor sit amet consectetur adipisicing.
    </p>
</body>
```

![](https://i.postimg.cc/kgc4jPQB/letter-spacing.png)



### text-align

The text-align property specifies the horizontal alignment of text in an element.

```markup
<style>
    .center {
        text-align: center;
    }
    .right {
        text-align: right;
    }
    .left {
        text-align: left;
    }
    .justify {
        text-align: justify;
    }
</style>
</head>

<body>
    <h1 class="center">Lorem ipsum</h1>
    <p class="right">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda
        facilis veniam tempora blanditiis, laboriosam rem pariatur molestias
        incidunt sint fuga repellat repellendus impedit facere esse deserunt
        iusto ad eligendi eius?
    </p>

    <p class="left">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda
        facilis veniam tempora blanditiis, laboriosam rem pariatur molestias
        incidunt sint fuga repellat repellendus impedit facere esse deserunt
        iusto ad eligendi eius?
    </p>

    <p class="justify">
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Assumenda
        facilis veniam tempora blanditiis, laboriosam rem pariatur molestias
        incidunt sint fuga repellat repellendus impedit facere esse deserunt
        iusto ad eligendi eius?
    </p>

    <a class="center" href="#"
        >Because `a` is inline element, text-align does not work(need to
        change display: block or inline-block)</a
    >
</body>
```

![](https://i.postimg.cc/bwbWx1tT/text-align.png)



### line-height

The line-height property specifies the height of a line.

```markup
<style>
    .line-height-70 {
        line-height: 70%; /* 16px * 70% */
    }
    .line-height-3 {
        line-height: 3; /* 16px * 3 */
    }
    .skyblue {
        background: skyblue;
        height: 50px;
    }
    .line-height50px {
        line-height: 50px;
    }
    .line-height75px {
        line-height: 75px;
    }
    .line-height50 {
        line-height: 50%;
    }
</style>
</head>

<body>
    <p>
        default line-height.<br />
        default line-height.<br />
        Usually, default line height is 110% ~ 120%.<br />
    </p>

    <p class="line-height-70">
        line-height: 70%<br />
        line-height: 70%<br />
    </p>

    <p class="line-height-3">
        line-height: 3<br />
        line-height: 3<br />
    </p>

    <div class="skyblue">
        <p class="line-height50px">div height: 50px / p line-height 50px</p>
    </div>

    <div class="skyblue">
        <p class="line-height75px">div height: 50px / p line-height 75px</p>
    </div>

    <div class="skyblue">
        <p class="line-height50">div height: 50px / p line-height 50%</p>
    </div>
</body>
```

![](https://i.postimg.cc/J0Tn19qp/line-height.png)



### white-space

The white-space property specifies how white-space\(space, tab, line break\) inside an element is handled.

```markup
<style>
            div {
                width: 150px;
                height: 150px;
                padding: 30px;
                margin-bottom: 200px;
                border: 1px solid #000;
            }
            .normal {
                white-space: normal;
            }
            .nowrap {
                white-space: nowrap;
            }
            .pre {
                white-space: pre;
            }
            .pre-wrap {
                white-space: pre-wrap;
            }
            .pre-line {
                white-space: pre-line;
            }
        </style>
    </head>

    <body>
        <h1>white-space</h1>
        <div class="normal">
            <h3>normal</h3>
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
        </div>
        <div class="nowrap">
            <h3>nowrap</h3>
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
        </div>
        <div class="pre">
            <h3>pre</h3>
                            Incomprehensibilities
            Incom    prehe    nsibil
            Incomprehensibilities Incomprehensibilities Incomprehensibilities
        </div>
        <div class="pre-wrap">
            <h3>pre-wrap</h3>
                            Incomprehensibilities
            Incom    prehe    nsibil
            Incomprehensibilities    Incomprehensibilities
        </div>
        <div class="pre-line">
            <h3>pre-line</h3>
                            Incomprehensibilities
            Incom    prehe    nsibil
            Incomprehensibilities    Incomprehensibilities
        </div>
    </body>
```

![](https://i.postimg.cc/vH7FCcMX/white-space.png)

Differences between pre-wrap and pre-line: In pre-warp, space / tab is applied as written, and in pre-line, space / tab is applied only once.



### text-overflow

The text-overflow property specifies how overflowed content that is not displayed should be signaled to the user. It can be clipped, display an ellipsis \(...\), or display a custom string.

```markup
<style>
    .div1 {
        width: 400px;
        height: 150px;
        padding: 30px;
        margin-bottom: 100px;
        border: 1px solid #000;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: clip;
    }
    .div2 {
        width: 400px;
        height: 150px;
        padding: 30px;
        margin-bottom: 100px;
        border: 1px solid #000;
        white-space: nowrap;
        overflow: hidden;
        text-overflow: ellipsis;
    }
</style>
</head>

<body>
    <h1>text-overflow</h1>
    <div class="div1">
        <h3>clip</h3>
        Incomprehensibilities Incomprehensibilities Incomprehensibilities
        Incomprehensibilities Incomprehensibilities Incomprehensibilities
    </div>
    <div class="div2">
        <h3>ellipsis</h3>
        Incomprehensibilities Incomprehensibilities Incomprehensibilities
        Incomprehensibilities Incomprehensibilities Incomprehensibilities
    </div>
</body>
```

![](https://i.postimg.cc/Bvp2z5ws/text-overflow.png)



### word-wrap / word-break

The word-wrap property allows long words to be able to be broken and wrap onto the next line.

The word-break property specifies how words should break when reaching the end of a line.

```markup
<style>
    .div {
        width: 200px;
        height: 150px;
        padding: 30px;
        margin-bottom: 50px;
        border: 1px solid #000;
    }
    .div1 {
        width: 200px;
        height: 150px;
        padding: 30px;
        margin-bottom: 50px;
        border: 1px solid #000;
        word-wrap: break-word;
    }
    .div2 {
        width: 200px;
        height: 150px;
        padding: 30px;
        margin-bottom: 50px;
        border: 1px solid #000;
        word-break: break-all;
    }
</style>
</head>

<body>
    <h1>word-wrap / word-break</h1>
    <div class="div">
        <h3>Normal</h3>
        IncomprehensibilitiesIncomprehensibilitiesIncomprehensibilities
        https://woochulhyun.github.io/Web-Development-Book/
    </div>
    <div class="div1">
        <h3>word-wrap</h3>
        IncomprehensibilitiesIncomprehensibilitiesIncomprehensibilities
        https://woochulhyun.github.io/Web-Development-Book/
    </div>
    <div class="div2">
        <h3>word-break</h3>
        IncomprehensibilitiesIncomprehensibilitiesIncomprehensibilities
        https://woochulhyun.github.io/Web-Development-Book/
    </div>
</body>
```

![](https://i.postimg.cc/25mBDH1M/word-wrap-word-break.png)

#### Reference

{% embed url="https://poiemaweb.com/css3-font-text" %}

{% embed url="https://www.w3schools.com/" %}

