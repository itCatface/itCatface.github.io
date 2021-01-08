---
# 说明

## _layouts目录

- default.html
    
    ```html
    <!DOCTYPE html>
    <html lang="en">
    {% include head.html %}
    <body>
    {% include nav.html %}
    {% include search.html %}
    {{ content }}
    {% include footer.html %}
    </body>
    </html>
    ```
 
    > 包含顶部导航搜索+html页面content+底部sns、copyright

- keynote.html

    > 包含顶部导航搜索iframe幻灯片(没有的话是大片灰色背景图)+html页面content+底部featured tags、友情链接、底部sns、copyright

- page.html

    > 包含顶部导航搜索博文标题及标题背景图+html页面content+右边featured tags、关于catalog目录、sns、友情链接+底部sns、copyright

- post.html

    > 包含顶部导航搜索博文标题副标题发布时间及标题背景图+html页面content+右边catalog目录+底部畅言评论热门话题、featured tags、友情链接、底部sns、copyright





---
[Hux Blog](https://huangxuan.me)
================================

> I never expected this becomes popular.

![](http://huangxuan.me/img/blog-desktop.jpg)


[User Manual 👉](_doc/Manual.md)
--------------------------------------------------

### Getting Started

1. You will need [Ruby](https://www.ruby-lang.org/en/) and [Bundler](https://bundler.io/) to use [Jekyll](https://jekyllrb.com/). Following [Using Jekyll with Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/) to fullfill the enviromental requirement.

2. Installed dependencies in the `Gemfile`:

```sh
$ bundle install 
```

3. Serve the website (`localhost:4000` by default):

```sh
$ bundle exec jekyll serve  # alternatively, npm start
```

### Development (Build From Source)

To modify the theme, you will need [Grunt](https://gruntjs.com/). There are numbers of tasks you can find in the `Gruntfile.js`, includes minifing JavaScript, compiling `.less` to `.css`, adding banners to keep the Apache 2.0 license intact, watching for changes, etc. 

Yes, they were inherited and are extremely old-fashioned. There is no modularization and transpilation, etc.

Critical Jekyll-related code are located in `_include/` and `_layouts/`. Most of them are [Liquid](https://github.com/Shopify/liquid/wiki) templates.

This theme uses the default code syntax highlighter of jekyll, [Rouge](http://rouge.jneen.net/), which is compatible with Pygments theme so just pick any pygments theme css (e.g. from [here](http://jwarby.github.io/jekyll-pygments-themes/languages/javascript.html) and replace the content of `highlight.less`.


### Interesting to know more? Checkout the [full user manual](_doc/Manual.md)!


Other Resources
---------------

Ports
- [**Hexo**](https://github.com/Kaijun/hexo-theme-huxblog) by @kaijun
- [**React-SSR**](https://github.com/LucasIcarus/huxpro.github.io/tree/ssr) by @LucasIcarus

[Starter/Boilerplate](https://github.com/huxpro/huxblog-boilerplate)
- Out of date. Helps wanted for updating it on par with the main repo

Translation
- [🇨🇳 (somewhat outdated)](https://github.com/Huxpro/huxpro.github.io/blob/master/_doc/README.zh.md)


License
-------

Apache License 2.0.
Copyright (c) 2015-present Huxpro

Hux Blog is derived from [Clean Blog Jekyll Theme (MIT License)](https://github.com/BlackrockDigital/startbootstrap-clean-blog-jekyll/)
Copyright (c) 2013-2016 Blackrock Digital LLC.
