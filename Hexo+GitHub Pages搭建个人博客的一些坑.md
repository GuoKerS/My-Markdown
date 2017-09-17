---
title: Hexo+GitHub Pages搭建个人博客的一些坑
tags: Hexo,坑,小计
grammar_cjkRuby: true
---
----------
**一、前言**
由于之前使用的都是免费博客，一段时间又不经常更新导致博客已失效。考虑到能够折腾的种种因素，最终跟风的选择了Hexo来搭建博客，共耗时2天。写下此文的目的是为了记录下我搭建过程中解决的一些坑，给需要的同学做个参考。



**二、准备工作**
先说下搭建Hexo的完整流程：
# <center> 流程图
``` flow!
st=>start: 环境准备
e=>end: 结束
op1=>operation: 安装Node.js、Git、Npm、Hexo
op2=>operation: 本地调试、预览Hexo、美化主题、插件安装
op3=>operation: 部署至Github Pages
st ->op1 ->op2 ->e
```
本机环境：Ubuntu 
**三、系统环境配置**

 1. 安装Node.js

``` zsh
sudo apt-get install nodejs #安装node.js
node -v #显示版本信息
```

 2. 安装Git

``` zsh?linenums
sudo apt-get install git #安装github
git --version #显示git版本
```


 3. 安装Npm（Cnpm）

``` zsh
sudo apt-get install npm #安装.......
npm -v #显示........
```
由于npm在国内的下载速度极慢（下载Hexo我楞是等待了1个多小时！），在查阅资料后我得知使用淘宝分流的npm后速度倍增，因此后续有关npm的命名都将有cnpm代替。

``` zsh
npm install cnpm -g --registry=https://registry.npm.taobao.org #安装cnpm
```

 4. 安装Hexo
 
 
 