## 博客简介

写自己的东西，记录一切有意思的事。

## 博客链接

[我的博客地址](https://peony7.github.io/hexo-blog/)

## bash 命令

```
//创建文章
$ hexo new "new-artical"

//创建草稿(私密文章)
$ hexo new draft "new draft"

//预览草稿
$ hexo server --drafts
```

## 遇到的一些坑

**hexo-asset-image 插件**

```js
//index.js中的44行
$(this).attr('src', '/' + link + src);
//修改如下
$(this).attr('src', config.root+'/' + link + src);
```