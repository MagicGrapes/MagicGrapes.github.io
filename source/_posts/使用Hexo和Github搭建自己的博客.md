---
title: 使用Hexo和Github搭建自己的博客
date: 2020-05-07 19:15:56
tags: 
	- "Hexo"
	- "Git"	
categories: "博客搭建"
---

## Github
- 获取域名

- 建立个人仓库，两个分支hexo分支存放Hexo的环境配置文件，master分支存放静态文件

- 安装git - 安装node.js - 安装Hexo

  使用npm命令安装Hexo，输入：

  ```bash
  npm install -g hexo-cli 
  ```

  安装完成后，在指定文件夹右键Gitbash初始化我们的博客，输入：

  ```bash
  hexo init blog
  ```

  为了检测我们的网站雏形，分别按顺序输入以下三条命令：

  ```bash
  hexo new "my_first_post"
  
  hexo g
  
  hexo s
  ```

  这些命令在后面作介绍，完成后，打开浏览器输入地址：

  localhost:4000 可以看到自己的博客

- **部署**

  首先，需要了解一下hexo项目的目录结构，以及各文件夹用来存放哪些文件（已经了解的可以跳过）。下面是本地hexo项目的目录结构。文件夹没有展开，为了和文件区别，我在文件夹名后加了一个`/`用以和文件名区分开来。

  ```
  HEXO
  ├──.deploy_git/
  ├──node_modules/
  ├──public/
  ├──scaffolds/
  ├──source/
  ├──themes/
  ├──_config.yml
  ├──.gitignore
  ├──db.json
  ├──debug.log
  └──package.json复制代码
  ```

  接下来要做的就是就是是发布网站。Hexo的目录里的_config.yml文件称为**站点**配置文件，根目录里的themes文件夹，里面也有个_config.yml文件，这个称为**主题**配置文件。

  首先打开站点的配置文件_config.yml，翻到最后修改部署方式为：

  deploy:
  type: git
  repo: 这里填入你之前在GitHub上创建仓库的完整路径，记得加上.git 前面https://改成git@，github.com后面斜杠改为冒号，否则即便配置了SSH还是要输入用户名和密码

  举个栗子：**git@github.com:**xiaoming/xiaoming.github.io**.git**

  branch: master（静态文件的分支）

  保存站点配置文件, 让hexo知道你要把blog部署在哪个位置

  最后安装Git部署插件，输入命令：

  ```basemake
  npm install hexo-deployer-git --save
  ```

  依次执行git add . 、git commit -m "..."、git push origin hexo 提交网站相关的文件到hexo分支

  ```bash
  git add . 
  git commit -m "..."
  git push origin hexo 
  ```

  之后，我们分别输入三条命令，部署网站到主分支：

  ```bash
  hexo clean 
  hexo generate 
  hexo deploy
  ```

  后两条可以并为：

  ```bash
  hexo g -d
  ```

- 关于日常的改动流程

  在本地对博客进行修改（添加新博文、修改样式等等）后，通过下面的流程进行管理。

  1. 依次执行git add .、git commit -m "..."、git push origin hexo指令将改动推送到GitHub（此时当前分支应为hexo）；
  2.  然后才执行hexo g -d发布网站到master分支上。

  虽然两个过程顺序调转一般不会有问题，不过逻辑上这样的顺序是绝对没问题的（例如突然死机要重装了，悲催....的情况，调转顺序就有问题了）。

- 本地资料丢失后的流程

  当重装电脑之后，或者想在其他电脑上修改博客，可以使用下列步骤：

  1. 使用git clone git@github.com:CrazyMilk/CrazyMilk.github.io.git拷贝仓库（默认分支为hexo）；
  2. 在本地新拷贝的http://Username.github.io文件夹下通过Git bash依次执行下列指令：npm install hexo、npm install、npm install hexo-deployer-git（记得，不需要hexo init这条指令）。

  [详见知乎高赞答案使用hexo，如果换了电脑怎么更新博客？](https://www.zhihu.com/question/21193762/answer/79109280)

- 域名解析要ping一下你的页面地址,然后加到域名解析中，同时在主分支中新建一个CNAME文件，里面写上你的**域名**（不加www等），由于每次部署会清除这个文件，所以把它放到你Hexo初始化文件夹下的source文件夹里，这样每次部署都会上传

## Hexo使用

创建新的博客

``` bash
$ hexo new "My New Post"
```

启动服务器

``` bash
$ hexo server
```

生成静态文件

``` bash
$ hexo generate
```

部署站点

``` bash
$ hexo deploy
```

详见:  [Writing](https://hexo.io/docs/writing.html)  [Server](https://hexo.io/docs/server.html)  [Generating](https://hexo.io/docs/generating.html) [Deployment](https://hexo.io/docs/one-command-deployment.html)
