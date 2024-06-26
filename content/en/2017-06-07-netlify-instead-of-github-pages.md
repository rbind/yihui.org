---
title: Consider Netlify instead of GitHub Pages for Your Static Websites
subtitle: GitHub Pages is Dead, Long Live Netlify!
date: '2017-06-07'
slug: netlify-instead-of-github-pages
---

If you do not have a personal website yet, congratulations! I think now is the best time to create a website.[^1] I started blogging in 2005, and benefited a lot from writing, although a lot of my blog posts were crap.[^2] I have used many website tools, including Dreamweaver, [Bo-Blog](http://www.bo-blog.com/index.php?l=en), WordPress, and Jekyll. Then I discovered [Hugo](https://gohugo.io), and created the [**blogdown**](https://github.com/rstudio/blogdown) package. I don't think I will need to change the tool in the next few years. The **blogdown** package is my own dog food anyway. I'm not going to say much about **blogdown** today, but just want to leave a friendly note to those who are starting their new websites:

> Do not use GitHub pages or the `*.github.io` subdomain. Use [Netlify](https://www.netlify.com) instead. Netlify is the new and much better GitHub pages.

I have outlined the reasons in [Section 3.3](https://bookdown.org/yihui/blogdown/github-pages.html) of the **blogdown** book. Netlify didn't pay me to say these words, and I was just amazed by their service (even the free plan is so awesome). I cannot praise Netlify too much in the book, because the book should stay as neutral as possible, but I think it is fine to be biased in my personal blog.

Actually here is a general philosophy for choose tools or services: you need to be careful about tools that you cannot leave, because you are likely to change your mind someday. You have to ask yourself a "what-if" question: what if this tool is dead someday or I don't want to use it any more? A few examples:

- If you do not want to use your `*.github.io` subdomain associated with your GitHub pages, you will be in trouble. It is not straightforward to redirect your web pages. By comparison, if you want to leave Netlify, you can [easily redirect](https://www.netlify.com/docs/redirects/) from `*.netlify.com` to your new website. Note Netlify does 301 or 302 redirects, which means search engines will know that your pages have been moved, so that they can index your new pages quickly.

- It is always easier to move from a simpler tool to a more complicated tool, and difficult in the opposite direction. That is one of the main reasons why I have been barking about Markdown these years. Start with Markdown, and you have plenty of choices if you want to leave. Start with LaTeX or Word, you are stuck there forever. Similarly, moving from Markdown to other tools like WordPress is easy, but it can be painful to come to the Markdown world from another world. I have my strong belief in plain-text files.

    Of course, you can ask "what if **blogdown** or Hugo is dead". Will you be stuck? I'd say it is unlikely. Your content is still in your own hands --- they are just a bunch of plain-text files (if you host a website via WordPress.com or similar services, you probably don't have this level of confidence). Any software can process plain-text files, and I'm pretty sure there will be smart software developers writing new tools to help you migrate your Hugo-based website if Hugo is dead for some reason.

- You may even ask "what if Netlify is dead". No worries. A static website means it is easy to publish it on almost any web servers. You can even publish it on GitHub pages (although it sounds weird), or Amazon S3, etc. Netlify cannot easily ruin your website or lock you in their room.

The reason that I say "Netlify is the new GitHub Pages" is that Netlify supports [continuous deployment](https://www.netlify.com/docs/continuous-deployment/), and you can choose from several static website generators, including Hugo. This means you just push to GitHub, and Netlify can automatically build your website from source and deploy it. That is very similar to how GitHub Pages works, except that GitHub Pages only supports Jekyll in terms of continuous deployment.[^3] I'm tired of the Ruby dependency hell. Hugo is a single binary with no dependencies. How cool is that?

So for those who still use or plan to use `*.github.io`, you may seriously consider moving to Netlify and actually purchasing your own domain name instead of using any of these free subdomains. A domain name is not that expensive (typically about 10 US dollars a year). Once you own a domain, you will have a lot of possibilities, such as an infinite amount of subdomains (depending on your nameservers) and your custom email accounts. I'd say it is totally worth it. Do not use those free `*.wordpress.com` or `*.tumblr.com` or Medium.com subdomains. Especially for those professors, I strongly recommend you not to use the old-fashioned `example.edu/~name` URLs. Set up your own domain to get rid of IT, and you won't need to change any URLs when you change your affiliation.

I have also seen folks publish **blogdown**-based websites to GitHub pages via Travis CI. I think that is a way too complicated workflow. Netlify has made things so much easier and faster (it often takes a few seconds to build and deploy my own website on Netlify).

In conclusion, my recommendations are:

1. Do not use the `*.github.io` subdomain. If you have to use a free subdomain, consider `*.netlify.com` instead, although I strongly recommend you to register your own domain if you can afford it.

1. Do not use GitHub pages, otherwise you are too closely tied to GitHub and you don't have much freedom to leave (that said, I do love GitHub very much).

1. Consider static websites instead of WordPress or Tumblr or Medium.com. If you have already been stuck there, move as early as possible. It is painful but there will be long-term benefits.

GitHub Pages has perfectly fulfilled its mission to promote static websites. I think it is time to let it go now.

[^1]: However, I do think it is too late to start a blog, because the whole society has been distracted by social media, which favors short, quick, debatable, misleading, and even fake messages. I feel there are much fewer people reading or commenting on blog posts now. That said, writing blog posts is still helpful, even if nobody reads your posts.

[^2]: I used to be young and naive. Now I'm different: old and naive.

[^3]: You can publish any HTML files generated by any static website generators to GitHub Pages, if you add a `.nojekyll` file under the root directory of your website repo. That is, you can use GitHub Pages as a static website host when you generate your web pages by yourself. However, if you want GitHub to build your website from source (Markdown), your only choice is Jekyll at the moment.
