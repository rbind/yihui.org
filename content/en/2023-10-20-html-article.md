---
title: A Simple HTML Article Format
date: '2023-10-20'
slug: html-article
---

A couple of weeks ago I wrote about a lightweight HTML presentation format,
[snap slides](/en/2023/09/snap-slides/). Today I want to briefly introduce a
simple and lightweight HTML article format. You can find [an example page
here](https://yihui.org/litedown/), which is also its documentation. You can
generate an article like this with either the R package **litedown** or Quarto
or any other tool that can generate HTML output. Under the hood, this article
format is based on CSS and JS, which can be reused on any web pages.

If you use R Markdown or plain Markdown, you can `install.packages('litedown')`
and specify the output format:

``` yaml
output:
  litedown::html_format:
    meta:
      css: ["default", "@article"]
      js: ["@sidenotes", "@appendix"]
```

If you use Quarto, you can also include the relevant CSS and JS:

``` yaml
format:
  html:
    minimal: true
    toc: true
    include-after-body:
      text: |
        <script src="https://cdn.jsdelivr.net/npm/@xiee/utils/js/sidenotes.min.js" defer></script>
        <script src="https://cdn.jsdelivr.net/npm/@xiee/utils/js/appendix.min.js" defer></script>
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@xiee/utils/css/default.min.css">
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@xiee/utils/css/article.min.css">
        <style type="text/css">header{text-align: center;}</style>
```

If you use other HTML generators, you can reuse the HTML code in the above
Quarto example (in the `text` field).

The main features of this article format are: side elements (TOC, footnotes,
sidenotes, and references), full-width elements, floating quotes, margin
embedding, and appendices. Again, you can read [its
documentation](https://yihui.org/litedown/#sec:html-articles) to know more.
