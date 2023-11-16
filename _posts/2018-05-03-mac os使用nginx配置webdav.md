---
layout: article
title:  "mac os使用nginx配置webdav"
date: 2018-05-03 11:58
categories: other
tags: nginx config osx
---

1. 使用htpasswd创建用户名密码

```bash
htpasswd -bc .webdav username password
```
<!--more-->
2. 安装带有webdav module的nginx
```shell
brew tap denji/nginx
brew unlink nginx  ［此步骤是因为此前已经安装了nginx］
brew install nginx-full --with-webdav --with-dav-ext-module
brew link nginx-full
```
3. 修改nginx配置文件
  osx上使用brew安装的nginx配置在/usr/local/etc/nginx/nginx.conf
```
server {
    listen 10000;
    error_page 404 /404;
    error_page 503 /503;

    location / {
        root /Users/username/Documents/webdav;
        autoindex on;
        dav_methods PUT DELETE MKCOL COPY MOVE;
        dav_ext_methods PROPFIND OPTIONS;
        create_full_put_path on;
        dav_access user:rw group:r all:r;
        auth_basic "Authorized Users Only";
        auth_basic_user_file /Users/username/.webdav;
    }
}
```