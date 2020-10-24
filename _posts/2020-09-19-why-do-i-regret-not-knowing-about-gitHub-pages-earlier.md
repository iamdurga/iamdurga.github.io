---
title:  "Why do i regret not knowing about GitHub Pages earlier?"
date:   2020-09-19 01:29:17 +0545
categories: github-pages
related_image: assets/scene.jpg
---

**Contents**
* TOC
{:toc}

## Introduction
A mathematics student from Nepal is about to write.

## Create GitHub account
Of course we need one account. Everyone knows how to make one.

## Download and Install Ruby
In order to maintain our project locally, it is necessary to download *Ruby*. I hope you can find it on rubyinstaller.org/downloads for your system. I am using windows right now so i will write about it. 

**Follow**: [Klit&Code](https://www.kiltandcode.com/2020/04/30/how-to-create-a-blog-using-jekyll-and-github-pages-on-windows/) for more hints.

**Note:** Please read more about installation on rubyinstaller.org for your easy setup. 

## Make First Jekyll Project
* First install jekyll.
    Do `gem install jekyll bundler` from terminal.
* Check your version if necessary by using -v argument. i.e. `jekyll -v`
* From the terminal `jekyll new path-to-project`.
* To view initial project, `bundle exec jekyll serve` then goto `http://localhost:4000`.

## Deploy it on GitHub
There are 2 ways, easy but slower, hard but faster. The easier way is using GitHub on browser and harder is GIT. To learn about GIT you can always go to pages like [this one](https://docs.gitlab.com/ee/gitlab-basics/start-using-git.html). I am going after easy part.

### Make a Repository
* Go to your GitHub account and make a new repository under the name :`your-github-username.github.io`. For me, `iamdurga.github.io`. 
* For easier setup, start with a Readme.md file.
* Then go to add files.
* Drag and drop the files you were working on earlier inside project folder.
* Then goto the new tab on browser and type `your-github-username.github.io` hit enter and TADAAAAA.

## Blogging
### Before writing a Math Blog
Just copy some files to your project from source theme. Type `bundle info minima` and hit enter to get onto minima directory. Goto that directory and copy the folders `_includes` and `_layouts` and paste them to project directory. 

#### On _config.yml
Add below code too.

`markdown: kramdown`<br>
`kramdown:`<br>
&ensp;`math_engine: mathjax`

[MathJax](https://www.mathjax.org) is awesome JS display engine that allows us to visualize Math Formulas. [Kramdown](https://kramdown.gettalong.org) according to developers is <i>kramdown (sic, not Kramdown or KramDown, just kramdown) is a free MIT-licensed Ruby library for parsing and converting a superset of Markdown. </i>

### Show Formula
Since i pretend to be Machine Learning guy, i have to write notations and symbols on blogs always so there is a better way of doing this by using MathJax. A Javascript Framework.

I searched and tried different solutions but none worked for me may be i was doing it on wrong way but finally i got through the post of [Ian Goodfellow](http://www.iangoodfellow.com/blog/jekyll/markdown/tex/2016/11/07/latex-in-markdown.html), father of GAN.

`<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>`

He suggested to use above code on `_includes/post.html` but seems putting it on top of `_includes/head.html` also works fine if we have formula on title too. It is not a magic but every blog page has stack of pages like header, footer etc.

### First Blog
* I hope you are a VS Code Fan. Goto the folder inside `_posts` of our project directory and create a new markdown file with the format like `2020-9-19-why-use-github-pages.md`.

* Then on the top of file, write somethinge like below:

    `---`<br>
    `layout: post `<br>
    `title:  "Why do i regret not knowing about GitHub Pages earlier?"`<br>
    `date:   2020-09-19 10:29:17 +0545`<br>
    `categories: jekyll update`<br>
    `---`

The above format is named as [front matter]https://jekyllrb.com/docs/front-matter/). The terms `layout`, `title` etc are known as variables. We can add our own varaibles to make more awesome blogs.
We can even use future date and the blog will be published on that date. The categories we used here will be automatically used on blog path by default. And the layout of this blog will be of post. It is interesting to see the file `_layouts/post.html`. We can only use layouts that are defined under that directory.
So the `$$ E=\frac{1}{2m} \sum_{i=0}^m {(y_i - t_i)^2} $$` is the LaTex code for RMS error on ML world.

$$ E=\frac{1}{2m} \sum_{i=0}^m {(y_i - t_i)^2} $$

Pretty Cool right?

## Make Awesome Posts
First thing we need is to make a custom category. Initially, we have only `jekyll`, you can see under the folder `_site`. But pretty thing is whenever we write a new post on markdown and give the category name different on the top bar(see above) then new category is made. But still the post will not be visible to the front page so what can we do is add a permalink on the `_config.yml`. i.e. `permalink: /:categories/:year/:month/:day/:title:output_ext`. Where `:categories` is placeholder for categories. Follow [this](https://jekyllrb.com/docs/permalinks/) official doc for more information.

## Add and View Comment
I scratched my head around for minutes and then i remembered some blogs where commenting was done by GitHub account. Jekyll is primarily used for static sites but comment falls under dynamic contents. There are various ideas though. Some people follows Disqus, and other stuffs. This [link](https://talk.jekyllrb.com/t/what-is-the-recommended-way-to-add-comment-sections-to-your-jekyll-blog/3330/6) contains a thread of commenting on Jekyll. And some people are smart to use GitHub's Issue as comment. Follow this [blog](https://aristath.github.io/blog/static-site-comments-using-github-issues-api) for more information. 


## Polish It
Sure the comments we are using right now is not that good. What we can do is add some CSS, JS and make it realtime commenting. But instead of that, i have used an awesome Jekyll theme [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/). I am using this same theme right now on this blog and i am more than gald to use it. I have seen many websites using this blog.