# CSS Selector

### CSS Selector Priority

* \* {} Universal Selector: 0 points
* body {} Type Selector: 1 point
* .class {} class selector: 10 points
* \#id {} ID Selector: 100 points
* `<p style = "color: red"> Inline Style </hr p>` Inline style: 1000 points

How to apply top level

When the Selector Priority is the same, the style you applied later appears, but if you type !Important, you can create a style that applies to the top level.

#### Example

```markup
<style>
            #contentsId {
                background: skyblue;
            }
            .contentsClass {
                background: yellow;
            }
            p {
                background: black;
            }
        </style>
    </head>
    <body>
        <h1>CSS Selectors</h1>

        <p id="contentsId" class="contentsClass">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Quaerat
            laudantium iste fugiat tempore, ab autem sequi saepe consequuntur
            quis vel labore blanditiis officia ea eaque similique totam iusto
            quasi architecto?
        </p>
    </body>
```

ID Selector &gt; class selector &gt; Type Selector

![](https://i.postimg.cc/HLj60GfC/CSS-Selectors.png)

```markup
<style>
            #contentsId {
                background: skyblue;
            }
            .contentsClass {
                background: yellow !important;    <-------
            }
            p {
                background: black;
            }
        </style>
    </head>
    <body>
        <h1>CSS Selectors</h1>

        <p id="contentsId" class="contentsClass">
            Lorem, ipsum dolor sit amet consectetur adipisicing elit. Quaerat
            laudantium iste fugiat tempore, ab autem sequi saepe consequuntur
            quis vel labore blanditiis officia ea eaque similique totam iusto
            quasi architecto?
        </p>
    </body>
```

!important &gt; ID Selector &gt; class selector &gt; Type Selector

![](https://i.postimg.cc/bYR1vCB0/CSS-Selectors-important.png)



### 1. .class

Selects all elements with class="yellow"

```markup
<style>
    .yellow {
        background-color: yellow;
    }
</style>
</head>
<body>
    <h1>CSS Selectors</h1>

    <div class="yellow">
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/PxsFd3Rs/CSS-Selectors-class-and-id.png)



### 2. .id

Selects the element with id="yellow"

```markup
<style>
    #yellow {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/PxsFd3Rs/CSS-Selectors-class-and-id.png)



### 3. \*

Selects all elements

```markup
<style>
* {
    background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div id="yellow">
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
    </div>
    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/R0h58DnM/CSS-Selectors.png)



### 4. element \(ex. html, body, div, p, a…\)

Selects all `<html, body, div, p, a...>` elements

```markup
<style>
    p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
    </div>

    <p>highlight3 highlight3 highlight3</p>
</body>
```

![](https://i.postimg.cc/L5TxmmrG/CSS-Selectors-element.png)



### 5. element, element

Selects all `<h1>` elements and all `<p>` elements

```markup
<style>
    h1,
    p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors (highlight0 highlight0 highlight0)</h1>

    <div id="yellow">
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
    </div>

    <p>highlight3 highlight3 highlight3</p>
</body>
```

![](https://i.postimg.cc/Kvp5fpF7/CSS-Selectors-element-element.png)



### 6. element element

Selects all `<p>` elements inside `<div>` elements

```markup
<style>
    div p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight1 highlight1 highlight1</p>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/MKfck9Vm/CSS-Selectors-element-element-1.png)

```markup
<style>
    div p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
        <div>
            <p>highlight3 highlight3 highlight3</p>
        </div>
        <span>
            <p>highlight4 highlight4 highlight4</p>
        </span>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/Zq5BQ4cC/CSS-Selectors-element-element-2.png)

Compare with element &gt; element



### 7. element &gt; element

Selects all `<p>` elements where the parent is a `<div>` element

```markup
<style>
    div > p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/3xVkcbK2/CSS-Selectors-element-element-1.png)

```markup
<style>
    div > p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
        <div>
            <p>highlight3 highlight3 highlight3</p>
        </div>
        <span>
            <p>nothing nothing nothing</p>
        </span>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/xTdqTS8K/CSS-Selectors-element-element-2.png)

Compare with element element



### 8. element + element

Selects all `<p>` elements that are placed immediately after `<div>` elements

```markup
<style>
    div + p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>nothing nothing nothing</p>
    </div>

    <p>highlight1 highlight1 highlight1</p>
</body>
```

![](https://i.postimg.cc/PJJhhTyJ/CSS-Selectors-element-element-1.png)

```markup
<style>
    span + p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
        <p>nothing nothing nothing</p>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/C5RyXJMf/CSS-Selectors-element-element-2.png)



### 9. element1 ~ element2

Selects every `<p>` element that are preceded by a `<span>` element

```markup
<style>
    span ~ p {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div id="yellow">
        <span>nothing nothing nothing</span>
        <p>highlight1 highlight1 highlight1</p>
        <p>highlight2 highlight2 highlight2</p>
        <div>
            <p>nothing nothing nothing</p>
        </div>
        <span>
            <p>nothing nothing nothing</p>
        </span>
    </div>

    <p>nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/QMMrcXLb/CSS-Selectors-element-element.png)



### 10. \[attribute\]

Selects all elements with a target attribute

```markup
<style>
    a[target] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <a href="https://www.naver.com">naver</a> <br />
    <br />
    <a href="http://www.daum.net" target="_blank">daum</a> <br />
    <br />
    <a href="http://www.google.com" target="_top">google</a>
</body>
```

![](https://i.postimg.cc/9Q79CjgL/CSS-Selectors-attribute.png)



### 11. \[attribute=value\]

Selects all elements with target="\_blank"

```markup
<style>
    a[target="_blank"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://www.naver.com">naver</a> <br />
    <br />
    <a href="http://www.daum.net" target="_blank">daum</a> <br />
    <br />
    <a href="http://www.google.com" target="_top">google</a>
</body>
```

![](https://i.postimg.cc/KznQzM9s/CSS-Selectors-attribute-value.png)



### 12. \[attribute~=value\]

Selects all elements with a class attribute containing the word "highlight"

```markup
<style>
    div[class~="highlight"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div class="nothing highlight">highlight highlight highlight</div>

    <div class="nothing">nothing nothing nothing</div>

    <div class="highlight">highlight highlight highlight</div>

    <div class="nothing_highlight">nothing nothing nothing</div>

    <p class="highlight">nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/sgmMVD99/CSS-Selectors-attribute-value.png)



### 13. \[attribute\|=value\]

Selects all elements with a lang attribute value starting with "en"

```markup
<style>
    [lang|="en"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div lang="en" class="nothing highlight">
        highlight highlight highlight
    </div>

    <div class="nothing">nothing nothing nothing</div>

    <div lang="ko" class="highlight">nothing nothing nothing</div>

    <div class="nothing_highlight">nothing nothing nothing</div>

    <p class="highlight">nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/MpvCG91P/CSS-Selectors-attribute-or-value.png)



### 14. \[attribute^=value\]

Selects every `<div>` element whose class attribute value begins with "highlight"

Must start at the same value. \(`div[class^="high"]`\) also possible.

```markup
<style>
    div[class^="highlight"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div class="nothing highlight">
        nothing nothing nothing
    </div>

    <div class="highlight_nothing">highlight highlight highlight</div>

    <div class="highlight">highlight highlight highlight</div>

    <div class="nothing_highlight">nothing nothing nothing</div>

    <p class="highlight">nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/7hRNtnbh/CSS-Selectors-attribute-value.png)



### 15. \[attribute$=value\]

Selects every `<div>` element whose class attribute value ends with "highlight"

Ending value must be the same. \(`div[class^="light"]`\) also possible.

```markup
<style>
    div[class$="highlight"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div class="nothing highlight">
        highlight highlight highlight
    </div>

    <div class="highlight_nothing">nothing nothing nothing</div>

    <div class="highlight">highlight highlight highlight</div>

    <div class="nothing_highlight">highlight highlight highlight</div>

    <p class="highlight">nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/jSc4GTDB/CSS-Selectors-attribute-value.png)



### 16. \[attribute\*=value\]

Selects every `<div>` element whose class attribute value contains the substring "highlight"

`div[class*="high"]` and`div[class*="light"]` also possible.

```markup
<style>
    div[class*="highlight"] {
        background-color: yellow;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <div class="nothing highlight nothing1">
        highlight highlight highlight
    </div>

    <div class="highlight_nothing">nothing nothing nothing</div>

    <div class="highlight">highlight highlight highlight</div>

    <div class="nothing_highlight">highlight highlight highlight</div>

    <p class="highlight">nothing nothing nothing</p>
</body>
```

![](https://i.postimg.cc/Y2NR1Qpp/CSS-Selectors-attribute-value.png)



### 17. Link-related selector

![](https://i.postimg.cc/Fz1j5kJ6/CSS-Selectors.png)

When we do not give any effect to link.

If you want to use the selector, use link -&gt; visited -&gt; hover -&gt; active -&gt; focus in general, we use these all selectors in once.

* :link

```markup
<style>
    a:link {
        color: black;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/Bvk8L78m/CSS-Selectors-link.png)

* :visited

When after you clicked the link.

```markup
<style>
    a:visited {
        color: gray;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/PfzxT5M3/CSS-Selectors-visited.png)



* :hover

When you hovered over the link.

```markup
<style>
    a:hover {
        color: blue;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/Jz3KQJ33/CSS-Selectors-hover.png)

* :active

When you are holding a click with your mouse

```markup
<style>
    a:active {
        color: red;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/4NfzTMpc/CSS-Selectors-active.png)

* :focus

It is applied at the moment of mouse click, but main usage is to be shown when approaching by tab key.

```markup
<style>
    a:focus {
        color: green;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/SKPhmwXx/CSS-Selectors-focus.png)

* Use all selectors in once

```markup
<style>
    a {
        color: black;
        text-decoration: none;
    }

    a:visited {
        color: black;
        text-decoration: none;
    }

    a:hover,
    a:active,
    a:focus {
        color: red;
        text-decoration: none;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <a href="https://google.com">Google</a>
</body>
```

![](https://i.postimg.cc/BbckPyvD/CSS-Selectors.png)



### 18. ::after and ::before

Insert something after the content of each `<h1>` element Insert something before the content of each `<h1>` element

```markup
<style>
    h1::before {
        content: "Before h1 ";
        color: skyblue;
    }

    h1::after {
        content: " After h1 ";
        color: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>

    <p class="contents">
        Lorem, ipsum dolor sit amet consectetur adipisicing elit. Quaerat
        laudantium iste fugiat tempore, ab autem sequi saepe consequuntur
        quis vel labore blanditiis officia ea eaque similique totam iusto
        quasi architecto?
    </p>
</body>
```

![](https://i.postimg.cc/hj3fWynL/CSS-Selectors-after-before.png)



### 19. :first-child, :first-of-type, ::first-letter, ::first-line

* :first-child

Selects every `<p>` element that is the first child of its parent

```markup
<style>
    p:first-child {
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div>
        <p>
            selected tag is first child of. selected tag is first child of.
        </p>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit.
        </p>
        <div>
            <p>
                selected tag is first child of. selected tag is first child
                of.
            </p>
            <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
            </p>
        </div>
        <div>
            <span
                >Lorem ipsum dolor, sit amet consectetur adipisicing.</span
            >
            <p>Lorem ipsum dolor sit amet consectetur adipisicing.</p>
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/cCyBYMkN/CSS-Selectors-first-child.png)

Differences from first-of-type is when first child is span in the last div: first-child does not select, but: first-of-type selects the first p in the last div, even if last div's first child is span.



* :fist-of-type

Selects every `<p>` element that is the first `<p>` element of its parent

```markup
<style>
    p:first-of-type {
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div>
        <p>
            selected type is first type in. selected type is first type in.
        </p>
        <div>
            <p>
                selected type is first type in. selected type is first type
                in.
            </p>
            <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
            </p>
        </div>
        <div>
            <span
                >Lorem ipsum dolor, sit amet consectetur adipisicing.</span
            >
            <p>
                selected type is first type in. selected type is first type
                in.
            </p>
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/DwTfDWHy/CSS-Selectors-first-of-type.png)



* ::fist-letter

Selects the first letter of every `<p>` element

```markup
<style>
    p::first-letter {
        font-size: 30px;
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div class="contentsDiv">
        <p class="contents">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Rem,
            eius.
        </p>
        <p class="contents">
            Lorem ipsum, dolor sit amet consectetur adipisicing elit. Rem,
            eius.
        </p>
        <div>
            <p class="contents">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Rem, eius.
            </p>
            <p class="contents">
                Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Rem, eius.
            </p>
        </div>
        <div>
            <span
                >Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Rem, eius.</span
            >
            <p>
                Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Rem, eius.
            </p>
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/x8fytTQs/CSS-Selectors-first-letter.png)



* ::first-line

Selects the first line of every `<p>` element

```markup
<style>
    p::first-line {
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div class="contentsDiv">
        <p class="contents">
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Maiores
            quidem ipsum, corporis assumenda nisi, praesentium ea dolor
            obcaecati, nesciunt itaque doloremque? Sed provident quod vero
            repudiandae non similique esse laudantium.Lorem ipsum dolor sit amet consectetur adipisicing elit. Maiores
            quidem ipsum, corporis assumenda nisi, praesentium ea dolor
            obcaecati, nesciunt itaque doloremque? Sed provident quod vero
            repudiandae non similique esse laudantium.
        </p>
        <div>
            <span
                >Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                Rem, eius.</span
            >
            <p>
                Lorem ipsum dolor sit amet consectetur adipisicing elit.
                Iure dolorum consequuntur debitis consequatur. Hic
                obcaecati, et atque laboriosam earum vitae rerum amet,
                expedita accusantium nostrum nulla ullam sit ipsum
                inventore! Lorem ipsum dolor sit amet consectetur adipisicing elit. Maiores
                quidem ipsum, corporis assumenda nisi, praesentium ea dolor
                obcaecati, nesciunt itaque doloremque? Sed provident quod vero
            </p>
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/d0J177jS/CSS-Selectors-first-line-1.png)

The same sentence, but only the top row is selected even if the number of words in the first line has been changed by screen size.

![](https://i.postimg.cc/mDDgw0qY/CSS-Selectors-first-line-2.png)



### 20. :last-child :last-of-type

* :last-child

Selects every `<p>` element that is the last child of its parent

```markup
<style>
    p:last-child {
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit.
        </p>
        <p>
            Lorem, ipsum dolor sit amet consectetur adipisicing elit.
        </p>
        <div>
            <p>
                Lorem, ipsum dolor sit amet consectetur adipisicing elit.
            </p>
            <p>
                selected tag is last child of. selected tag is last child
                of.
            </p>
        </div>
        <div>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing.</p>
            <span
                >Lorem ipsum dolor, sit amet consectetur adipisicing.</span
            >
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/5NkTYDqc/CSS-Selectors-last-child.png)



* :last-of-type

Selects every `<p>` element that is the last `<p>` element of its parent

```markup
<style>
    p:last-of-type {
        background: skyblue;
    }
</style>
</head>

<body>
    <h1>CSS Selectors</h1>
    <div class="contentsDiv">
        <p class="contents">
            Lorem ipsum dolor, sit amet consectetur adipisicing.
        </p>
        <p class="contents">
            selected type is last type in. selected type is last type in.
        </p>
        <div>
            <p class="contents">
                Lorem ipsum dolor, sit amet consectetur adipisicing.
            </p>
            <p class="contents">
                selected type is last type in. selected type is last type
                in.
            </p>
        </div>
        <div>
            <p>
                selected type is last type in. selected type is last type
                in.
            </p>
            <span
                >Lorem ipsum dolor, sit amet consectetur adipisicing.</span
            >
        </div>
    </div>
</body>
```

![](https://i.postimg.cc/GtfKtn0q/CSS-Selectors-last-of-type.png)

### 21. :nth-child\(n\), :nth-of-type\(n\)

{% embed url="http://nthmaster.com/" %}

#### Reference

{% embed url="https://www.w3schools.com/cssref/css\_selectors.asp" %}

