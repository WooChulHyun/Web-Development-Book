# Block / Inline

### Block / Inline elements of HTML

 Go to link to find out which of the HTML elements are block or inline elements.

{% page-ref page="../../html/useful-website/block-and-inline-elements.md" %}



### Block

A block-level element always starts on a new line and takes up the full width available \(stretches out to the left and right as far as it can\).

Width, height, margin, and padding properties can be specified.

Block elements can include inline level elements.

```markup
<style>
    div {
        background: skyblue;
        padding: 20px;
        margin: 30px;
    }
    .box1 {
        margin-bottom: 50px;
    }
    .box2 {
        width: 300px;
        height: 200px;
    }
</style>
</head>

<body>
    <div class="box1">
        width, height unspecified
    </div>
    <div class="box2">
        width, height specify
    </div>
</body>
```

![](https://i.postimg.cc/prqP9DQV/block.png)



### Inline

An inline element does not start on a new line and only takes up as much width as necessary.

Width, height, margin-top, and margin-bottom properties can not be specified. top and bottom spaces are specified by line-height.

If there is a space after the inline level element \(enter, space, etc.\), an unspecified space \(4px\) is automatically specified.

Inline level elements are not be able to include a block level element. The inline level element is typically used in block level elements.

```markup
<style>
    span {
        background-color: skyblue;
        color: white;
        padding: 10px;
        border: 1px solid #000;
    }
</style>
</head>

<body>
    <h1>Hello <span>World</span></h1>
    <span>Enter</span>
    <span>Enter / Space</span> <span>Space / inline</span
    ><span>inline</span>
</body>
```

![](https://i.postimg.cc/65tDg2rz/inline.png)



### inline-block

Inline-block has both characteristic of block and inline level elements.

You can specify all of the width, height, and margin properties and it appears on one line like the inline level element.

```markup
<style>
    .inline-block {
        display: inline-block;
        background: skyblue;
        vertical-align: middle;
        border: 1px solid #000;
    }
    .box1 {
        width: 300px;
        height: 70px;
    }
    .box2 {
        width: 300px;
        height: 150px;
    }
</style>
</head>

<body>
    <div class="inline-block box1">inline-block Enter</div>
    <div class="inline-block box2">inline-block Enter</div>
    <br />
    <br />
    <div class="inline-block box1">
        no Enter / no Space
    </div><div class="inline-block box2">no Enter / no Space</div>
</body>
```

![](https://i.postimg.cc/850zw2nQ/inline-block.png)

