<div align ="center">

<p><img src="./assets/images/banners/jekyll.jpg"  alt="jekyll"></p>

<h3>
  <a href="https://jekyllrb.com/" target="_blank"><code>Jekyll</code></a> theme for elegant writers.
</h3>


<a href="https://github.com/vanhiupun/Vanhiupun.github.io/actions/workflows/jekyll.yml" target="_blank">
    <img src="https://github.com/vanhiupun/Vanhiupun.github.io/actions/workflows/jekyll.yml/badge.svg"  alt="jekyll"/>
</a>
  
<!-- <a href="https://circleci.com/gh/vanhiupun/Vanhiupun.github.io/tree/master" target="_blank">
  <img src="https://circleci.com/gh/vanhiupun/Vanhiupun.github.io/tree/master.svg?style=shield" alt="circleci">
</a>  -->
  
<a href="https://github.com/vanhiupun/Vanhiupun.github.io/actions/workflows/codeql-analysis.yml" target="_blank">
  <img src="https://github.com/vanhiupun/Vanhiupun.github.io/actions/workflows/codeql-analysis.yml/badge.svg" alt="analysis">
</a> 
  
<a href="https://github.com/vanhiupun/Vanhiupun.github.io" target="_blank">
  <img src="https://www.codefactor.io/repository/github/vanhiupun/vanhiupun.github.io/badge" alt="CodeFactor" />
</a>

<a href="https://codeclimate.com/github/vanhiupun/Vanhiupun.github.io/maintainability">
  <img src="https://api.codeclimate.com/v1/badges/708da11ffb90a8f6f13b/maintainability" alt="maintainability" />
</a>

<a href="https://rubygems.org/gems/jekyll-theme-yat" target="_blank">
    <img src="https://badge.fury.io/rb/jekyll-theme-yat.svg"     alt="jekyll-theme-yat" />
</a> 

<a href="https://github.com/vanhiupun" target="_blank">
    <img src="https://img.shields.io/badge/Github%20Repository-222222?style=flat-square&logo=github&logoColor=ffffff"
     alt="Github" />
</a> 
      
<a href="https://vanhiupun.github.io" target="_blank">
    <img src="https://img.shields.io/badge/Github%20Page-222222?style=flat-square&logo=github&logoColor=ffffff" 
     alt="Blog" />
</a> 
      
<a href="mailto:fanxiaobin422@gmail.com" target="_blank">
    <img src="https://img.shields.io/badge/Send%20me%20Gmail-EA4335?style=flat-square&logo=Gmail&logoColor=ffffff" 
     alt="Gmail" />
</a> 
      
<a href="https://github.com/vanhiupun/Vanhiupun.github.io/blob/c0c037532393ee2718892f87b200a0bbe33e7eb9/License" target="_blank">
    <img src="https://img.shields.io/badge/License%20MIT-f2cb05?style=flat-square&logo=Mitsubishi&logoColor=222222" 
     alt="MIT" />
</a>
      
<a href="http://jekyllthemes.org/" target="_blank">
    <img src="https://img.shields.io/badge/Jekyll%20Themes-f2cb05?style=flat-square&logo=Jekyll&logoColor=222222" 
     alt="jekyll-themes" />
</a> 

<a href="https://github.com/jeffreytse/jekyll-theme-yat" target="_blank">
    <img src="https://img.shields.io/badge/Jekyll%C2%B7Theme%C2%B7Yat-f2cb05?style=flat-square&logo=github&logoColor=181717" 
     alt="Jekyll-yat" />
</a> 
  
<a href="https://raw.githubusercontent.com/vanhiupun/Vanhiupun.github.io/master/assets/images/img/zz.png" target="_blank">
    <img src="https://img.shields.io/badge/GitHub%20Sponsors-EA4335?style=flat-square&logo=GitHub%20Sponsors&logoColor=222222" 
     alt="/GitHub%20Sponsors" />
</a> 
  
</div>
<div align="center">
  <sub><a href="https://vanhiupun.github.io/jekyll/2021/11/20/制作和我一样的Jekyll博客.html" target="_blank">构建Jekyll博客</a>❤︎
  </sub>
</div>


<div align="center">
  <sub><a href="https://vanhiupun.github.io/" target="_blank">演示站点</a>
  </sub>
</div>

----

<div align="center">
<p><img src="./assets/images/readme/1.gif"  alt=""></p>
</div>

<div align="center">
<p><img src="./assets/images/readme/1.png"  alt="gif"></p>
</div>

<div align="center">
<p><img src="./assets/images/readme/3.png"  alt="gif"></p>
</div>

<div align="center">
<p><img src="./assets/images/readme/2.png"  alt="gif"></p>
</div>

----

#### 安装

```zsh
git clone git@github.com:vanhiupun/Vanhiupun.github.io.git
```

#### 设置环境

1.您将需要[Ruby](https://www.ruby-lang.org/zh_cn/)和[Bundler](https://bundler.io/)才能使用[Jekyll](https://www.jekyll.com.cn/)。遵循使用 [Jekyll 和 Bundler](https://jekyllrb.com/tutorials/using-jekyll-with-bundler/)来满足环境要求。

2.要设置您的环境来开发此主题，请运行`bundle install`.

3.要测试您的主题，请运行`bundle exec jekyll serve`并打开您的浏览器[http://localhost:4000](http://localhost:4000)
这将使用您的主题启动 Jekyll 服务器。
像往常一样添加页面、文档、数据等来测试您的主题内容。当您对主题和内容进行修改时，您的站点将重新生成，刷新后您应该会看到浏览器中的更改

当你的主题被释放，只有在文件中`_data`，`_layouts`，`_includes`，`_sass`和`assets`使用 Git 跟踪将被捆绑在一起。
要将自定义目录添加到您的主题宝石，请相应地编辑正则表达式`jekyll-theme-yat.gemspec`。

#### 开始

你可以通用修改`_config.yml`文件来轻松的开始搭建自己的博客:

```yaml
title: Vanhiupun blog  # 你的博客网站标题

email: fanxiaobin422@gamil.com # 你的邮箱

author: Vanhiupun # 你的名字

baseurl: "" # 网站的子路径，e.g. /blog

url: "" # 站点的基本主机名和协议，e.g. http://example.com

favicon: "/favicon.png" # 网站的图标 使用绝对路径e.g. /favicon.png，不推荐使用./favicon.png

# 分页设置
paginate: 5 #在主页显示5篇文章

# 摘录大小设置
excerpt_size: 250 #主页文章字数显示为250字

```

#### 撰写博文

要发表的文章一般以 Markdown 的格式放在这里`_posts/`，你只要看看这篇模板里的文章你就立刻明白该如何设置。

```yaml
---
layout: post #布局
title: 科学上网指南（二）：线路的区别与选择 #标题
categories: 科学上网 #分类
banner:
  image: https://vanhiupun.github.io/assets/images/banners/jichang.jpeg #图片地址 也可以使用 ./assets/images/banners/jichang.jpeg
  opacity: 0.618 #不透明度
  background: "#000" #背景颜色
  height: "50vh" #高度
  min_height: "50vh" #宽度
  heading_style: "font-size: 4.25em; font-weight: bold; " #标题样式
  subheading_style: "color: gold" #副标题样式
tags: [机场指南] #标签
---
```

#### Header Image

博客每页的标题底图是可以自己选的，看看几篇示例 post 你就知道如何设置了。

标题底图的选取完全是看个人的审美了。每一篇文章可以有不同的底图，你想放什么就放什么，最后宽度要够，大小不要太大，否则加载慢啊。

> 上传的图片最好先压缩，这里推荐 imageOptim 图片压缩软件，让你的博客起飞。

但是需要注意的是本模板的标题是**白色**的，所以背景色要设置为**灰色**或者**黑色**，总之深色系就对了。当然你还可以自定义修改字体颜色，总之，用 github pages 就是可以完全的个性定制自己的博客。

#### Customization

如果你喜欢折腾，你可以去自定义这个模板的 Code。

**如果你可以理解 `_include/ `和 `_layouts/`文件夹下的代码（这里是整个界面布局的地方），你就可以使用 `Jekyll` 使用的模版引擎 `Liquid`的语法直接修改/添加代码，来进行更有创意的自定义界面啦！**

#### Disqus 评论

国际比较流行，界面也很大气、简洁，如果有人评论，还能实时通知，直接回复通知的邮件就行了
需要去注册一个[Disqus 帐号](https://disqus.com/)。将我的账号替换成你的就可以

```yaml
# Disqus 评论
disqus:
  shortname: "vanhiupun" #在disqus注册一个账号 并将此处换成你自己的账号
```

#### Analytics

网站分析，现在支持[Google Analytics](https://analytics.google.com/analytics/web/)。需要去官方网站注册一下，然后将返回的 code 贴在下面：

```yaml
# Google Analytics
google_analytics: "UA-212989441-1"    # 你用Google账号去注册一个就会给你一个这样的id 将此处替换即可
```

## 贡献

如果你对这个项目感兴趣，你可以在以下任何一个方面做出贡献：
- 为这个项目加星
- 您可以[打开一个问题](https://github.com/vanhiupun/Vanhiupun.github.io/issues/new)，描述您要解决的问题，我们将从那里开始。
- 使用或测试，报告错误或发送补丁请求。
- 如果您的英语很好，请帮助我编写文档。
  
## 致谢

这个模板是从 [jeffreytse](https://github.com/jeffreytse/jekyll-theme-yat) Fork 的, 感谢这个作者。:+1:

## License

遵循 MIT 许可证。有关详细,请参阅 [LICENSE](./License)。

## 相关资源

[演示站点](https://vanhiupun.github.io)

[构建Jekyll博客](https://vanhiupun.github.io/jekyll/2021/11/20/制作和我一样的Jekyll博客.html)

[Jekyll详细搭建过程](https://vanhiupun.github.io/jekyll/2021/11/16/一步一步创建Jekyll主题.html)
