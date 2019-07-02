# Quotation

## blockquote

`<blockquote>` is used to define as block-level quotation. The `<blockquote>` is a block-level element, but it must contain other block-level elements such as `<p>`, not directly inline elements and text. You can specify the URI where quoted with cite attribute or use the title attribute to specify the title of the quote.

```markup
<blockquote title="HTML is... (description)">
    <p>
        HTML stands for Hyper Text Markup Language<br />
        HTML is the standard markup language for Web pages
    </p>
    <p>
        HTML elements are the building blocks of HTML pages<br />
        HTML elements are represented by &lt;&gt; tags
    </p>
    <footer>
        source:
        <cite
            ><a href="https://www.w3schools.com/whatis/whatis_html.asp">
                W3schools.com (website title) &gt; What is HTML? (child page
                title)</a
            ></cite
        >
    </footer>
</blockquote>
```

![](https://i.postimg.cc/CLsQhLW6/blockquote.png)



## q

Use `<q>` tag when quoting is required in inline

```markup
<p>Socrates said <q cite="www.example.com">Know yourself</q></p>
```

![](https://i.postimg.cc/vHb0Nwc7/q.png)

