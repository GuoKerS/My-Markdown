---
title: Hexo+GitHub Pages搭建个人博客的一些坑
tags: Hexo
grammar_cjkRuby: true
---
----------
# 一、前言
由于之前使用的都是免费博客，一段时间又不经常更新导致博客已失效。考虑到能够折腾的种种因素，最终跟风的选择了Hexo来搭建博客，共耗时2天。写下此文的目的是为了记录下我搭建过程中解决的一些坑，给需要的同学做个参考。



# 二、准备工作
先说下搭建Hexo的完整流程：

``` flow
st=>start: 环境准备
e=>end: 结束
op1=>operation: 安装Node.js、Git、Npm、Hexo
op2=>operation: 本地调试、预览Hexo、美化主题、插件安装
op3=>operation: 部署至Github Pages
st ->op1 ->op2 ->e
```
本机环境：Ubuntu 

# 三、系统环境配置

##  1. 安装Node.js

``` zsh
sudo apt-get install nodejs #安装node.js
node -v #显示版本信息
```

##  2. 安装Git

``` zsh?linenums
sudo apt-get install git #安装github
git --version #显示git版本
```


 ## 3. 安装Npm（Cnpm）

``` zsh
sudo apt-get install npm #安装.......
npm -v #显示........
```
由于npm在国内的下载速度极慢（下载Hexo我楞是等待了1个多小时！），在查阅资料后我得知使用淘宝分流的npm后速度倍增，因此后续有关npm的命名都将有cnpm代替。

``` zsh
npm install cnpm -g --registry=https://registry.npm.taobao.org #安装cnpm
```

 ## 4. 安装Hexo
 
 

``` zsh
mkdir hexo #创建hexo目录
cd hexo 
sudo cnpm install hexo-cli -g #安装hexo
hexo init blog #新建博客，Hexo目录下会生产blog文件夹
cd blog
sudo cnpm install 
hexo g #生成、编译
hexo s #本地预览 
```
这时本地搭建已经完成，可以在本机预览自己的博客了

常用的hexo命令：

``` zsh
hexo n  "name" #新建文章
hexo n page "file" #新建文件夹
hexo clean #清理缓存
hexo d #部署
```
# 四、部署Hexo至Git
## 注册Git
进入[GitHub][1]注册账号后新建一个仓库
![enter description here][2]

## 配置git公钥相关

``` zsh
ssh-keygen -C '你的邮箱' -t rsa # 一路回车后会在用户目录～/.ssh/下建立相应的密钥文件
```
生成成功后找到 ～/.ssh/目录下的id_rsa.pub文件把内容添加到github账户的profile里，选择SSH KEYS 选项，然后Add SSH Key中。上传成功后，就可以使用下面这条命令。

``` zsh
ssh -v git@github.com # 测试连接是否畅通，首次连接会要求你输入邮箱及密码
```

第一次使用必须要上传一个文件
## 设置Hexo部署
在blog目录中找到名为_config.yml的配置文件修改deploy的相关信息

``` `stylus`
deploy:
  type: git
  repo: 你的ssh克隆地址
  branch: master
```
![enter description here][3]
修改完成后在blog目录下输入以下命令

``` `zsh`
sudo cnpm install hexo-deployer-git --save #安装hexo-deployer-git插件
hexo clean #清理缓存
hexo g #生成文件
hexo d #部署
```


# 五、Hexo设置主题
 


  [1]: http://github.com
  [2]: http://owd8lsn77.bkt.clouddn.com//images/1505631092291.jpg
  [3]: owd8lsn77.bkt.clouddn.com/blog/Hexo+GitHub%20Pages%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E7%9A%84%E4%B8%80%E4%BA%9B%E5%9D%91/1505667297281.jpg