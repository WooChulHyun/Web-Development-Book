# Table

### Table

Tables \(`<table>`, `<tr>`, `<th>`, and `<td>`\)

When creating a table, use the `<table>` which is block-level element. The basic structure of the table is, first defines a table row as a `<tr>`, and encloses the whole table elements include a table header cell as a `<th>` and a data cell as a `<td>` in `<table>`

The title of the table uses the `<caption>` after the start `<table>`.

Use `<thead>`, `<tbody>`, and `<tfoot>` to group rows in a table.

You can specify the scope attribute to tell `<th>` to be a heading in which direction, and use id and headers to clarify the relationship.



### Basic Table

```markup
<table border="1">
    <caption>
        Title of table (description)
    </caption>
    <thead>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="row">result</th>
            <td>...</td>
            <td>...</td>
            <td>...</td>
        </tr>
    </tfoot>
</table>
```

![](https://i.postimg.cc/JzDC7DC5/table1.png)



### colspan Table

```markup
<table border="1">
    <caption>
        Title of table (description)
    </caption>
    <thead>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="row">result</th>
            <!-- colspan -->
            <td colspan="3">...</td>
            <!-- <td>...</td> -->
            <!-- <td>...</td> -->
        </tr>
    </tfoot>
</table>
```

![](https://i.postimg.cc/q7Q7y6g6/table2.png)



### rowspan Table

```markup
<table border="1">
    <caption>
        Title of table (description)
    </caption>
    <thead>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>table data cell</td>
            <!-- rowspan -->
            <td rowspan="2">table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
        <tr>
            <td>table data cell</td>
            <!-- rowspan -->
            <!-- <td>table data cell</td>  -->
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="row">result</th>
            <td>...</td>
            <td>...</td>
            <td>...</td>
        </tr>
    </tfoot>
</table>
```

![](https://i.postimg.cc/cHr8JBTL/table3.png)



### colgroup Table

```markup
<!-- table width="30%" -->
<table border="1" width="30%">
    <caption>
        Title of table (description)
    </caption>
    <!-- width % We do not have to fill % in every col width // (*) -->
    <colgroup>
        <col width="*" />
        <col width="20%" />
        <col width="20%" />
        <col width="20%" />
    </colgroup>
    <thead>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
            <th scope="col">table header cell</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
        <tr>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
            <td>table data cell</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <!-- <th> scope = "col" || "row" || "colgroup" || "rowgroup" -->
            <th scope="row">result</th>
            <!-- colspan -->
            <td colspan="3">...</td>
            <!-- <td>...</td> -->
            <!-- <td>...</td> -->
        </tr>
    </tfoot>
</table>
```

![](https://i.postimg.cc/59z6k0RT/table4.png)



### Example Table

```markup
<table border="1" width="30%"">
    <colgroup>
        <col width="13%" />
        <col width="13%" />
        <col width="13%" />
        <col width="13%" />
        <col width="13%" />
        <col width="*" />
    </colgroup>
    <thead>
        <tr>
            <th>text</th>
            <th>text</th>
            <th>text</th>
            <th>text</th>
            <th>text</th>
            <th></th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th colspan="6">
                <table border="3" width = "100%">
                    <colgroup>
                        <col width="60%" />
                        <col width="*" />
                    </colgroup>
                    <tbody>
                        <tr>
                            <td rowspan="3">
                                Lorem ipsum dolor sit amet1.
                            </td>
                            <td>Lorem ipsum dolor sit amet2.</td>
                        </tr>
                        <tr>
                            <!-- <td>table data cell</td> -->
                            <td>Lorem ipsum dolor sit amet3.</td>
                        </tr>
                        <tr>
                            <!-- <td>table data cell</td> -->
                            <td rowspan="2">
                                image2
                            </td>
                        </tr>
                        <tr>
                            <td rowspan="3">image1</td>
                            <!-- <td>table data cell</td> -->
                        </tr>
                        <tr>
                            <!-- <td>table data cell</td> -->
                            <td>======</td>
                        </tr>
                        <tr>
                            <!-- <td>table data cell</td> -->
                            <td>image3</td>
                        </tr>
                    </tbody>
                </table>
            </th>
        </tr>

        <tr>
            <th colspan = "6">
                <table border="1" width = "100%">
                    <thead>
                        <tr>
                            <th scope="col">text</th>
                            <th scope="col">text</th>
                            <th scope="col">text</th>
                            <th scope="col">text</th>
                        </tr>
                    </thead>

                    <tbody>
                        <tr>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                        </tr>
                        <tr>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                        </tr>
                        <tr>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                        </tr>
                        <tr>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                            <td>table data cell</td>
                        </tr>
                    </tbody>
                </table>
            </th>
        </tr>
    </tbody>
</table>
```

![](https://i.postimg.cc/pd92hcN4/table5.png)

