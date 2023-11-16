---
layout: article
title:  "解压cocos creator代码"
date: 2020-04-22 17:02
categories: other
tags: dev game cocos
---



```js
var fs = require("fs");
var app = require("electron").remote.app;

// example usage : copyFileOutsideOfElectronAsar("editor", '/Users/user/Downloads/tmp')

var copyFileOutsideOfElectronAsar = function(sourceInAsarArchive, destOutsideAsarArchive) {
if ( fs.existsSync( app.getAppPath() + "/" + sourceInAsarArchive ) ) {

    // file will be copied
    if ( fs.statSync( app.getAppPath() + "/" + sourceInAsarArchive ).isFile() ) {
        fs.writeFileSync(destOutsideAsarArchive, fs.readFileSync( app.getAppPath() + "/" + sourceInAsarArchive ));
    }
    // dir is browsed
    else if ( fs.statSync( app.getAppPath() + "/" + sourceInAsarArchive ).isDirectory() ) {
        fs.readdirSync( app.getAppPath() + "/" + sourceInAsarArchive ).forEach(function(fileOrFolderName) {
           fs.existsSync(destOutsideAsarArchive) || fs.mkdirSync(destOutsideAsarArchive);
           copyFileOutsideOfElectronAsar( sourceInAsarArchive + "/" + fileOrFolderName, destOutsideAsarArchive + "/" + fileOrFolderName );
        });
    }
  }
}

```
将此代码复制到cocos creator的console中, 然后执行
```js
copyFileOutsideOfElectronAsar("", '/Users/user/Downloads/tmp')
```

在console中输入app.getPath("temp")可获取路径

