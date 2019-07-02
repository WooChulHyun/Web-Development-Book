# GitBook Setting

## Create a book.json file

Create a book.json file in the same location as the SUMMARY.md and README.md files.

![](https://i.postimg.cc/63StVqmN/book-json.png)

File contents:

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    }
}
```



## Create Sidebar

 Edit book.json file like follow:

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    },
    "links": {
        "sidebar": {
            "GitHub": "https://github.com/WooChulHyun"
        }
    }
}
```

![](https://i.postimg.cc/FsGmGTqZ/sidebar.png)



## Create style sheet

By creating a stylesheet, you can decorate your GitBook with CSS.

Create a style file in the same location as the SUMMARY.md and README.md files.

![](https://i.postimg.cc/J4FY1JB8/style-sheet.png)

Edit book.json file:

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    },
    "links": {
        "sidebar": {
            "GitHub": "https://github.com/WooChulHyun"
        }
    },
    "styles": {
        "website": "styles/website.css"
    }
}
```



## Delete sharing icon

![](https://i.postimg.cc/zvV3549q/sharing-icon.png)

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    },
    "links": {
        "sidebar": {
            "GitHub": "https://github.com/WooChulHyun"
        }
    },
    "styles": {
        "website": "styles/website.css"
    },

    "plugins": ["-sharing"],
    "pluginsConfig": {
        "sharing": {
            "facebook": false,
            "twitter": false,
            "google": false,
            "all": ["facebook", "google", "twitter"]
        }
}
```

![](https://i.postimg.cc/h4ZqN2cP/sharing-delete-icon.png)



## Fontsettings

You can control the theme, font-family, and size of your GitBook.

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    },
    "links": {
        "sidebar": {
            "GitHub": "https://github.com/WooChulHyun"
        }
    },
    "styles": {
        "website": "styles/website.css"
    },

    "plugins": ["-sharing", "-fontsettings"],
    "pluginsConfig": {
        "sharing": {
            "facebook": false,
            "twitter": false,
            "google": false,
            "all": ["facebook", "google", "twitter"]
        },
        "fontsettings": {
            "theme": "white",
            "family": "sans",
            "size": 2
        }
    }
}
```



## Toggle Chapters

You can put a toggle effect in the sidebar chapter. `"plugins": ["toggle-chapters"]`

```text
{
    "title": "Web Development Book",
    "description": "HTML CSS JS CS 정리",
    "author": "Woochul Hyun",
    "language": "en, ko",
    "root": ".",
    "structure": {
        "summary": "SUMMARY.md"
    },
    "links": {
        "sidebar": {
            "GitHub": "https://github.com/WooChulHyun"
        }
    },
    "styles": {
        "website": "styles/website.css"
    },

    "plugins": ["-sharing", "-fontsettings", "toggle-chapters"],
    "pluginsConfig": {
        "sharing": {
            "facebook": false,
            "twitter": false,
            "google": false,
            "all": ["facebook", "google", "twitter"]
        },
        "fontsettings": {
            "theme": "white",
            "family": "sans",
            "size": 2
        }
    }
}
```

