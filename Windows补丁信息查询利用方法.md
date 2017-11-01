---
title: Windows补丁信息查询利用方法
tags: 提权
grammar_cjkRuby: true
---

t00ls上看到的回复，make

# 获取补丁信息：

wmic qfe get Caption,Description,HotFixID,InstalledOn

 ![enter description here][1]

也可以修改命令查看特定漏洞补丁信息：

``` zsh
wmic qfe get Caption,Description,HotFixID,InstalledOn | findstr /C:"KB3136041" /C:"KB4018483"
```


也可以用脚本啊：

# Metasploit：
post/windows/gather/

 ![enter description here][2]

Windows Exploit Suggester：https://github.com/GDSSecurity/Windows-Exploit-Suggester

 ![enter description here][3]

Sherlock：https://github.com/rasta-mouse/Sherlock

![enter description here][4]


  [1]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1509557950942.jpg
  [2]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1509557956538.jpg
  [3]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1509557964339.jpg
  [4]: http://owd8lsn77.bkt.clouddn.com/%E5%B0%8F%E4%B9%A6%E5%8C%A0/1509557969450.jpg