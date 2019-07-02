# abbr, dfn, cite, small

## abbr

`<abbr>` represents an abbreviation or acronym, optionally representing its extension. You can use the "title" attribute to indicate the original words of abbreviation. When using "title" attributes, only the original words of the abbreviation should be included.

```markup
<h1>abbr element</h1>

<p>
    <abbr title="Web Hypertext Application Technology Working Group"
        >WHATWG</abbr
    >
    is a community of people interested in evolving HTML and related
    technologies. The WHATWG was founded by individuals from Apple Inc., the
    Mozilla Foundation and Opera Software, leading Web browser vendors, in 2004.
    Since then, the editor of the WHATWG specifications, Ian Hickson (originally
    with Opera), has moved to Google.
</p>
<p>
    HTML5 is a
    <abbr title="World Wide Web Consortium">W3C</abbr> Recommendation
</p>
```

![](https://i.postimg.cc/QdJqxxc9/abbr.png)



## dfn

`<dfn>` represents the definition of a word. The closest ancestor element of a `<dfn>` \(ex. A paragraph, a definition list group, a section\) must contain a description of the word given in the dfn element.

```markup
<h1>dfn element</h1>

<p><abbr title="Hypertext Markup Language">html</abbr></p>
<p>
    <dfn
        title="Hypertext Markup Language, a standardized system for taggintext files to achieve font, color, graphic, and hyperlink effects oWorld Wide Web pages."
        >html</dfn
    >
</p>
```

![](https://i.postimg.cc/0ykwnGJj/dfn.png)

## cite

`<cite>` represents the title of any work. Works are, for example, books, essays, poems, scores, songs, scripts, films, TV shows, games, statues, paintings, movies, plays, operas, musicals and exhibitions. You may have cited works, citation detailedly, or just briefly mentioned them.

```markup
<h1>cite element</h1>

<ol>
    <li><cite>moves like jagger</cite> Maroon 5</li>
    <li><cite>hey jude</cite> Beatles</li>
</ol>
```

![](https://i.postimg.cc/hPFwXvQp/cite.png)



## small

`<small>` represents a side comment, such as a small print.

```markup
<h1>small element</h1>

<p>
    The price of 1 box of apples is 20 dollars
    <small>(tax not included in price)</small>
</p>
```

![](https://i.postimg.cc/xTxzsJGP/small.png)

