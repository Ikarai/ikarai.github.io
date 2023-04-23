---
title: Vercel+Hithub免费搭建Hexo博客

date: 2023.04.20 17:48

tags: 博客

description: Vercel+Hithub免费搭建Hexo博客

---

# 安装nodejs和git

nodejs[下载地址](https://nodejs.org/zh-cn/download) 建议安装长期维护版中的最新版本

git [下载地址](https://gitforwindows.org/)

# 安装Hexo

首先，在文件夹空白处或是桌面右击鼠标，选择 *Git Bash Here* 打开终端

![git](https://missuo.ru/file/f5a8e830b9ab34b17099c.png)

<!--more-->

执行  `npm config set registry https://registry.npm.taobao.org` 命令切换至国内源

执行 `npm install hexo-cli -g`  命令安装hexo

执行 `hexo init blog` 命令新建blog文件夹并下载一些文件

如果出现*Start blogging with Hexo!* 信息则初始化完成

执行 `cd blog` 进入blog文件夹

执行 `npm install` 安装依赖

执行 `hexo s` 本地运行hexo，出现 *Hexo is running at http://localhost:4000* 则运行成功，访问这个网址就可以看到网站现在的初始样子了。 *Ctrl +C* 停止运行

# 更改基本信息及主题

## 更改配置文件

用记事本或者任何编辑器打开blog文件夹内的 *_config.yml* 文件

自行更改 *site* 栏中的信息

![config](https://missuo.ru/file/258c1466376507a572fca.png)

**请注意！冒号和值之间务必留一个空格，这是这类文件的格式要求，不遵守可能会报错**

## 更改主题

[官方网站]([Themes | Hexo](https://hexo.io/themes/)) 中不少优秀的主题可供选择

这里就以 [hexo-theme-yilia-plus主题](https://github.com/JoeyBling/hexo-theme-yilia-plus) 做演示。作者的[博客](https://joeybling.github.io/) 

这个主题是根据[hexo-theme-yilia](https://github.com/litten/hexo-theme-yilia)主题做了一些优化和改动，个人还是蛮喜欢这个主题的，~~但是作者好像已经失联好久了~~

下载并把主题放入themes文件夹中或`cd themes` 后 `git clone --depth=1 https://github.com/JoeyBling/hexo-theme-yilia-plus.git ./yilia-plus` 下载主题

然后修改 *_config.yml* 文件中的 *theme* 值为 *yilia-plus*

完成后样子 ![yilia](https://missuo.ru/file/9adfde5a425198eb54839.png)

你可以根据作者提供的[demo](https://github.com/JoeyBling/yilia-plus-demo) 对 *yilia-plus* 文件夹中的配置文件 *_config.yml* 进行修改

 你可以随时执行`hexo s` 后查看修改后的样子

# 部署到Github

打开[github](https://github.com/) ，如果你是第一次使用，点击右上角 *Sign up* 注册验证邮箱并登录

点击右上角头像，选择 *your profile*

![github](https://missuo.ru/file/8e340195cc3e297b34dd7.png)

这里会显示你的所i有仓库， *Repositories* — *New* 新建一个仓库

![github](https://missuo.ru/file/1774dc5f5e054b2ff57c9.png)

输入仓库名称，下面一定要选择 *Public* ，将仓库公开

![github](https://missuo.ru/file/5e22b1bed59b54e764de1.png)

**下面介绍两种部署方法** 

## 1.使用git命令提交(不建议新手使用)

执行 `ssh-keygen -t rsa -C "邮箱"` 生成密钥，默认在 *C:\Users\你的用户名\ .ssh* 目录下

进入设置

![github](https://missuo.ru/file/8af719c8f2db18360b51e.png)

*SSH and GPG keys*

![github](https://missuo.ru/file/f5c41998c36e458e7f169.png)

*New SSH key* ，*Title* 名称随意，将 *id_rsa.pub* 文件中的内容复制到 *key* 中

![github](https://missuo.ru/file/d636ee83427fa01b85328.png)

执行以下命令

```
git config --global user.name "你的github用户名"
git config --global user.email "你的github邮箱"
ssh -T git@github.com
```

如果这里显示的是你的用户名，那么就设置成功了，现在本地的git就和github连接成功

![github](https://missuo.ru/file/be72dd9999774c4a56320.png)

接下来我们要将本地的文件部署到gith仓库中

进入刚才创建好的仓库，点击 *code* ，复制这个链接

![github](https://missuo.ru/file/b668baf5fddc9a48dbeb2.png)

打开博客根目录的 *_config.yml* 文件，找到最后一行的 *deploy* ，修改为

![yml](https://missuo.ru/file/d4af2d5c1902d14f94bf4.png)

依次执行以下命令

```
npm install hexo-deployer-git --save
hexo c
hexo g
hexo d
```

提交成功

## 2.使用可视化git工具提交(推荐新手使用，简单易操作)

这类工具有很多，这里使用sourcetree

> SourceTree 是 Windows 和Mac OS X 下免费的 Git 和 Hg 客户端管理工具，同时也是Mn版本控制系统工具。支持创建、克隆、提交、push、pull 和合并等操作。

可以去[官网](https://www.sourcetreeapp.com/) 下载，免费且支持中文

打开软件，在地址栏输入仓库地址，下方会自动生成本地路径，可自行更改

![tree](https://missuo.ru/file/9b3c313f31ab458fd82d7.png)

![tree](https://missuo.ru/file/895fd011f5058f2ddf140.png)

将Hexo博客blog文件里的内容复制到本地仓库blog文件夹内

回到sourcetree，检测到本地仓库文件变化后，软件会显示所有发生变化的文件

![tree](https://missuo.ru/file/ccb9205f8f91a0afbebb5.png)

选择 *暂存所有* 

![tree](https://missuo.ru/file/b22ffc5bb8798dc755b92.png)

暂存完成后文件会转移到上方的已暂存文件中，接下来在下方文本框中输入description后点击 *提交* 

![tree](https://missuo.ru/file/7a5f172b6d1d4d201c078.png)

再点击 *推送* ，本地仓库中的文件就会更新到云端Github仓库中了

![tree](https://missuo.ru/file/0a34687a9b1e1147b1e0a.png)

之后如果需要增删改文件也是一样的操作，先在本地进行操作，再 *暂存—提交—推送* 即可

这里只是简单介绍一下如何提交，关于软件的详细使用感兴趣的可以自行搜索学习

提交完成后进入下一步

![tree](https://missuo.ru/file/913fc2afaf9792de77acf.png)

# 连接至Vercel加速访问

首先打开[Vercel](vercel.com) ，右上角 *sign up* 输入用户名，选择使用Github登录

新建项目，选择添加Github账户

![ver](https://missuo.ru/file/8a7fea062e3d08fbbe004.png)

在弹出的窗口中选择之前建好的仓库，提交，输入密码验证

![ver](https://missuo.ru/file/33b918abdf9d6531cabba.png)

点击 *Import*

![ver](https://missuo.ru/file/0a3a6892416dbbe33ad0d.png)

可以看到Vercel会自动识别到这是个Hexo项目，在这一步你可以更改项目名称，然后点击*Deploy* 进行部署

![ver](https://missuo.ru/file/1cc0cc552a6e1e5974ff7.png)

部署成功

![ver](https://missuo.ru/file/6a908a05618c5307e3d71.png)

这样就部署成功了，现在你可以尝试用Vercel给的网址访问博客了

但是，vercel.app域名在国内遭到污染，所以可能出现访问速度慢或无法访问的情况

建议通过[namesilo](https://www.namesilo.com/?rid=d27fa32do) 或 [硅云](https://www.vpsor.cn/product/domain-buy) 购买一个域名。在本文发布时硅云还有一个活动，新用户可以免费注册一个域名，第一年免费(但是需要备案)

在项目中点击 *view Domains*

![ver](https://missuo.ru/file/deca158e44f9edf44dc0f.png)

输入域名，*add* ,按照要求添加解析记录即可

![ver](https://missuo.ru/file/b4d1ffb07b6d308afa3a5.png)

---

flag：关于域名和备案以后大概会单独写一篇文章吧
