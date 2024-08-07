---
title: 'A Special Graphics Device in R: the Null Device'
date: '2010-12-22'
slug: a-special-graphics-device-in-r-the-null-device
---

Update on 2024-07-04

:   Since Mehrad discovered and mentioned this post [on Mastodon](https://mastodon.social/@Mehrad@fosstodon.org/112728074463012723), I want to point out that the null device has been [officially introduced into R](https://cran.r-project.org/doc/manuals/r-release/NEWS.2.html#:~:text=pdf()%20accepts%20file%20%3D%20NULL) since v2.15.0 (2012-03-30), so you can set:
    ```r 
    options(device = function(...) {
      pdf(NULL, ...)
    })
    ```

    The `R_GD_nullDevice` was said [to be removed in the future](https://cran.r-project.org/doc/manuals/r-release/NEWS.2.html#:~:text=.Call(%22R_GD_nullDevice%22%2C%20package%20%3D%20%22grDevices%22)%20is%20about%20to%20be%20removed), so you'd better not use it any more.

It is well-known that R has several graphics devices -- either the screen devices (`X11()`, `windows()`, ...) or the off-screen devices (`pdf()`, `png()`, ...). We can query the default graphics device in `options()`:

```r 
getOption('device')
```

In a non-interactive session, the default device is `pdf()`. This is why Sweave has to create a file named `Rplots.pdf` _no matter if you want it or not_ when you run Sweave on an Rnw file which has code chunks creating plots. Such a behaviour is annoying to me -- the PDF file is not only unnecessary, but also time-consuming (creating this PDF file is completely a waste of time). Is there a way to set a "null" device? (like the `/dev/null` for *nix users) The answer is yes, but not so obvious. I have not found the device below documented anywhere:

```r 
options(device = function(...) {
    .Call("R_GD_nullDevice", PACKAGE = "grDevices")
})
```

This device can speed up Sweave a lot when there are many plots to draw. Here is a comparison:

```r 
x = rnorm(1000)
system.time({
    .Call("R_GD_nullDevice", PACKAGE = "grDevices")
    replicate(500, plot(x, pch = 1:21))
    dev.off()
})
#   user  system elapsed
#   1.51    0.02    1.53
system.time({
    pdf(file.path(tempdir(), "Rplots.pdf"))
    replicate(500, plot(x, pch = 1:21))
    dev.off()
})
#   user  system elapsed
#  47.81    0.20   48.10
```

One thing I don't understand in Sweave is that it evaluates the code chunk _twice_ if its Sweave options contain `fig=TRUE`. I think this might be a waste of time as well, and this is why I like [pgfSweave](http://cran.r-project.org/package=pgfSweave), which has both the mechanism of caching R objects (using **cacheSweave**) and a smart way to cache graphics (using pgf).

**WARNING**: this null device may not work with plots that contain (math) expressions! (take a look at `demo(plotmath)` in case you do not know what are expressions in R graphics)

