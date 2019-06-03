# GitBook on GitHub

### GitBook

For the GitBook, there are two ways to create a GitBook. One is a self-hosted service provided by [https://gitbook.io](https://gitbook.io), and other is a GitBook project that creates static sites as open source.

Here we will create a GitBook through the Github page.

### GitHub Page

There are three main ways to host Github Pages.

1. The master branch of the repo named username.github.io.
2. Any repo with docs folder.
3. Any repo with gh-pages branch.

We will create a gitBook with second way, any repo with docs folder.

* Create a repository.

![](https://i.postimg.cc/15XRkcsK/repoMain.png)

* Connect local Git and github via `git clone` or `git init`.
* On the settings page, activate the page with master branch.

![](https://i.postimg.cc/Gt5RLVdx/github-setting-page.png)

### GitBook installation

First of all, because the GitBook is based on node.js, node and npm should be installed in the system. npm is usually installed with node.js.

Now that you have npm installed on your system, install `gitbook-cli` with the following command:

I will display the branch name together. Just copy the code after $.

```bash
(master) $ npm install -g gitbook-cli
```

When the installation is complete, run the gitBook init command from the project directory.

```bash
(master) $ gitbook init
```

After running, there will be README.md and SUMMARY.md files in the project directory.

```bash
// README.md
# Introduction


// SUMMARY.md
# Summary

* [Introduction](README.md)
```

You can build and upload directly using `gitbook build` command, but that can make it inconvenient to manage your project directory structure and files built.

So let's split the branches that make up the markdown and the files that we build into.

```bash
(master) $ git add .

(master) $ git commit -m "init gitbook"

(master) $ git branch docs
```

Now, we committed the files created by gitbook init, and created the docs branch.

This docs branch will be the branch we will use to write down the markdown files, and the existing master branch will be used to build the gitbook and host the built-in html files.

Before we checkout, let's build it once. \(You do not have to follow\)

```bash
(master) $ gitbook build
```

After you build, you will have a \_book directory.

```bash
_book/  <----
  gitbook/
  index.html
  search_index.json
README.md
SUMMARY.md
```

Because the files in the \_book directory are the files you need to host, you have to get them out.

```bash
(master) $ cp -R _book/* .
```

```bash
gitbook/
index.html
search_index.json
README.md
SUMMARY.md
```

After pushing in this state, connect to the URL of the page and the following screen appears.

Please note that it may take some time to push and apply to the github page.

![](https://i.postimg.cc/1z5R0LJs/gitbook-first-page.png)

### GitBook adding file

Go to the docs branch.

```bash
(master) $ git checkout docs
```

Add the md file to the docs folder \(docs folder and docs branch is different\)

![](https://i.postimg.cc/HnWtTWtF/gitbook-docs-folder-files.png)

Now change the SUMMARY.md file as follows:

```bash
# Summary

-   [Introduction](README.md)

-   [HTML](docs/HTML/index.md)

    -   [Useful Website](docs/HTML/useful_website.md)
    -   [meta Tag](docs/HTML/meta_tag.md)
    -   [Block, Inline Elements](docs/HTML/block_inline_elements.md)
        (omit)

-   [CSS](docs/CSS/index.md)

    -   [Useful Website](docs/CSS/useful_website.md)

-   [JavaScript](docs/JavaScript/index.md)

    (omit)
```

Since gitbook reads the summary file and builds the files in the list, you must add it to summary if you want to add it.

Now, after the commit, go to the master branch and build and push.

```bash
(docs) $ git add .
(docs) $ git commit -m "add files"

(docs) $ git checkout master

(master) $ git merge docs
(master) $ gitbook build
(master) $ cp -R _book/* .
(master) $ rm -r _book/

(master) $ git add .
(master) $ git commit -m "Update"
(master) $ git push origin master
```

After completing this process, the github page looks like this:

![](https://i.postimg.cc/L8rK5wwx/gitbook-example-page.png)

### Build your gitbook comfortably

Back to the docs branch again.

```bash
(master) $ git checkout docs
```

Then, add the `publish_gitbook.sh` file. The contents are as follows.

```bash
git checkout master
git merge docs

gitbook build

cp -R _book/* .
rm -r _book/

git add .
git commit -m "Update"
git push origin master

git checkout docs
```

Then execute the following commands. \(Just follow it once.\)

```bash
(docs) $ git add .
(docs) $ git commit -m "add script"
(docs) $ git checkout master

(master) $ git merge docs
(master) $ git checkout docs
```

From now on, when you edit something in your docs branch and build it on your gitbook, you can run it with a single command line `./publish_gitbook.sh`.

```bash
(docs) $ .\publish_gitbook.sh
```

If you want to preview your changes to the local server before publishing to the server,

```bash
(docs) $ gitbook serve
```

