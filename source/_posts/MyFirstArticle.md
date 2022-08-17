---
title: 对于博客还没搭好就打算写搭博客教程这件事
date: 2021-04-05 23:25:44
categories:           # 文章分类目录, 多个分类使用[a,b,c]这种格式
tags:                 # 文章标签
---


{% blockquote 本人,引言 %}
趁着博客刚搭建还没几小时的热乎劲，把我脑袋里的流程先记一下，
图片（暂无） 排版（小改） 跳转链接（暂无）
需求工具 node.js git hexo github
{% endblockquote %}
<!--more-->
<!--more标签以下的内容要点击“阅读全文”才能看见-->

# 安装Node.js
node.js下载https://nodejs.org/en/download/  
过程中大部分默认，网上教程有对过程各部分含义的解释

/--------------------图先欠着-----------------/

安装后在cmd控制台输入path查看环境变量是否成功配置
``` bash
node --version  //查看node.js版本
npm -v          //查看npm版本
```
# 安装Git
git下载https://git-scm.com/download/win    
过程中也是大部分默认，网上教程有对过程各部分含义的解释

/--------------------图先欠着-----------------/

安装后在cmd控制台输入git --version查看版本
# 安装Hexo
接下来安装hexo  
安装命令
```bash
npm install -g hexo-cli
```
Windows下可能会报两个warning
``` bash
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@~2.3.1 (node_modules\hexo-cli\node_modules\chokidar\node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
```
因为fsevents在Windows下是可选的依赖，不安装也没事，所以直接忽略就行

接下来找个路径新建一个文件夹作为你存放博客的目录，可以手动，也可以在控制台
```bash
cd /	#切换至根目录下 
mkdir blog  #创建目录，一会要装的东西都放在这个目录下，出错也别慌，把这个目录干掉重来，几分钟后还是一条好汉~ 
cd blog #进入blog目录
```

在blog目录下  在控制台输入以下指令
```bash
hexo init   //初始化一个博客，成功控制台会显示INFO  Start blogging with Hexo!
hexo generate/hexo g    //生成静态文件，目录下会多一个public文件夹
hexo server/hexo s      //等价于 hexo server ，hexo 会监视文件变动并自动更新，除修改站点配置文件外，无须重启服务器，直接刷新网页即可生效。
```
当控制台显示以下代码的时候
```bash
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```
在网页输入http://localhost:4000就可以查看默认页面（图）
在控制台按Ctrl+C断开服务
以上为本地部署
# 部署Github
接下来创建github page      
codeing和码云类似
GitHub注册，用户名，邮箱，密码，
new Repository
这个名字的格式必须为{user_name}.github.io, 其中{user_name}必须与你的用户名一样, 这是github pages的特殊命名规范
不然之后用这个域名打开会出现404 There isn't a GitHub Pages site here的问题


# 配置Git
首先在本地创建ssh key；
``` bash
$ ssh-keygen -t rsa -C “your_email@youremail.com”
```
后面的your_email@youremail.com改为你在github上注册的邮箱，之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在C:\Users\当前用户下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key。
回到github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴在你电脑上生成的key。

为了验证是否成功，在git bash下输入：
``` bash
$ ssh -T git@github.com
```
如果是第一次的会提示是否continue，输入yes就会看到：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。


还需要设置username和email，因为github每次commit都会记录他们。
``` bash
$ git config —global user.name “your name”
$ git config —global user.email “your_email@youremail.com”
```
安装Git部署插件
```bash
npm install hexo-deployer-git --save/npm install --save hexo-deployer-git
```
同样可能会报两个warning
```bash
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@2.3.2 (node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@2.3.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
```

打开站点配置文件, 拉到底部, 修改部署配置:
```bash
Deployment
 Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo:
    github: git@github.com:masteranthoneyd/masteranthoneyd.github.io.git,master
    coding: git@git.coding.net:ookamiantd/ookamiantd.git,master
```

 最后控制台 hexo d就可以了

 中间我出现的遇到的一些问题和比较浪费时间的点
1.git的下载比较慢，花了点时间
2.node.js和git安装的比较犹豫，安装过程中每个选项都仔细去看了，然后安装完就忘了，
3.npm install -g hexo-cli过程出现的两个warning去查了一下
4.$ git config —global user.name “your name”
  $ git config —global user.email “your_email@youremail.com”
  以上两个没设置，导致hexo d一直失败
5.Repository设置的名称里面和我的用户名有一个字母的差别一直没发现，导致用GitHub域名打开的时候一直404

最后是我搭建时的几个参考文章
https://yangbingdong.com/2017/build-blog-hexo-base/
https://www.jianshu.com/p/f499ad02ab65
https://blog.csdn.net/CoolSkill/article/details/107137993
https://blog.csdn.net/weixin_39345384/article/details/80095883
https://anne416wu.github.io/posts/2727/


