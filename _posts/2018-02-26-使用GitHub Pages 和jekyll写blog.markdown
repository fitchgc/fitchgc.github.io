---
layout: article
title:  "使用GitHub Pages 和jekyll写blog"
date: 2018-02-26 23:24
categories: other
tags: git jekyll
---
1. 在https://github.com/new上create new repository, 名字为 username.github.io
2. 将项目clone到本地
```bash
git clone https://github.com/username/username.github.io
cd username.github.io
```
<!--more-->
3. 使用jekyll创建本地blog
```bash
#需要安装ruby
sudo gem install jekyll
#创建基本的项目
jekyll new .
#如果目录非空,
jekyll new . --force
#启动jekyll服务
jekyll serve
#通过http://localhost:4000访问页面
```
jekyll serve启动参数
--livereload 当有改动时候自动刷新页面
--incremental Incremental will perform a partial build in order to reduce regeneration time.
--detach 和jekyll serve类似, 但和当前terminal分离, 如果需要关闭服务, 输入kill -9 PID
--no-watch not watch for changes
[jekyll的文档](https://jekyllrb.com/docs/quickstart/)
4. 在_posts目录创建文件, 即可创建博客, 文件名格式为YYYY-MM-DD-title.markdown
5. 文件内容如下:
```markdown
---
layout: post
title:  "blog标题"
date: 发表日期
categories: other
---
博客内容, 支持markdown
```
layout: post 表示使用_layouts下的post模板来显示这篇blog
categories为分类, 可以使用site.posts.categories这样的标签来引用指定分类的博客
