---
title: hexo博客上传图片
tags: hexo
categories: 博客
abbrlink: 10557
date: 2018-11-22 12:38:39
---

#### 今天想写博客，突然发现要用到图片，然而自己却不会上传，于是就拜托了谷歌大神。一开始下载了插件之后，发现不好用，于是用了七牛云。七牛云很麻烦，还要实名认证。所以我还是决定用插件来操作。话不多说，看操作。
#### 1.首先把hexo下的_config.yml下的post_asset_folder改为true
#### 2.在hexo目录下git bash here
<!--more-->
```
npm install hexo-asset-image --save
```
#### 3.之后你再hexo n “博客名”生成md博客时，在_post目录下会生成一个与博客名相同的文件夹。

#### 4.将想要上传的图片放到文件夹下，用markdown插入图片：
```
![想输入的文字](文件夹名/图片名.jpg)
```
#### 5.用hexo上传博客。
##### 一波小小的福利
 ![福利](./hexo博客上传图片/test.jpg)
<!--more-->