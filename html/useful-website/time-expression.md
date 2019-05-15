# Time Expression

### Time

`<time>` tag let computer know the time precisely and we can also know it through the code, but not directly on the screen.

| Time | Description |
| :--- | :--- |
| 2019 | Year |
| 2019-04 | Year – Month |
| 2019-04-24 | Year – Month – Day |
| 2019-04-24T17:00 | Year – Month – Day Hour : Minute |
| 2019-04-24T17:00:00 | Year – Month – Day Hour : Minute : Second |
| 2019-04-24T17:00:00.000 | Year – Month – Day Hour : Minute : Second : Millisecond |
| 2019-04-24T17:00+09:00 | Coordinated Universal Time \(UTC\) |



### Example

```markup
<body>
    <p>I exercise every day at <time datetime="19:00">7P.M.</time></p>
    <p>I exercise every day at <time>19:00</time>.</p>
    <p><time datetime="2019-03-01">Today</time>is John's birthday.</p>
</body>
```

![](https://i.postimg.cc/rmNqgwYk/time.png)

