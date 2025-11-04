# 极空间无公网IP搭建Cloudflared免费隧道内网穿透，部署docker教程_NAS存储_什么值得买
2023-01-12 19:51:06 24点赞 255收藏 27评论

今天发一个部署Cloudflared教程，内网穿透免费设置，用域名直接访问docker容器，[dd](https://pinpai.smzdm.com/102135/)nsto经常需要验证比较烦，另外穿透后的域名会比较长，比较难记住，Cloudflared内网穿透后可以使用自己好记的域名，还可以做多个二级域名访问，不限制数量

部署步骤
----

1，注册域名
------

2，注册Cloudflared账号
-----------------

3，部署docker
----------

4，配置tunnels域名穿透
---------------

### 注册域名

以阿里云为例，去注册一个域名，现在有很多个性化的后缀名，价格很便宜注册一个域名也就几块钱，注册好了以后需要实名认证，如果只是单纯的做公网穿透使用是不用做备案的  

[![](https://qnam.smzdm.com/202301/11/63beb8a23f9539722.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_2/)

实名认证的过程大家自行操作，很方便，按照指引一步一步实名，注意必须完成实名认证，不然使用不了

### 注册Cloudflared账号

我们登录Cloudflared注册一个账号并登录，官网链接：https://www.cloudflare-cn.com/

[![](https://qnam.smzdm.com/202301/11/63beb9b6648bc8851.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_3/)邮箱注册

站点添加刚才注册的网站  

[![](https://qnam.smzdm.com/202301/11/63beb9f9ab11d1561.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_4/)

选择Free 继续下一步  

[![](https://qnam.smzdm.com/202301/11/63beba56b4f138073.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_5/)

[![](https://am.zdmimg.com/202301/11/63bebaec851233117.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_6/)继续下一步

然后来到这一页面，分别复制保存好这两个Cloudflare

[![](https://qnam.smzdm.com/202301/11/63bebb1d0116e6096.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_7/)

回到刚才阿里云域名管理，左侧域名列表

点击域名进入

[![](https://qnam.smzdm.com/202301/11/63bebbf6cd03f4519.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_8/)

修改dns，把刚才复制的2个Cloudflare ，填到这里，确定保存

[![](https://qnam.smzdm.com/202301/11/63bebbfa3f8756015.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_9/)

然后回到Cloudflare，点完成

[![](https://qnam.smzdm.com/202301/11/63bebc7208f4d3270.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_10/)

这里按操作流程点，使用保存  

[![](https://qnam.smzdm.com/202301/11/63bebc9ee1bf91963.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_11/)

回到首页点Access

[![](https://qnam.smzdm.com/202301/11/63bebcef86f4c7866.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_12/)

启动Zero Trust，进入这个网站会有点慢，不要着急  

[![](https://qnam.smzdm.com/202301/11/63bebcf434f205261.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_13/)

点击Access下的Tunnels 点Create a tunnel

[![](https://qnam.smzdm.com/202301/11/63bec0f3bb3364148.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_14/)

选择Free 点Select plan

这里有2步是要选择ferr免费版本和0元购买的，因为我购买过所以没有这个截图，有的人会有预扣款，然后退款，  

然后接下来填一个你喜欢的名字

[![](https://qnam.smzdm.com/202301/11/63bebff61ea9c8423.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_15/)

选择Docker，复制下面这串代码，这串代码里实际上有用的只有我红框框里打码的那串Token

编辑保存好这串Token，备用，然后点下方的Next

[![](https://qnam.smzdm.com/202301/11/63bec09e6d6b13953.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_16/)

来到Public Hostname Page

Subdomain填 www  

Domain(Required)选择 刚刚注册的域名

Service(Required)选择 HTTP ://后面填 自己Nas的IP：自己想要映射的端口（如我想要映射刚做的Heimdall网页，端口是9010）

然后点Save hostname

[![](https://qnam.smzdm.com/202301/11/63bec40af1f056813.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_17/)

### 部署docker

来到极空间docker仓库，搜cloudflare/cloudflared点击下载

[![](https://qnam.smzdm.com/202301/11/63bec4bc6a9181322.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_18/)

双击打开以后来到文件夹路径，在Docker文件夹里新建一个Cloudflared文件夹

路径选择Cloudflared文件夹

装载路径填 /etc/cloudflared

[![](https://qnam.smzdm.com/202301/11/63bec50ed552d4989.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_19/)

[![](https://qnam.smzdm.com/202301/11/63bec5312fbb27630.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_20/)网络改成host

命令这里修改，这一步很关键，这里修改错了就会不断重启，查了很教程才发现

'tunnel' '--no-autoupdate' 'run' '--token' '这里替换刚刚复制备用的Token'

前面在Zero Trust复制的token替换上面的就行

启用容器，等几分钟配置  

[![](https://qnam.smzdm.com/202301/11/63bec5601d3df9333.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_21/)

在浏览器输入我们注册好的域名，即可成功登录我们隧道穿透的端口了

[![](https://am.zdmimg.com/202301/12/63bfc4e67ff228292.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_22/)

[手机](https://www.smzdm.com/fenlei/zhinengshouji/)端访问，建议手机可以添加快捷方式到桌面比较方便使用

[![](https://qnam.smzdm.com/202301/12/63bfc4fc061179889.jpg_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_23/)

如果我们还有很多端口怎么配置，很简单  

左侧栏tunnels可以看到我们刚才配置的域名，点Configure

[![](https://qnam.smzdm.com/202301/11/63bec69de316a7332.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_24/)

来到Public Hostname Page

点Add a public hostname

[![](https://qnam.smzdm.com/202301/11/63bec741e14dd1209.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_25/)

Subdomain填和我们第一条域名不一样的， 比如填wwc

Domain(Required)选择 刚刚注册的域名

Service(Required)选择 HTTP ://后面填 自己Nas的IP：自己想要映射的端口

[![](https://qnam.smzdm.com/202301/11/63bec769dd28c3223.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_26/)

[![](https://qnam.smzdm.com/202301/11/63bec8d79c9867200.png_e1080.jpg)
](https://post.smzdm.com/p/ao9vdw8n/pic_27/)

理论上可以配置非常多的端口二级子域名，如果这么算的话还是比ddnsto好用，毕竟只用付一个域名的费用，可以无限穿透子域名，有比较多端口的小伙伴还是不错的选择，内网穿透有很多教程和工具，目前看Cloudflared隧道是最好使用的了。

我的操作是把穿透的子域名都加到Heimdall里，这样只要有一个主域名就可以访问所有其他端口了

没有看到Heimdall部署可以看下面的教程

![](https://qna.smzdm.com/202212/25/63a86fe341b467128.png_a200.jpg)

docker端口是不是不好记， 极空间部署Heimdall实现个人导航，美观简洁

![](https://avatarimg.smzdm.com/default/6734006921/6395bf303c88a2076-small.jpg)

没事随便写写

22-12-26

如果端口不多的话用ddnsto比较简单省事，就是在不同设备上需要验证比较麻烦

下面是ddnsto的教程，比较简单容易配置，一年套餐26元也不贵，可以加12条穿透域名，如果数量不多的话可以使用，省得折腾  

![](https://qna.smzdm.com/202212/08/6391e43d6db4d6030.jpg_a200.jpg)

极空间NAS外网访问DDNSTO篇,超级简单配置，访问docker轻松简单，小白必备

![](https://avatarimg.smzdm.com/default/6734006921/6395bf303c88a2076-small.jpg)

没事随便写写

22-12-08

![](https://qna.smzdm.com/202301/11/63becb1ba47819500.jpg_a200.jpg)

极空间Z4-8G版四核4盘位NAS网络存储服务器（无内置硬盘）

![](https://a.zdmimg.com/202301/11/63becb2db1e4e724.jpg_a200.jpg)

极空间 私有云 Z2S 四核 2盘位NAS家庭个人云网盘 私有极空间 网络存储服务器【无内置硬盘】钛金灰色

![](https://qna.smzdm.com/202301/11/63becb4cdb04f8244.jpg_a200.jpg)

贝锐蒲公英路由器X1 旁路组网盒子nas自建私有云网盘云盘USB网络存储局域异地组网家用远程访问无需公网IP 蒲公英X1

作者声明本文无利益相关，欢迎值友理性交流，和谐讨论～

![](https://res.smzdm.com/pc/pc_shequ/dist/img/the-end.png)

![](https://qny.smzdm.com/202207/06/62c53ac5ee9b53455.jpg_a200.jpg)

![](https://qna.smzdm.com/202301/11/63becb4cdb04f8244.jpg_a200.jpg)

贝锐蒲公英路由器X1 旁路组网盒子nas自建私有云网盘云盘USB网络存储局域异地组网家用远程访问无需公网IP 蒲公英X1

![](https://qna.smzdm.com/202301/11/63becb1ba47819500.jpg_a200.jpg)

极空间Z4-8G版四核4盘位NAS网络存储服务器（无内置硬盘）