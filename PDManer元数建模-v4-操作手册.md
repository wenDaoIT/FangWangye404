# PDManer元数建模-v4-操作手册
  
  
  
  
数据库建模软件  
用户操作手册  
  
  
  
  
  
  
目录  
1 概述 7  
1.1 运行环境 7  
1.1.1 操作系统 7  
1.1.2 硬件配置 7  
1.1.3 相关软件 7  
2 主要功能介绍 8  
2.1 特别说明 8  
2.2 启动 8  
2.3 欢迎界面 9  
2.4 新建项目 10  
2.4.1 创建新项目 10  
2.4.2 填写项目信息完成创建 10  
2.5 维护数据类型 11  
2.5.1 基础数据类型 11  
2.5.2 数据域 13  
2.5.3 数据库及语言 16  
2.6 项目设置 19  
2.6.1 新建表默认字段 19  
2.6.2 新建表默认属性 20  
2.6.3 系统参数设置 22  
2.7 数据表管理 23  
2.7.1 新建数据表 23  
2.7.2 字段设置 24  
2.7.3 索引设置 28  
2.7.4 代码生成 31  
2.8 视图管理 31  
2.8.1 新建视图 31  
2.8.2 编辑视图 35  
2.8.3 索引设置 38  
2.8.4 代码生成 38  
2.9 关系图管理 38  
2.9.1 简单的概念模型图 38  
2.9.2 数据表关系图 48  
2.10 数据字典 54  
2.10.1 创建数据字典 55  
2.10.2 编辑数据字典 56  
3 生态对接功能介绍 58  
3.1 数据库逆向解析 58  
3.1.1 建立数据库连接 58  
3.1.2 解析表清单 59  
3.1.3 选择目标表 61  
3.1.4 确认 61  
3.2 导入PowerDesigner文件 62  
3.2.1 选择pdm文件 62  
3.2.2 解析表清单并选择目标表 63  
3.2.3 确认 63  
3.3 导入PDMan文件 64  
3.3.1 选择文件 64  
3.3.2 解析表清单并选择目标表 65  
3.3.3 确认 65  
3.4 导出WORD文件 67  
3.4.1 选择导出位置 67  
3.4.2 打开导出文档 70  
3.5 导出DDL文件 71  
3.5.1 选择导出数据库及表 71  
3.5.2 选择导出位置 73  
3.6 导出/导入数据域 73  
3.6.1 导出数据域 73  
3.6.2 导入数据域 74  
3.7 导出图片文件 75  
4 高级功能 78  
4.1 多模块分组以及简单项目简单模式 78  
4.1.1 切换模块分组视图 78  
4.1.2 设置项目默认使用分组模式 79  
4.1.3 新建分组并设置分组下对象 80  
4.1.4 批量改变分组 83  
4.2 字段库管理 84  
4.2.1 定位字段库 84  
4.2.2 字段库管理 86  
4.2.3 字段库分类管理 87  
4.2.4 字段库分类下字段管理 88  
4.2.5 数据表字段加入字段库 88  
4.2.6 字段库应用于建表 90  
4.2.7 字段库应用于关系图 91  
4.2.8 导出字段库 93  
4.2.9 导出字段库 93  
4.3 字段的批量操作 94  
4.3.1 批量大小写转换 94  
4.3.2 批量显示及隐藏 94  
4.3.3 批量修改数据域 95  
4.4 全局搜索以及定位 97  
4.4.1 数据表定位 98  
4.4.2 数据表详情 99  
4.4.3 字典搜索 100  
4.5 可定制化的代码模板 101  
4.6 可定制化的WORD文档模板 101  
4.7 国际化多语言切换 104  
  
1 概述  
1.1 运行环境  
1.1.1 版本历史  
PDManer为本应用的第四个版本，版本更迭中，也经历过更名，在这里建议使用历史版本的朋友尽快升级到最新版本，过去版本介绍：  
第一次重大版本迭代：  

![](https://github.com/wenDaoIT/FangWangye404/blob/pic/clipper/2025-3-21%2016-14-08/d342d76c-34bd-496d-9881-4dc472ea1d4a.webp?raw=true)

  
第二次迭代，经历了更名：  

![](https://github.com/wenDaoIT/FangWangye404/blob/pic/clipper/2025-3-21%2016-14-08/378dbdb4-5741-453a-8c4e-7a087ca33613.webp?raw=true)

  
最新的版本：  

![](https://github.com/wenDaoIT/FangWangye404/blob/pic/clipper/2025-3-21%2016-14-08/bbfcf8c6-ca29-4566-87bb-eac0ad7b9627.webp?raw=true)

  
  
1.1.2 操作系统  
Linux系列(如Redhat,CentOS，SUSE等），Windows，MacOS以及国产操作系统等  
1.1.3 硬件配置  
工作台式机或笔记本，CPU：酷睿I3及以上，内存: 4G  
1.1.4 相关软件  
Java8，NodeJS  
  
2 主要功能介绍  
2.1 特别说明  
1截图中所有的数据是模拟在真实场景下制作的模拟数据，并非客户的真实数据；  
2本文档操作展示平台为Win10。  
2.2 启动  
下载安装文件，双击“PDManer-win\_v4.0.0.exe”，启动安装：  

![](https://www.yuque.com/pdmaner/docs/%E5%AE%89%E8%A3%85exeLogo.jpg)

  
  
安装完毕后双击“PDManer”，启动应用：  

![](https://www.yuque.com/pdmaner/docs/%E5%90%AF%E5%8A%A8%E8%BD%BD%E5%85%A5.png)

  
  
  
2.3 欢迎界面  
启动成功后，进入欢迎页面，如图所示：  

![](https://www.yuque.com/pdmaner/docs/%E6%93%8D%E4%BD%9C%E4%B8%BB%E9%A1%B5%E9%9D%A2.jpg)

  
2.4 新建项目  
2.4.1 创建新项目  
●通过欢迎界面，点击“新建”按钮，新建项目：  

![](https://www.yuque.com/pdmaner/docs/%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE1.jpg)

  
2.4.2 填写项目信息完成创建  
●完成创建后，进入项目主界面，如图所示：  

![](https://www.yuque.com/pdmaner/docs/%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE2.jpg)

  
2.5 左侧栏-数据域  
2.5.1 基础数据类型的编辑  
系统自带常见基础数据类型（如字串，小数，日期等），同时用户也可以根据自己的需要添加新的数据类型。数据类型只有类型，无长度，长度需要用户在定义字段时设置或者在数据域中进行模板化设置。  
1查看数据类型：点击左侧数据域导航项，然后选中数据类型，可查看详情，如图所示：

![](https://www.yuque.com/pdmaner/docs/%E6%95%B0%E6%8D%AE%E5%9F%9F%E6%96%B0%E5%A2%9E%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B.jpg)

  
2创建新的数据类型：右击“数据类型”分组，弹出创建菜单，如图所示：  

![](https://www.yuque.com/pdmaner/docs/%E6%95%B0%E6%8D%AE%E5%9F%9F%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B%E8%AE%BE%E7%BD%AE.png)

  
点击“确定”后，完成创建。  
3编辑数据类型：双击数据类型，弹出数据类型编辑页面，界面显示同上。  
2.5.2 数据域的编辑  
数据域是在数据类型的基础上，基于当前项目，定义有一定业务含义的数据类型，例如我们定义ID为32位长度的字串，金额为18位整数+小数点后保留6位的小数，名称为250位长度的字串等，主要用于快速设置字段的数据类型。  
1查看数据域：点击左侧数据域导航项，如图所示：  
  
2新建数据域：点击左侧数据域分类导航项，如图所示：  
  
  
3编辑数据域：双击一个已有的数据域，如上图所示：  
第三项，数据类型，为基础数据类型，选定数据类型之后，再设置长度以及小数位数。设置好数据域之后，在数据表中选择此数据域时，就会指定字段数据类型以及长度了，如下图：  
  
4编辑数据库（本次更新）：  
本次新增了数个可连接的数据库类型，整体如下：  
●mysql（默认）  
●ORACLE  
●SQLserver  
●PostgreSQL  
●DB2  
●DM  
●GaussDB  
●Kingbase  
●MaxCompute  
●SQLite  

![](https://www.yuque.com/pdmaner/docs/%E6%94%AF%E6%8C%81%E6%95%B0%E6%8D%AE%E5%BA%93.jpg)

  
右击左侧栏“数据域”中的数据库菜单或上边栏的数据库图标，添加新的数据库类型，如图所示：  

![](https://www.yuque.com/pdmaner/docs/%E6%96%B0%E5%A2%9E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%85%A5%E5%8F%A3.jpg)

  
点击弹窗中的“新增”：  

![](https://www.yuque.com/pdmaner/docs/%E6%96%B0%E5%A2%9E%E6%95%B0%E6%8D%AE%E5%BA%93%E5%BC%B9%E7%AA%97.jpg)

  
点击新增，选择数据源、填写相关参数建立连接：  

![](https://www.yuque.com/pdmaner/docs/%E6%96%B0%E5%A2%9E%E6%95%B0%E6%8D%AE%E5%BA%93%E8%BF%9E%E6%8E%A5.jpg)

  
点击测试，如果测试通过，则创建完成。  
  
2.5.3 代码生成器（本次更新）  
数据库及语言用于定制不同类型的数据库，定制在该种数据库类型下，他的创建表DDL语句模板，创建索引语句模板等。  
1代码生成器：点击左侧栏代码生成器，现支持以下语言：  
●JAVA  
●javaMybatis  
●javaMybatisPlus  
●C#  

![](https://www.yuque.com/pdmaner/docs/%E5%BB%BA%E8%A1%A8%E4%BB%A3%E7%A0%81%E7%94%9F%E6%88%90.jpg)

  
2  
  
数据库定义和程序代码定义是两种不同的类型。  
1数据库定义：数据库定义，支持数据表创建DDL，索引创建语句模板，语句模板是一个基于javasript的开源模板引擎:”doT.js”  
2预览编辑：点击预览编辑，进入一个有案例数据，代码模板，预览效果的编辑界面，在中间的模板定制区完成相关代码模板定制，顶部的有关于doT.js快速学习的介绍内容窗口，可以点击打开，预览编辑如下图：  
  
模板引擎介绍，如下图：  
  
  
  
2.6 项目设置  
打开项目后，通过点击工具栏的“设置”按钮，进入项目设置界面，如下图：  
  
  
2.6.1 新建表默认字段  
设置界面的第一个标签页，为设置新建表预置字段，设置之后，每新一个表，将会预置这些字段，如下图：  
  
新建表后，将会预置项目统一设置的预置字段，如下图：  
  
2.6.2 新建表默认属性  
设置界面的第二个标签页，为设置新建表预置属性，设置之后，每新一个表，将会预置这些属性集，如下图：  
  
此界面，工具栏提供新增，删除，上移，下移等按钮，对属性列表进行相应操作。  
设置好预置属性后，新建表的扩展属性，将会预置此属性，如下图：  
  
  
2.6.3 系统参数设置  
设置界面的第三个标签页，为系统参数，对项目进行一些统一的设置，如下图：  
  
参数说明，如下：  
| 

JAVA\_HOME  


 | 

JDK的JAVA\_HOME路径，该变量不和项目绑定，一个客户端一份  


 |
| 

SQL分隔符  


 | 

生成DDL建表语句时，分隔符变量的值  


 |
| 

WORD模板  


 | 

导出WORD文档使用的WORD文档模板，用于客户化定制自己生成文档  


 |
| 

语言  


 | 

目前支持中文，英文两种语言  


 |
| 

模型默认显示模式  


 | 

如果项目不需要分模块，则设置为简单模式，如果项目较大，设置为分组模式，能够支持更多业务表的分组  


 |
| 

关系图最大展示字段数  


 | 

数据表在关系图上最多允许展示的字段数，一般而言，关系图上展示的字段为该表的典型字段。  


 |  
2.7 数据表管理  
2.7.1 新建数据表  
右击“数据表”弹出快捷菜单，选择“新增数据表”，如下图：  
  
填写表信息，如下图：  
  
点击“确定”后，如下图：  
  
2.7.2 字段设置  
双击数据表，标签页中打开表编辑模式，如下图：  
  
2.7.2.1 字段行选择操作说明  
1单击行号选中当前行  
2按住Ctrl+单击行号，选中跳跃行  
3按住Shift+单击行号，选中连续行  
4选中行后，Ctrl+C复制，Ctrl+V粘贴  
5单元格内部使用Ctrl+Shift+U转换大小写  
6选择多行，能够批量调整数据域  
2.7.2.2 工具栏操作说明  
选中一行或者多行后，工具栏允许的操作按钮将会被启用，允许的操作及操作内容如下：  
●字段行允许的操作如下：  
| 

●置顶：选中行移至最上方置顶；  
●上移：选中行相对当前位置上移一行；  
●下移：选中行相对当前位置下移一行；  
●置底：选中行移至最下方置底；  
●删除：删除选中行；  
●可见：设置选中行在关系图上可见（行首眼睛图标标示为可见状态）；  
●隐藏：设置选中行在关系图上不可见（行首眼睛图标标示为不可见状态）；  
●入库：选中行移至”标准字段库“，字段库中字段列表在其他表编辑时可复用；  


 |  
点击“新增”按钮在当前选中行位置前添加一个空行，如果没有选中行，则在最末尾添加一个空行，新增按钮分段按钮后面有一次性添加5行，10行，15行的快捷操作，方便一次性添加多行。  
  
●字段列允许的操作  
在选中一列后，允许对当前列进行以下操作：  
| 

●左移：将选中列相对当列位置右移一列；  
●右移：将选中列相对当列位置左移一列；  
●大小写：将选中列的字段名大小写相互转换；  


 |  
第一行表头内嵌操作按钮，可进行操作如下：  
| 

●眼睛图标-显示隐藏：设置当前列在关系图上是否显示；  
●锁图标-冻结：冻结当前列，横向滚动时，确保当前列一直可见；  


 |  
2.7.2.3 字段填写说明  
| 

●字段代码：字段的英文代码，一般情况下为数据库字段代码；  
●显示名称：字段的显示名称，一般情况下为字段的中文名，生成DDL后拼到注释字段中；  
●数据域：设置字段所使用的数据域，通过数据域快速设置数据类型，长度及小数位数；  
●数据类型：设置字段的数据类型，一般而言是数据库的数据类型；  
●长度：设置字段的长度；  
●小数位数：设置字段的小数位数，长度-小数位数=整数位数；  
●说明：注释说明，对字段的业务含义进行补充说明；  
●数据字典：关联字段的数据字典，例如1表示男，2表示女；  
●默认值：字段默认值，如果为数字，填写如：10，如果为字串，则写为‘10’；  


 |2.7.2.4 字段扩展属性  
在字段页面最右侧有个拓展属性，如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
可以给字段增加拓展属性，满足用户对模型文件的自定义需求  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
2.7.3 索引设置  
双击数据表，标签页中打开表编辑模式，切换到“索引”标签页，如下图：  
  
●新增、删除索引：通过工具栏的新增，删除按钮完成索引的相应操作；  
●调整索引：通过工具栏的上移下移等操作调整索引位置；  
●索引下添加删除字段：  
  
字段区工具栏点击“新增”按钮，选择数据表字段，如下图：  
  
2.7.4 代码生成  
2.7.4.1 数据库代码  
双击数据表，标签页中打开表编辑模式，切换到“数据库代码”标签页，如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
所有的数据域均列至标签页下方，选择不同的数据库，可以生成该数据库的数据表代码，同时还可以选择新建、删除、新建索引代码。并可以在数据域调整代码模板实现数据表向对应代码的转换。  
v4.1.0修复了MaxCompute数据库注释写法的错误。  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
2.7.4.2 程序代码  
切换到“程序代码”标签页，如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
在程序代码中可以选择Java、C#语言，如果是Java语言还能生成对应的MyBatis、MyBatisPlus文件。  
2.7.4.3 路径及变量  
点击左侧的路径及变量标签，如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
保存位置可以设置文件的保存路径，nameSpace包路径。点击生成可以在相应的文件夹下生成对应的文件。  

![](https://www.yuque.com/pdmaner/docs/image.png)

  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
2.7.4.4 代码生成器  
选择左侧的代码生成器标签，可以查看编辑代码生成的模板。如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
双击左侧的程序代码，能编辑查看响应语言的模板。其中mybatis模板分成Controller、Service、ServiceImpl、Mapper、Mapper.xml、Entity6个模板。如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
v4.1.0增加了对Golang语言模板的支持  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
2.7.5 批量修改表名  
右击数据表，可以看到列出全部按钮，如下图：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
点击列出全部，可以看到系统中所有的表名以及显示的名称，在该页面可以进行编辑，达到批量修改的目的。  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
2.8 视图管理  
此视图主要用于管理视图的字段，以及联合多个对象生成JavaBean等操作。  
2.8.1 新建视图  
  
右击“视图”弹出快捷菜单，选择“新增视图”，如下图：  
  
1选择数据表  
  
1选择数据表下字段  
  
1填写视图信息  
  
1确定生成视图  
  
2.8.2 编辑视图  
1打开视图  
导航区，双击视图，打开视图编辑，如下图：  
  
视图，工具栏操作与数据表工具栏操作完全一致。  
1调整实体  
  
  
1添加删除字段  
  
  
  
2.8.3 索引设置  
视图的索引设置与数据表操作一致。  
2.8.4 代码生成  
视图的代码生成与数据表操作一致。  
  
2.9 关系图管理  
2.9.1 简单的概念模型图  
2.9.1.1 创建关系图  
关系图分组右击，选择”新增关系图“，如下所示：  
  
  
2.9.1.2 编辑关系图  
双击刚才创建好的关系图，右侧编辑关系图，如下图：  
  
  
2.9.1.3 编辑关系图内容  
1拖入形状  
从工具栏将相应形状拖入关系图，如下图：  
  
1填写形状名称  
双击形状，输入形状名，如下图：  
  
1建立关联  
鼠标移至源形状，形状外边显示多个锚点，如下图：  
  
拖动锚点至目标形状，如下图：  
  
放开鼠标后，关系建立完成，如下图：  
  
  
1设置形状样式  
选中形状，设置填充颜色，如下图：  
  
选中形状，设置文字颜色，如下图：  
  
1编辑关联关系  
选中连线，右击弹出菜单，如下图：  
  
选中“编辑关系”，设置一对多的对应关系，如下图：  
  
选中“编辑关系”，设置一对多的对应关系，如下图：  
  
  
2.9.1.4 形状分组  
分组组件框用于将类似的形状放到一个分组框中：  
从工具栏拖入分组框，拖动边框上的小圆点能够改变形状的大小，双击分组框，可填写分组框内容，如下图：  
  
  
选中形状对象，可以将形状放入分组框，此后，拖动分组框，形状会一起被拖动，如下图：  
  
  
2.9.2 数据表关系图  
2.9.2.1 创建关系图  
关系图创建与概念模型图的创建方式一致。  
2.9.2.2 放入/创建表  
通过工具栏”新建空表”拖动至画布，将创建新表，如下所示：  
  
  
双击新建的表，打开编辑窗口，如下所示：  
  
  
也可以从左侧表清单中将表拖入至画布中，如下所示：  
  
  
2.9.2.3 设置显示大小  
在关系图或者左侧表清单，双击打开表编辑模式，关系图的大小，由显示的列以及显示的字段个数决定，如下图所示：  
  
  
2.9.2.4 建立关联  
由源字段锚点向目标字段锚点拖动，默认建立源字段至目标字段的1对N关系，如下图所示：  
  
  
  
右击弹出快捷菜单，选中编辑关系，可编辑关联关系，如下图：  
  
  
  
右击弹出快捷菜单，选中关系说明，可关系说明文字，如下图：  
  
  
  
  
2.9.2.5 关系图分组  
数据表分组同形状分组操作方法一致。  
  
2.10 数据字典  
数据字典用于解决字段值代码与代码解释的映射关系，如1表示男，2表示女等情况。如下图所示：  
  
2.10.1 创建数据字典  
右击“数据字典”分组，弹出快捷菜单，选择“新增字典”，如下图所示：  
  
  
  
2.10.2 编辑数据字典  
双击数据字典项，打开并编辑数据字典项，如下图所示：  
  
  
2.11 版本管理  
版本管理用于查看数据表的变更记录，添加、更改、删除字段以及表信息后，会自动生成变更脚本。如下图所示：  

![](https://www.yuque.com/pdmaner/docs/image.png)

  
3 生态对接功能介绍  
3.1 数据库逆向解析  
3.1.1 建立数据库连接  
通过JDBC配置数据库连接，点击工具栏上”数据库“按钮，如下图：  
  
点击数据库连接配置的“新增”按钮，如下图：  
  
填写数据库配置信息，如下图：  
  
特别说明：如果jdbc的驱动类位于第三方jar包，则可以通过自定义驱动选择第三方jar包。目前MySQL，DB2，ORACLE，PostgreSQL这几个数据库系统提供默认驱动包，不需额外加载。  
3.1.2 解析表清单  
点击工具栏导入/从数据库导入，如下三图：  
  
  
3.1.3 选择目标表  
  
3.1.4 确认  
  
  
3.2 导入PowerDesigner文件  
3.2.1 选择pdm文件  
点击工具栏上”导入/导入PowerDesigner文件”，按钮，如下图：  
  
  
3.2.2 解析表清单并选择目标表  
  
3.2.3 确认  
  
3.3 导入PDMan文件  
3.3.1 选择文件  
点击工具栏上”导入/导入PDMan文件”，按钮，如下图：  
  
  
3.3.2 解析表清单并选择目标表  
PDMan文件，如果数据表在关系图上，则默认被选中，且不能取消：  
  
3.3.3 确认  
由于PDMan是强分组的，因此导入后会将视图切换对分组视图，如下图：  
  
  
  
切换至简单视图，如下图：  
  
3.4 导出WORD文件  
3.4.1 选择导出位置  
点击工具栏上”导出/导出WORD”，按钮，如下图：  
  
  
  
  
  
3.4.2 打开导出文档  
  
  
3.5 导出DDL文件  
3.5.1 选择导出数据库及表  
  
  
  
  
3.5.2 选择导出位置  
  
点击“存储”后，将此文件保存至相应位置。  
3.6 导出/导入数据域  
导出导出数据域，一次性导出导入数据类型+数据域+数据库类型。  
3.6.1 导出数据域  
将数域导出为JSON文件，如下图：  
  
  
  
3.6.2 导入数据域  
将数域导出的JSON导入至项目中，如果冲突则覆盖，如下图：  
  
  
  
3.7 导出图片文件  
打开关系图，将关系图导出为图片，如下图：  
  
  
  
  
4 高级功能  
4.1 多模块分组以及简单项目简单模式  
当系统较为复杂的情况下，需要对数据表、视图、关系图、数据字典进行分组分模块管理，又因为同一数据表可能会被多个模块使用，因此允许同一表、视图、字典从属于多个分组，如下图：  
  
4.1.1 切换模块分组视图  
只需要将导航区的“简单模式”前的勾去掉，如下图：  
  
  
  
4.1.2 设置项目默认使用分组模式  
打开：设置/系统参数，在参数“模型默认显示模式”中，选择“分组模式”，如下图：  
  
这样，第次打开本项目时，就会默认显示为分组模式打开。  
4.1.3 新建分组并设置分组下对象  
分组模式下，右击导航的空白区域，弹出快捷菜单，选择“新增分组”，如下图：  
  
  
切换至数据表、视图、关系图、数据字典等标签，归属于本分组下的相关对象，如下图：  
  
  
  
打开对象，查看所属的所有分组，如下图：  
  
  
  
  
4.1.4 批量改变分组  
选择多个对象，右击弹出菜单，选择“改变分组”，可实现批量改变分组，如下图所示：  
  
  
  
4.2 字段库管理  
右字段库用于存放系统中常用字段，用于在新建数据表时，能够快速引入，在于字段复用，统一数据标准，元数建模提供字段库管理功能。  
4.2.1 定位字段库  
通过关系图或者数据表编辑视图均可打开字段库，如下三图：  
  
  
  
4.2.2 字段库管理  
直接通过字段库管理功能添加字段，如下图：  
  
  
  
4.2.3 字段库分类管理  
通过字段库管理界面上方的按钮，可完成字段分组的添加，删除等相关操作，如下图：  
  
  
  
  
4.2.4 字段库分类下字段管理  
点击展开，打开分组成字段库，如下图：  
  
通过字段列表上方工具栏的添加删除等相关操作，可维护字段库下字段信息：  
4.2.5 数据表字段加入字段库  
打开需要加入字段库的数据表，点击工具栏上方的入库操作，如下图：  
  
  
打开需要加入字段库的数据表，点击工具栏上方的入库操作。  
可以在分类中选择已有分类，如下图：  
  
也可以重新填写新的分类代码及名称，新选择的字段放入新的分类下，如下图：  
  
  
4.2.6 字段库应用于建表  
双击打开需要编辑的数据表，并展开字段库，如下图：  
  
字段库中选择需要复用的字段，拖入数据表，如下图：  
  
如果字段重复，则忽略，没重复的部分，自动加入目标数据表，如下图：  
  
  
4.2.7 字段库应用于关系图  
双击打开需要编辑的关系图，并展开字段库，如下图：  
  
选中目标字段，拖入目标表，如下图：  
  
操作结果，如下图：  
  
  
4.2.8 导出字段库  
  
通过以上操作，将数据库导出至文件。  
  
4.2.9 导出字段库  
  
通过以上操作，从文件将字段库导入至系统。  
  
4.3 字段的批量操作  
4.3.1 批量大小写转换  
选中一列，批量转换该列的大小写，如下图：  
  
4.3.2 批量显示及隐藏  
选中多个字段行，批量设置显示隐藏，如下图：  
  
4.3.3 批量修改数据域  
选中多个字段行，点击第一行的数据域，统一设置选中行的数据域，如下图：  
  
  
  
4.4 全局搜索以及定位  
全局搜索用于根据代码或名称快速定位数据表、视图、数据字典、等，如下图：  
  
4.4.1 数据表定位  
  
  
  
4.4.2 数据表详情  
  
  
  
4.4.3 字典搜索  
  
  
  
  
  
4.5 可定制化的代码模板  
数据库及语言用于指定数据库DDL语句及程序代码模板，基于doT.js引擎，进行配置，以适应不同的业务情况，代码模板请参考：2.5.3数据库及语言。  
  
4.6 可定制化的WORD文档模板  
导出WORD文档，通过java+poi-tl构建生成引擎，文档模板可定制化，数据模型为可通过设置界面查看，如下图：  
  
查看模型，用于查看模板对应的数据模型，如下图：  
  
另存为，用于另存当前word模板，如下图：  
  
另存为，用于另存当前word模板，如下图：  
  
  
4.7 国际化多语言切换  
通过系统设置可切换软件语言，目前支持简体中文和英文。  
打开软件设置，如下图：  
  
  
  
换后的英文界面，如下图：