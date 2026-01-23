# 洛雪音乐助手同步服务的搭建_lxmusic github-CSDN博客
![](https://i-blog.csdnimg.cn/blog_migrate/619bd635da0f672bb1f44884f1890474.png#pic_center)

> 本文软件是应网友 `不要告别2023` 要求折腾的

**什么是 LX Music** ？

> 洛雪音乐助手是一款个人开发第三方的音乐搜索、下载、播放软件，功能强大、音乐齐全、操作简单，支持导入其他主流音乐播放器的歌单、支持多设备同步功能，可在 `Windows`、`MacOS`、`Linux`、`Android` 平台运行。

**什么是 LX Music Sync Server？**

> 洛雪音乐数据同步服务端，目前用于收藏列表数据同步，类似原来 `PC` 端的数据同步服务，只不过它现在是一个独立版的服务，可以将其部署到服务器上使用。

老苏觉得用独立版数据同步服务比原来 `PC` 端的数据同步服务有优势，一方面支持多用户，另一方面比较适合服务器上部署，从而实现随时随地可访问

构建镜像
----

> 如果你不想自己构建，可以跳过，直接阅读下一章节

官方提供了 `Dockerfile`，只是没找到官方的镜像，所以需要自己编一下

构建镜像和容器运行的基本命令如下👇

```
 `git clone https://github.com/lyswhut/lx-music-sync-server.git

git clone https://ghproxy.com/github.com/lyswhut/lx-music-sync-server.git
 

cd lx-music-sync-server  
  

docker build -t wbsu2003/lx-music-sync-server:v1 .  
  

docker run -d \
   --name lx-music-sync-server \
   -p 9527:9527 \
   wbsu2003/lx-music-sync-server:v1` 

![](https://csdnimg.cn/release/blogv2/dist/pc/img/runCode/icon-arrowwhite.png)

*   1
*   2
*   3
*   4
*   5
*   6
*   7
*   8
*   9
*   10
*   11
*   12
*   13
*   14
*   15
*   16
*   17


```

安装
--

在[群晖](https://so.csdn.net/so/search?q=%E7%BE%A4%E6%99%96&spm=1001.2101.3001.7020)上以 Docker 方式安装。

在注册表中搜索 `wbsu2003/lx-music-sync-server` ，版本选择 `latest`。

![](https://i-blog.csdnimg.cn/blog_migrate/ebc956d967c1f596c4f9366fce7b9354.png#pic_center)

### 卷

在 `docker` 文件夹中，创建一个新文件夹 `lx-music-sync-server`，并在其中建两个子文件夹，分别是 `data` 和 `logs`

| 文件夹 | 装载路径 | 说明 |
| --- | --- | --- |
| `docker/lx-music-sync-server/data` | `/server/data` | 存放设置信息 |
| `docker/lx-music-sync-server/logs` | `/server/logs` | 存放日志 |

![](https://i-blog.csdnimg.cn/blog_migrate/d05b43ed322a6ae7a92b7efc7a00c096.png)

### 端口

本地端口不冲突就行，不确定的话可以用命令查一下

```
 `netstat -tunlp | grep 端口号` 

*   1
*   2


```

![](https://i-blog.csdnimg.cn/blog_migrate/f4dca049761540f51a96d84342131bea.png)

### 环境

| 可变 | 值 |
| --- | --- |
| `LX_USER_user1` | 设置用户密码为 `mypassword123` |

官方提供的可用变量挺多，除了密码，基本上可以直接用默认的，[https://github.com/lyswhut/lx-music-sync-server#可用的环境变量](https://github.com/lyswhut/lx-music-sync-server#%E5%8F%AF%E7%94%A8%E7%9A%84%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F)

![](https://i-blog.csdnimg.cn/blog_migrate/e6b068d10bf6ae791e238cdd65d0968e.png)

> 软件支持多用户设置，但是密码不能一样；

![](https://i-blog.csdnimg.cn/blog_migrate/4ccc21d00e87c676f6eb279e8ebcd0b3.png)

命令行安装
-----

如果你熟悉命令行，可能用 `docker cli` 更快捷

```
 `mkdir -p /volume2/docker/lx-music-sync-server/{data,logs}

cd /volume2/docker/lx-music-sync-server

docker run -d \
   --restart unless-stopped \
   --name lx-music-sync-server \
   -p 9527:9527 \
   -v $(pwd)/data:/server/data \
   -v $(pwd)/logs://server/logs \
   -e LX_USER_user1=mypassword123 \
   wbsu2003/lx-music-sync-server` 

![](https://csdnimg.cn/release/blogv2/dist/pc/img/runCode/icon-arrowwhite.png)

*   1
*   2
*   3
*   4
*   5
*   6
*   7
*   8
*   9
*   10
*   11
*   12
*   13
*   14
*   15


```

也可以用 `docker-compose` 安装，将下面的内容保存为 `docker-compose.yml` 文件

```
`version: '3'

services:
  syncserver:
    image: wbsu2003/lx-music-sync-server
    container_name: lx-music-sync-server
    restart: unless-stopped
    ports:
      - 9527:9527
    volumes:
      - ./data:/server/data
      - ./logs:/server/logs
    environment:  
      - LX_USER_user1=mypassword123` 

![](https://csdnimg.cn/release/blogv2/dist/pc/img/runCode/icon-arrowwhite.png)

*   1
*   2
*   3
*   4
*   5
*   6
*   7
*   8
*   9
*   10
*   11
*   12
*   13
*   14


```

然后执行下面的命令

```
 `mkdir -p /volume2/docker/lx-music-sync-server/{data,logs}

cd /volume2/docker/lx-music-sync-server

docker-compose up -d` 

![](https://csdnimg.cn/release/blogv2/dist/pc/img/runCode/icon-arrowwhite.png)

*   1
*   2
*   3
*   4
*   5
*   6
*   7
*   8
*   9
*   10


```

运行
--

### 服务端

在浏览器中输入 `http://群晖IP:9527/hello`，如果在页面上你看到 `Hello~::^-^::~v3~`，说明服务已经 `OK` 了

![](https://i-blog.csdnimg.cn/blog_migrate/0153d988040f5b9f918404d28902366c.png)

### Windows 客户端

下载地址：[https://github.com/lyswhut/lx-music-desktop/releases](https://github.com/lyswhut/lx-music-desktop/releases)

![](https://i-blog.csdnimg.cn/blog_migrate/72e38d8d810c35ca49ce1268523d9f21.png)

老苏下载的 `windows` 的 `2.2.0` 绿色版 `lx-music-desktop-v2.2.0-win_x64-green.7z`

解压运行之后，搜了 `石进`

![](https://i-blog.csdnimg.cn/blog_migrate/73b3c287ff5c34cd9bf0149e8e676a5e.png)

进入设置–> 数据同步，默认是 `服务端模式`

*   服务端模式，用于在同一局域网下，为其他设备提供同步服务
*   客户端模式，与移动端一样，可用于连接另一个处于“服务端模式”的PC端或独立版数据同步服务

![](https://i-blog.csdnimg.cn/blog_migrate/e3aebb1c88faa01f7c4b3a4455b9643b.png)

但是我们已经安装了独立版数据同步服务 `lx-music-sync-server` ，所以我们要改为 `客户端模式`

![](https://i-blog.csdnimg.cn/blog_migrate/853b5baaffc82059ba1c991956cfc42e.png)

输入服务器地址，勾选 `启用同步功能`，输入连接码就可以了

> 连接码就是我们前面设置的密码，如果你用 `mypassword123`，连接信息就会记录在 `user1` 用户目录下，如果你用 `123456`，j就会记录在 `laosu` 目录下

![](https://i-blog.csdnimg.cn/blog_migrate/5c2c0f239e61816a23e6ff64d5f40ded.png)

查看 `File Station` 中的目录

![](https://i-blog.csdnimg.cn/blog_migrate/386e01a259237cec5cb792e4f1dbd8a4.png)

### 移动端

下载地址：[https://github.com/lyswhut/lx-music-mobile/releases](https://github.com/lyswhut/lx-music-mobile/releases)

一般 `Android` 手机只要下载 `lx-music-mobile-v1.0.3-arm64-v8a.apk` 就行

![](https://i-blog.csdnimg.cn/blog_migrate/591a75fbe97ca2599a5e500b9f90fdf5.png)

填好 `服务器地址` 之后，勾选 `启用同步`

![](https://i-blog.csdnimg.cn/blog_migrate/5810f5024a197f4773e82cf3189cb56f.png)

填写连接码之后，因为桌面端已经同步过，所以要选择你的同步方式

![](https://i-blog.csdnimg.cn/blog_migrate/df2fa8aa880db2949c1f7a4082bc0da4.png#pic_center)

### 反代

用 `npm` 正常处理就可以，没有特殊设置

参考文档
----

> lyswhut/lx-music-sync-server: 运行在Node.js上的LX Music数据同步服务  
> 地址：[https://github.com/lyswhut/lx-music-sync-server](https://github.com/lyswhut/lx-music-sync-server)

> 同步功能的使用 | LX Music  
> 地址：[https://lxmusic.toside.cn/desktop/faq/sync](https://lxmusic.toside.cn/desktop/faq/sync)

> LX Music - 一个免费&开源的音乐查找工具 | LX Music  
> 地址：[https://lxmusic.toside.cn/](https://lxmusic.toside.cn/)

> lyswhut/lx-music-desktop: 一个基于 electron 的音乐软件  
> 地址：[https://github.com/lyswhut/lx-music-desktop](https://github.com/lyswhut/lx-music-desktop)