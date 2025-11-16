# (35 封私信) Immich 数据库 pg14 → pg17 升级指南 - 知乎
**背景**
------

*   • 当前 Immich 数据库版本：**PostgreSQL 14**
*   • 升级目标版本：**PostgreSQL 17**
*   • 系统环境：**[飞牛 OS](https://zhida.zhihu.com/search?content_id=263977604&content_type=Article&match_order=1&q=%E9%A3%9E%E7%89%9B+OS&zhida_source=entity)（NAS）**
*   • 升级方式：**使用 Docker 容器进行数据升级**

* * *

**升级流程概览**
----------

1.  **备份现有数据库数据**
2.  **准备 PostgreSQL 14 程序文件**
3.  **准备 PostgreSQL 17 数据目录与程序文件**
4.  **执行数据升级**
5.  **更新 Immich 镜像信息**

* * *

### **1\. 备份数据库数据**

最简单粗暴的方式：直接复制挂载的数据目录。

示例：

```text
原始数据目录: vol2/1000/immich/postgres 
备份目录:    vol2/1000/immich/backup/postgres
```

操作截图：

![](https://pic2.zhimg.com/v2-6b41a4f82e551be68f79a93f66b1fba9_1440w.jpg)

> _⚠️ 确保在复制前 Immich 容器已停止运行。_

* * *

### **2\. 准备 PostgreSQL 14 程序文件**

**步骤**

1.  1\. 停止 Immich 服务：  
    `点击 【Compose】 → 【immich】 → 【停止】`
2.  2\. 挂载一个目录到 pg14 Docker 容器 `/mnt`：  
    `点击 【容器】 → 【immich_postgres】 → 【设置】 → 【存储位置】`
3.  3\. 进入容器终端，复制程序文件：cp -rf /usr/lib/postgresql/14 /mnt/postgresql/14  
    cp -rf /usr/share/postgresql /mnt/share

截图示例：

![](https://pic3.zhimg.com/v2-c419b4ae4c9d6da9a69708245abc8ba6_1440w.jpg)

> _这一步确保 pg14 的二进制程序和共享文件备份完整。_

* * *

### **3\. 准备 PostgreSQL 17 数据目录与程序文件**

**步骤一：下载 pg17 镜像**

`镜像 URL: ghcr.io/immich-app/postgres:17-vectorchord0.4.3-pgvectors0.3.0`

操作：

`Docker → 镜像管理 → 添加镜像 → 输入 URL → 确认`

截图：

![](https://pic2.zhimg.com/v2-5ccf76bfbac64ec29c01945d7dbf9adb_1440w.jpg)

**步骤二：创建 pg17 容器**

*   • 设置环境变量：POSTGRES\_USER  
    POSTGRES\_PASSWORD  
    （需与 pg14 用户一致）
*   • 创建新的 pg17 数据目录，并挂载到容器 `/var/lib/postgresql/data`

**步骤三：验证容器启动成功**

```text
2025-10-08 14:48:05.556 UTC [34] LOG:  database system was shut down at 2025-10-08 14:44:24 UTC 
2025-10-08 14:48:05.638 UTC [1] LOG:  database system is ready to accept connections
```

> _成功显示日志即可连接。_

* * *

### **4\. 数据升级**

**步骤一：停止 pg17 容器**

`容器 → 找到 postgres17 容器 → 停止`

**步骤二：挂载 pg14 文件到 pg17 容器**

挂载目录对应关系：

```text
pg14 lib目录 → /usr/lib/postgresql/14 
pg14 share目录 → /usr/share/postgresql/14 
pg14 数据目录 → /var/lib/postgresql/14/data
```

> _⚠️ 启动命令修改为_ _`/bin/bash`，避免 pg 服务自动启动。_

截图：  

![](https://pica.zhimg.com/v2-2ac1ad6442a934dda826d5c2437df7b0_1440w.jpg)

![](https://picx.zhimg.com/v2-c3dd3f14a8a1c871cb2c8752687b2af9_1440w.jpg)

**步骤三：执行升级**

进入容器终端：

```text
chmod -R 777 /usr/lib/postgresql/14 
chmod -R 777 /usr/share/postgresql/14 
chmod -R 777 /var/lib/postgresql/14/data  

su postgres 

cd /var/lib/postgresql  

pg_upgrade -b /usr/lib/postgresql/14/bin/ -B /usr/lib/postgresql/17/bin/ -d /var/lib/postgresql/14/data/ -D /var/lib/postgresql/data/ --old-options="-c shared_preload_libraries=vchord" --new-options="-c shared_preload_libraries=vchord"
```

> _升级成功后，输出：_

`PostgreSQL init process complete; ready for start up.`

* * *

### **5\. 更新 Immich 镜像信息**

1.  1\. 将 Immich 中 `immich_postgres` 镜像更新为：  
    `ghcr.io/immich-app/postgres:17-vectorchord0.4.3-pgvectors0.3.0`
2.  2\. 更新挂载路径为 pg17 数据目录
3.  3\. 重启 Immich，验证功能正常

* * *

**参考资料**
--------

[更新 Docker 运行的 PostgreSQL 实例的版本 | 个人技术学习](https://link.zhihu.com/?target=https%3A//6xyun.cn/article/pg-upgrade)