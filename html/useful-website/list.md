# List

### ul, ol, li

In general, `<ul>`\(unordered list\) and `<ol>`\(ordered list\) tags are used to make list, and each item defines as `<li>`\(list item\).

Both `<ul>` and `<ol>` are block-level elements, but can not contain elements other than the `<li>`. The `<li>` is a block-level element that can contain inline elements and text, and can contain other block-level elements.

#### Example

```markup
<h1>Types of Cars</h1>
<ul>
    <li>
        Small Cars
        <ul>
            <li>Ford Focus</li>
            <li>Kia Rio</li>
            <li>Chevrolet Cruze</li>
        </ul>
    </li>
    <li>
        Compact Cars
        <ul>
            <li>Nissan Versa.</li>
            <li>Nissan Sentra</li>
        </ul>
    </li>
    <li>Midsize Car</li>
    <li>Full-size Car</li>
</ul>
<hr />
<h1>Process</h1>
<ol type="a">
    <!--type = i | I | a | A | 1 -->
    <li>step1</li>
    <li>step2</li>
    <li>step3</li>
    <li>step4</li>
    <li>step5</li>
</ol>
```

![](https://i.postimg.cc/htqyTYpY/ul-ol-li.png)



### dl, dt, dd

A list that consist of 'terms' and 'descriptions' is called a 'definition list'. The definition list is defined by `<dl>`, and includes `<dt>`\(definition term\) and `<dd>`\(definition description\).

`<dl>` is a block-level element, but it can not contain any elements other than the `<dt>` and `<dd>`. `<dt>` is an inline element and can contain inline elements and text. `<dd>` is a block-level element that can contain inline elements and text, and can also contain block-level elements.

`<dl>` must have at least one `<dt>` and `<dd>`.

Number of `<dt>` &lt;= number of `<dd>` is OK but number of `<dt>` &gt; number of `<dd>` is not suitable.

#### Example

```markup
<dl>
    <dt><strong>HTML</strong></dt>
    <dd>
        <p>
            HTML stands for Hyper Text Markup Language, HTML is the standard
            markup language for Web pages, <br />HTML elements are the building
            blocks of HTML pages, HTML elements are represented by &lt;&gt; tags
        </p>
    </dd>
    <dt><strong>CSS</strong></dt>
    <dd>
        <p>
            CSS stands for Cascading Style Sheets, CSS describes how HTML
            elements are to be displayed
        </p>
    </dd>
</dl>
```

![](https://i.postimg.cc/DZVcsjQZ/dl-dt-dd.png)

