---
title: 利用hexo和github建立个人博客
date: 2018-08-13 20:18:11
tags: 
  - hexo
  - github
categories:
  - hexo
---

## 利用github和hexo建立个人博客

### 1. 依赖

- GitHub账号
- 本地Git安装
- 本地Node.js，Hexo安装

### 2. 博客搭建

#### hexo安装

<!--more-->

由于之前已经在本地安装好了git和Node.js，所以只需要安装Hexo即可

```
$ npm install -g hexo-cli
```

等待安装成功。

#### 在本地创建博客目录

```
$ hexo init blog
```

Hexo安装成功之后，即可创建博客。选择一个文件夹，打开bash，输入上面的命令就可在当前文件夹下新建名为blog的博客文件夹，并初始化。

现在可以执行下述命令：

```
$ hexo g
$ hexo s
```

然后在浏览器中输入地址`localhost:4000`即可查看博客 

 {% asset_img /1.png 初始化博客 %}  

![](./1.png)

#### 在github中建立新仓库

在github建立新仓库 [tmyvvit.github.io](https://github.com/tmyVvit/tmyVvit.github.io.git) 。打开博客根目录下的配置文件`_config.yml`，在末尾添加以下代码

```yml
deploy:
  type: git
  repo: https://github.com/tmyVvit/tmyVvit.github.io.git
  branch: master
```

然后重新推送部署

```
$ hexo clean
$ hexo g
$ hexo d
```

，就可以在浏览框中输入地址`tmyvvit.github.io`来访问博客。



#### 绑定域名

我在阿里云买了一个域名`tmyxyz.xyz`， 现在要将这个域名绑定在Github提供的域名上面。进入阿里云域名管理控制台，找到个性化域名并设置解析 

 {% asset_img /域名解析.png 域名解析 %}

![]( ./域名解析.png)

下一步在Github上进入刚才新建的仓库，点击Setting，设置Custom domain为`tmyxyz.xyz`

然后在本地博客`blog/source`目录下创建一个名为`CNAME`的文件，内容为个性化域名。然后重新推送部署就可以根据个性化域名进入我的博客。



### 3 hexo基本指令

#### init

```
$ hexo init [folder]
```

新建一个网站，没有设置`folder`则在当前文件夹建立网站

#### new

```
$ hexo new [layout] <title>
```

新建文章，`layout` 默认为配置文件`_config.yml`中的`default_layout`参数

| 布局  | 路径           |
| ----- | -------------- |
| post  | source/_posts  |
| page  | source         |
| draft | source/_drafts |

#### generate

```
$ hexo [-d][-w] generate
```

生成静态文件，选项`-d,--deploy`文件成成后立即部署网站，选项`-w,--watch`监视文件变动，命令可以简写为

```
$ hexo g
```

#### publish

```
$ hexo publish [layout] <filename>
```

发表草稿，将草稿转为post。

#### server

```
$ hexo server
```

启动服务器。默认`http://localhost:4000`

| 选项         | 描述                           |
| ------------ | ------------------------------ |
| -p, --port   | 重设端口                       |
| -s, --static | 只使用静态文件                 |
| -l, --log    | 启动日记记录，使用覆盖记录格式 |

#### deploy

```
$ hexo [-g, --generate] deploy
```

部署网站，选项`-g, --generate`部署前预先生成静态文件

#### clean

```
$ hexo clean
```

清除缓存文件（`db.json`）和已经生成的静态文件（`public`）。

在某些情况下（尤其是更换主题），如果对站点的更改不生效，则可以运行该指令。