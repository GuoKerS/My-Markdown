---
grammar_cjkruby: true
tags: Hexo
date: 2017-09-24 19:48
status: public
title: Hexo+GitHub Pages搭建个人博客的一些坑
---

----------
#一、前言#
由于之前使用的都是免费博客，一段时间又不经常更新导致博客已失效。考虑到能够折腾的种种因素，最终跟风的选择了Hexo来搭建博客，共耗时2天。写下此文的目的是为了记录下我搭建过程中解决的一些坑，给需要的同学做个参考。


#二、准备工作#
先说下搭建Hexo的完整流程：
1.环境准备
2.安装Node.js、Git、Npm、Hexo
3.本地调试、预览Hexo、更换主题
4.部署至Github Pages

本机环境：Ubuntu 
#三、系统环境配置#

##1. 安装Git##

``` zsh?linenums
sudo apt-get install git #安装github
git --version #显示git版本
```
## 2. 安装Node.js##

``` zsh
sudo apt-get install nodejs #安装node.js
nodejs -v #显示版本信息
```

## 3. 安装Npm（Cnpm）##

``` zsh
sudo apt-get install npm #安装.......
npm -v #显示........
#由于node不是最新的，node有个模块叫n，是专门用来管理node.js的版本。因此我们安装n模块，然后升级node.js到最新稳定版，否则后导致后续的cnpm安装不成功
sudo npm install -g n  #安装n模块
sudo n stable #升级node.js
```
由于npm在国内的下载速度极慢（下载Hexo我楞是等待了1个多小时！），在查阅资料后我得知使用淘宝分流的npm安装模块会以肉眼可见的速度在进行着！！，因此后续有关npm的命名都将有cnpm代替。

``` zsh
sudo npm install cnpm -g --registry=https://registry.npm.taobao.org #安装cnpm
```

## 4. 安装Hexo##
 
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

![enter description here][1]

常用的hexo命令：

``` zsh
hexo n  "name" #新建文章
hexo n page "file" #新建文件夹
hexo clean #清理缓存
hexo d #部署
```
## 5.更换主题##
可以参照知乎上的一篇文章
- [有哪些好看的hexo主题-知乎](https://www.zhihu.com/question/24422335 "有哪些好看的hexo主题-知乎")
在这儿我使用的是
-[next](https://github.com/iissnan/hexo-theme-next "next")
在blog目录下输入
``` zsh
sudo git clone https://github.com/iissnan/hexo-theme-next.git theme/next
```
下载完成后修改blog目录下的_config.yml文件，推荐使用vim
``` zsh
sudo apt-get install vim
vim _config.yml
```
找到theme:landscape 在75行左右将其修改为theme:next

``` zsh
hexo g #生成、编译
hexo s #预览下更换主题后的博客
```

![enter description here][2]



#四、部署Hexo至Git#
进入[GitHub][3]注册账号后新建一个仓库
![enter description here][4]

##生成SSH Key 
```zsh
ssh-keygen -t rsa -C "邮件地址@youremail.com" #一路回车
``` 
##添加SSH Key到GitHub
```zsh
cd ~/.ssh #进入保存ssh密钥的目录
```
找到 id_rsa.pub文件复制文件内容，登陆github 点击右上角的 Settings--->SSH Public keys ---> New SSH key ---> 粘贴key ---> Add SSH key

![enter description here][5]
##测试连接
```zsh
ssh -T git@GitHub.com #不要修改git@GitHub.com
```
![enter description here][6]
yes 回车

![enter description here][7]
成功
##首次上传文件至github
点击右上角 ---> Your profile --->你新建的仓库(blog2) 
在终端输入以下命令
```zsh
git config --global user.email "你的邮箱"
git config --global user.name "你的名字"
echo "# blog2" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:GuoKerS/blog2.git #改成你的
git push -u origin master
```
##通过hexo d部署至github
打开blog目录下的_config.yml 
```
deploy:
    type: git
    repository: git@github.com:GuoKerS/blog2.git ##改成你的
    branch: master
```
保存,在blog目录下输入以下命令
```zsh
sudo cnpm install hexo-deployer-git --save #安装所需插件
hexo clean
hexo g
hexo d
```
然后找到 setting ---> GitHub Pages

[enter description here][8]


![enter description here][9]
修改成如上图后点击保存（之后绑定域名也将会在这儿设置）
部署完成后访问 https://你的id.github.io/blog2 即可

#绑定域名
添加解析

![enter description here][10]
添加完成后 进入github 点击blog2 找到 setting ---> GitHub Pages
在Custom domain 出输入你要绑定域名

![enter description here][11]
然后回到终端，我们需要创建CNAME文件才能使得域名成功解析，输入以下命令
```zsh
echo "你的域名" >> CNAME
git init
git add CNAME 
git commit -m "first commit"
git push -u origin master
```
上传完成，至此你的hexo博客已经初步搭建完成并运行与互联网上了，后续有机会的话将会说一说，hexo的美化，关于如何书写文章，请参照markdown以及baidu


  [1]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477348313.jpg
  [2]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477372512.jpg
  [3]: http://github.com
  [4]: http://owd8lsn77.bkt.clouddn.com//images/1505631092291.jpg
  [5]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477395106.jpg
  [6]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477411780.jpg
  [7]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477428028.jpg
  [8]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477450541.jpg
  [9]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477460733.jpg
  [10]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477474068.jpg
  [11]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1507477487064.jpg