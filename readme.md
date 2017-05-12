## 博客简介

写自己的东西，记录一切有意思的事。

## 博客链接

[我的博客地址](https://peony7.github.io/hexo-blog/)

## bash 命令

```bash
# 创建文章
$ hexo new "new-artical"

# 创建草稿(私密文章)
$ hexo new draft "new draft"

# 预览草稿
$ hexo server --drafts

# 启动本地服务
$ npm run start

# 清理文件
$ npm run clean

# 生成文件
$ npm run generate

# 发布网站
$ npm run deploy
```

## 遇到的一些坑

**hexo-asset-image 插件**

```js
//index.js中的44行
$(this).attr('src', '/' + link + src);
//修改如下
$(this).attr('src', config.root+'/' + link + src);
```
**插入图片**

```markdown
# img前后必须加上**，否则网站上图片显示不正确
**![img](css-variable/bg2017050901.jpg)**
```

**修改主题的样式**

配置文件路径：`themes/indigo/_confit.yml`

```yaml
# 设置为 true 发布后将使用 unpkg cdn
cdn: false
```



