# meta Tag

## Character code set `<meta charset = "utf-8">`

This meta tag must be placed before `<title>`, and rest of all meta tags can be placed whether before or after the `<title>`.   
   


```markup
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <title>Page Title</title>
    </head>
</html>
```

#### `<meta name="">`

* `<meta name = "keywords" content="keyword1, keyword2>`
  * Enter the "keyword" in "content" by ",".
* `<meta name="description" content="A description of the page">` \(Important for SEO\)
  * This tag provides a short description of this page \(when you are searching in Google, so provide different description for each page\)
  * Ex\) `<meta name="Description" CONTENT="author: name, category: Book, Price: $10.25, pages: 500pages">`
  * Featured snippets in search: [https://support.google.com/webmasters/answer/6229325?hl=en](https://support.google.com/webmasters/answer/6229325?hl=en)
  * Create good titles and snippets in Search Results: [https://support.google.com/webmasters/answer/35624?hl=en](https://support.google.com/webmasters/answer/35624?hl=en)



## Robots meta tag `<meta name="robots" content="all">`

Not valid for all search engines.

* content = ""
  * all: default. Same as specifying 'index, follow'.
  * none: Same as specifying 'noindex, nofollow'.
  * index: The page is targeted for collection.
  * follow: The page and where the link is located are targeted for collection.
  * noindex: Exclude the page from collection.
  * nofollow: Exclude the page and where the link is located from collection.



## Robots meta tag `<meta property="">`

Detailed settings to show the link in various socials such as Open Graph, KakaoTalk, etc.

* `<meta property="og:title" content="Page Title">`
  * 우체국 EMS 요금, 국제택배 가격표 :\)
* `<meta property="og:url" content="http://site URL/">`
* `<meta property="og:image" content="http://be displayed image">`
* `<meta property="og:image:width" content="200">`
* `<meta property="og:image:heigth" content="200">`
* `<meta property="og:image:type" content="image/jpeg">`
* `<meta property="og:type" content="website">`
  * ex\) website, article, etc.
* `<meta property="og:description" content="site description">`
  * 한국에서 파리로 택배 붙힐일이 더 많이 생길 것……

Example picture

![](https://i.postimg.cc/NFFGq7J0/meta-property-og.png)



## Other useful meta tags

* `<meta name="author" content="Woochul Hyun">`
* `<meta name="generator" content="what framework you used">`
  * ex\) bootstrap, wordpress
* `<meta name="copyright" content="(c)abc.com">`
* `<meta name="reply-to" content="abc@gmail.com">`
* `<meta name="date" content="2019-04-23T17:54:00+09:00">`
* `<meta http-equiv="X-UA-Compatible" content="IE=edge">`
  * to make latest version of explorer be applied
* `<meta name="viewport" content="width=device-width,initial-scale=1">`
  * for Responsive website
* `<meta http-equiv="refresh" content="10”>`
  * Site is going to be updated at every specified times \(here 10sec\)
* `<meta http-equiv="refresh" content="10; url=http://example.com/">`
  * after the certain period of time \(here 10sec\), site will be redirected to example site \(useful tag when you are checking, fixing your site\)



## Example Code

```markup
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <title>Page Title</title>
        <meta name="keywords" content="" />
        <meta name="description" content="" />
        <meta name="author" content="" />
        <meta name="generator" content="" />
        <meta name="robots" content="" />

        <meta property="og:title" content="page_title" />
        <meta property="og:url" content="http://site_url/" />
        <meta property="og:image" content="http://Image_url" />
        <meta property="og:image:width" content="200" />
        <meta property="og:image:heigth" content="200" />
        <meta property="og:image:type" content="image/jpeg" />
        <meta property="og:type" content="website" />
        <meta property="og:description" content="site_description" />

        <meta name="viewport" content="width=device-width, initial-scale=1" />

        <link rel="stylesheet" type="text/css" media="screen" href="main.css" />
        <script defer src="main.js"></script>
    </head>
    <body></body>
</html>
```

