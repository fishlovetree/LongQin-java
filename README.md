# 龙琴工作流系统[java版]

<h1>介绍</h1>

LongQin-java 是一款基于Spring Boot、Spring Cloud、Vue3、Element Plus的前后端分离微服务低代码工作流平台，内置模块如：部门管理、角色用户、菜单、数据权限、日志管理、表单设计器、流程设计器、列表设计器、图表设计器等。可用于企业日常办公及个人学习娱乐。

QQ群：413025488

#### 在线体验
- JAVA版本：http://121.40.200.58/
默认账号密码：admin/11111111
- .NET版本：https://www.signsing.com
默认账号密码：custom/11111111

#### 内置功能
- 公司管理：以公司为单位进行数据权限隔离，公司内部员工只有本公司数据权限。
- 用户管理：用户是系统操作者，该功能主要完成系统用户配置。
- 部门管理：管理公司内部部门信息。
- 职位管理：管理公司内部职位信息。
- 菜单管理：管理系统功能菜单及用户自定义菜单。
- 角色管理：角色菜单权限分配。
- 系统日志：系统正常操作日志记录和查询。
- 错误日志：系统异常信息日志记录和查询。
- 系统设置：设置公司基本信息。
- 公告管理：公司内部公告发布管理。
- 待办工作：工作流中待处理的事项。
- 已办工作：工作流中已处理的事项。
- 流程发起：发起工作流程。
- 自定义表单：表单设计器。
- 自定义流程：工作流设计器。
- 自定义列表：数据表格设计器。
- 自定义图表：canvas图形化展示页面设计器。

#### 技术选型
- 数据库: mysql5.6.26以上
- jdk: 1.8
- springboot: 2.1.4
- redis: 3.0
- vue: 3.4.31
- element-plus: 2.7.6
- sortablejs: 1.15.2
- vform3-builds: <a href="https://www.vform666.com/" target="_blank">3.0.10</a>

#### 项目结构说明
- longqin-business: 业务微服务，默认端口: 9162
- longqin-system: 账号微服务，默认端口: 9161
- longqin-register: 微服务注册中心，默认端口: 9160
- longqin-zuul: 微服务网关，默认端口: 9163
- longqin-web: 前端代码，默认端口: 3000

#### 主要特性
- 拖拉式生成丰富的表单，可选组件多达20余项。
- 拖拉式生成复杂工作流程，包含提交、分支、多人协作、自动识别审批人等特性。
- 拖拉式生成丰富的数据报表，自定义列表包含增删改功能。
- 拖拉式生成丰富的图表界面。
- 运用自定义表单和自定义列表以及自定义图表功能可扩展其他功能模块，一套系统可幻化出无数套。

<h1>环境部署</h1>

#### 准备工作

```
JDK >= 1.8 (推荐1.8版本)
Mysql >= 5.6.0 (推荐5.7版本)
Redis >= 3.0
Maven >= 3.0
Node >= 18
```

#### 后端运行

1、前往Gitee下载页面(https://gitee.com/fish_fish_wood/long-qin-java)下载解压到工作目录
2、导入到Eclipse，菜单 File -> Import，然后选择 Maven -> Existing Maven Projects，点击 Next> 按钮，选择工作目录，然后点击 Finish 按钮，即可成功导入。Eclipse会自动加载Maven依赖包，初次加载会比较慢（根据自身网络情况而定）
3、创建数据库longqin并导入数据脚本“数据库.sql”
4、配置mysql数据源，修改conf/application-dev.yml（开发环境）、conf/application-prod.yml（生产环境）文件，增加支持mysql数据源配置

```
url: jdbc:mysql://localhot:3306/longqin?useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowMultiQueries=true
username: root
password: 123456
driver-class-name: com.mysql.cj.jdbc.Driver
```
5、配置Redis，修改conf/application-dev.yml（开发环境）、conf/application-prod.yml（生产环境）文件，增加支持Redis配置

```
redis:
    host: localhost
    port: 6379
    password: 123456
    database: 0
    timeout: 5000
    jedis:
      pool:
        max-active: 50
        max-wait: 3000
        max-idle: 20
        min-idle: 2
```
6、打开运行微服务

- longqin-register: 微服务注册中心，默认端口: 9160
- longqin-system: 账号微服务，默认端口: 9161
- longqin-business: 业务微服务，默认端口: 9162
- longqin-zuul: 微服务网关，默认端口: 9163

#### 前端运行
```
# 进入项目目录
cd longqin-web

# 安装依赖
npm install

# 强烈建议不要用直接使用 cnpm 安装，会有各种诡异的 bug，可以通过重新指定 registry 来解决 npm 安装速度慢的问题。
npm install --registry=https://registry.npmmirror.com

# 本地开发 启动项目
npm run dev
```

1、打开浏览器，输入：(http://localhost:3000) 默认账户/密码 admin/11111111）
若能正确展示登录页面，并能成功登录，菜单及页面展示正常，则表明环境搭建成功


>**提示**
>因为本项目是前后端完全分离的，所以需要前后端都单独启动好，才能进行访问。
前端安装完node后，最好设置下淘宝的镜像源，不建议使用cnpm（可能会出现奇怪的问题）

#### 部署系统
1、打包工程文件
在LongQin项目右键>Run As>Maven install，生成jar包文件。然后会在项目下生成target文件夹包含jar
2、部署工程文件
使用命令行执行：java –jar longqin-system-1.0.0.jar
3、打包前端文件
在vscode中执行命令：npm run build，构建打包成功之后，会在根目录生成 dist 文件夹，里面就是构建打包好的文件，通常是 ***.js 、***.css、index.html 等静态文件
>通常情况下 dist 文件夹的静态文件发布到你的 nginx 或者静态服务器即可，其中的 index.html 是后台服务的入口页面。

4、Nginx配置
```
events {
    worker_connections 1024;
}

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;
    
    #服务器的集群  
    upstream  longqin.com {  #服务器集群名字   
	  #服务器配置   weight是权重的意思，权重越大，分配的概率越大。
	    server  localhost:9163 weight=1 fail_timeout=1s;
    }

    server {
        listen       80;
        server_name  localhost;

        
        location / {
    	    root   /usr/share/nginx/html/dist;
    	    try_files $uri $uri/ /index.html; #前端采用history去掉了'#',nginx因此配置相应路由
    	    index  index.html;
        }
        
        location /api/ {
            proxy_pass http://longqin.com/;
    	    proxy_connect_timeout       1;#连接超时时间
    			
    	    #获取客户端真实ip
    	    proxy_set_header        Host            $host;
    	    proxy_set_header        X-Real-IP       $remote_addr;
    	    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
```
<h1>操作手册</h1>
#### 新增公司
- 登录admin账号，打开【系统管理】-【公司管理】模块，点击【新增】按钮，在弹出框中输入公司相关信息，然后点击【确定】按钮完成新增。
- ![b7989c3f7e4bc5c35a77bcf35636b70f.png](en-resource://database/554:0)
#### 新增管理员角色
- 登录admin账号，打开【系统管理】-【角色管理】模块，点击【新增】按钮，在弹出框中输入角色信息，然后点击【确定】按钮完成新增。
- ![f909c01af2f9e935268353e81bf09f7a.png](en-resource://database/570:0)

#### 分配权限
- 登录admin账号，打开【系统管理】-【角色管理】模块，在新增的角色右侧点击【分配权限】按钮，在弹出框中选择权限对应的功能菜单，然后点击【确定】按钮完成分配。
- ![a4a22ffd6e7339dc92a28cfd6b412148.png](en-resource://database/558:0)
- ![0556866e071fb5c17b11b68ab7cd84c8.png](en-resource://database/560:0)
#### 新增公司管理员
- 登录admin账号，打开【系统管理】-【用户管理】模块，点击【新增】按钮，在弹出框中输入用户信息，然后点击【确定】按钮完成分配。
- ![94f5b3af5858804d9d197f9d254a1367.png](en-resource://database/564:0)

> admin创建的用户应选择新增的公司，以作为公司的管理员。管理员的所属部门和职位为空，角色应选择admin创建的管理员角色。新增完成后应采用公司管理员账号登录系统进行后续操作。

#### 新增部门
- 登录公司管理员账号，打开【系统管理】-【部门管理】模块，点击【新增】按钮，在弹出框中输入部门信息，然后点击【确定】按钮完成新增。
- ![154cd35130c95ac39d98418c0c098466.png](en-resource://database/566:0)
#### 新增职位
- 登录公司管理员账号，打开【系统管理】-【职位管理】模块，点击【新增】按钮，在弹出框中输入职位信息，然后点击【确定】按钮完成新增。
- ![eb915fb96a42a591dbed7fc0ab836f05.png](en-resource://database/568:0)
#### 新增内部角色
- 登录公司管理员账号，打开【系统管理】-【角色管理】模块，点击【新增】按钮，在弹出框中输入角色信息，然后点击【确定】按钮完成新增。
- ![4ec222d526ae447c3051f6441576bfa4.png](en-resource://database/576:0)
#### 新增公司员工
- 登录公司管理员账号，打开【系统管理】-【用户管理】模块，点击【新增】按钮，在弹出框中输入用户信息，选择所属部门、职位和角色，然后点击【确定】按钮完成分配。
- ![df95db0092559e66190fee692dcc298c.png](en-resource://database/578:0)
#### 表单设计
- 登录公司管理员账号，打开【自定义表单】-【表单设计器】模块。
- ![12f61e8b542e31361bffc9334e4345fe.png](en-resource://database/580:0)

1、添加组件
- 鼠标选中页面左侧组件库中组件，拖动到中间区域。
- ![8d5c7ed7c532c897c3d7cff8efd5f289.png](en-resource://database/582:0)
- ![9d31ef337cabc39a341ed476c10bcd4c.png](en-resource://database/584:0)
2、删除组件
- 鼠标点击组件右下角删除按钮，完成组件删除。
- ![19129572f972dfc826037356f8a2b22a.png](en-resource://database/586:0)
3、移动组件
- 在表单设计区域，鼠标选中已添加的组件并上下拖动，实现组件位置的调整。
- ![5c7ecc11c9470eb0ea01a470709ee1ae.png](en-resource://database/588:0)
4、组件设置
- 在表单设计区域，鼠标选中已添加的组件，在页面右侧显示组件相关属性并可进行修改。
- ![9a82ef59f43f7b7663add14e5302493d.png](en-resource://database/590:0)
5、表单设置
- 在页面右侧点击【表单设置】按钮，打开表单设置界面。其中数据对象名称对应数据库表名，必须唯一。
- ![31101a58486f905a74450c34b5cbd1a0.png](en-resource://database/592:0)
6、保存
- 点击设计器上方的【保存】按钮完成表单保存。
- ![0e037a42d2d26fa2c5a4b0cd81d973ec.png](en-resource://database/594:0)
> 若提示“表单已存在”，则须更改表单设置里的“数据对象名称”。

#### 流程设计
- 登录公司管理员账号，打开【自定义流程】-【流程设计器】模块。
- ![7304de9a7682fcca62b152518c6fdf67.png](en-resource://database/596:1)

1、添加节点
- 鼠标点击【新建节点】按钮，系统会在设计器中新增一个流程节点。
- ![4506ee934951853125cab7579fdd6ef1.png](en-resource://database/598:0)
2、设置节点属性
- 鼠标选中新建的节点，系统会在设计器右侧显示节点属性。
- ![52e6cf3831a39e6d879dfda27d2e2a3f.png](en-resource://database/600:0)
```
节点名称：工作流节点名称。
节点类型：普通节点（前置和后置节点只有一个）、分流节点（前置节点只有一个，后置节点至少两个）、合流节点（前置节点至少两个，后置节点只有一个）、分合流点（前置和后置节点至少两个）
是否审批：是否是审批节点，如果选择审批节点，则自动选中默认的审批表单。
节点表单：节点对应的处理表单，必须设置。
多人协作：工作提交给多人处理后，如果选择多人协作，则需每个人都处理完毕，流程才会继续；反之，只需一人处理完毕，流程就会继续。
处理部门：节点对应工作由哪个部门处理。
处理职位：节点对应工作由哪个职位处理。
处理人：节点对应由哪个员工进行处理。
（若选择了处理人，则优先提交给处理人；若只选择了部门，则根据部门和提交人的职位自动匹配上级处理人；若只选择了职位，则根据职位和提交人的部门自动匹配上级处理人；若三者都不选，则根据提交人的部门和职位自动匹配上级处理人）
```
3、删除节点
- 鼠标选中要删除的节点，按下键盘中的“delete”按键，完成节点删除。
4、添加连线
-  选中添加的节点，当出现【前置】和【后继】标签后，点击【添加连线】按钮，完成连线额的添加，连线由前置指向后置。
- ![8355e2cf184236f0186fb32cb32b1078.png](en-resource://database/602:0)
5、设置连线属性
- 鼠标选中新建的连线，系统会在设计器右侧显示连线属性。
- ![746b2ad0139c92d494c7f2898243b280.png](en-resource://database/606:0)

```
连线名称：工作流连线名称。
连线条件：选择条件符号、条件表单、条件字段，输入条件值，表示前置节点表单中的值需满足设定的条件才会执行改连线对应的后继节点。如请假流程中不同的职级对应不同的方向
```
6、删除连线
- 鼠标选中要删除的连线，按下键盘中的“delete”按键，完成连线删除。
7、保存流程
- 在设计器上方输入流程名称，选择流程类别，然后点击【保存】按钮，完成流程保存。
- ![09f7c6107975498e244c8c10f8d958fd.png](en-resource://database/608:0)

#### 启动流程
- 登录公司普通员工账号，打开【我的工作】-【流程发起】模块，点击流程右侧【启动】按钮，打开流程发起节点表单，输入表单内容后点击【提交】按钮，完成流程发起。
- ![f2fea4f2db200cb5792be918a913e0aa.png](en-resource://database/610:0)
- ![23c89ae4b36fe8bc78d908c94ddd1e37.png](en-resource://database/612:0)
> 若出现提示“找不到下个节点处理人”，则表明发起流程的员工没有配置好部门和角色，或者下个节点没有配置处理人。

#### 流程处理
- 登录流程处理人账号，打开【我的工作】-【待办国内工作】模块，显示待处理工作清单，点击【处理】按钮，在表单中输入相关内容点击【提交】按钮，完成处理。
- ![d3512c9cc9adc485befc8555138229db.png](en-resource://database/614:0)
- ![9e8d41b9e6f4e9c2fe40def7df75d5be.png](en-resource://database/616:0)

#### 列表设计
- 登录公司管理员账号，打开【自定义列表】-【列表设计器】模块。
- ![bdf21ca638754ebb0cd1c8df4d2c8f16.png](en-resource://database/618:0)
1、选择列表列。
- 先选择表头数据源，根据选择的数据源在表头选择框中加载数据源的列，勾选需要展示的列即完成列选择。系统会在表头属性框和预览窗口中显示选中的列
- ![34f3583b86e3e579c39c24baa0d2a3e4.png](en-resource://database/620:0)
2、调整列位置。
- 在表头属性框中上下拖动选中的列即可调整列显示位置，同时在预览窗口中会自动调整列位置。
3、设置列属性。
- 在表头属性框中可设置列的宽度、数据排序方式（按列升序或降序）。
- ![29b0e44bcc22a6da4c421d7f6636673e.png](en-resource://database/622:0)

4、列数据加工
- 在表头属性框中可选择列数据加工方式，与公式值联合使用。例如选择数据加工方式为“拼接”，则列表展示时显示列的原始值拼接上公式值。
- ![b5e1cb722c2b80435b727a418e4bf726.png](en-resource://database/624:0)
5、列搜索
- 在表头属性框中选择搜索条件，则在预览窗口中会新增相关搜索框。实际列表展示时可根据该条件进行搜索。
- ![159d43af95dc373c4776d229596c1885.png](en-resource://database/626:0)

6、列表增删改
- 勾选基本信息框中的增删改，则在预览窗口中会显示响应的按钮，点击按钮可对数据进行编辑。
- ![6e00d8af31bae5f1bee4d1011aebb6a9.png](en-resource://database/628:0)

7、保存列表
- 点击列表设计器中的【保存列表】按钮，完成保存，同时系统会在菜单【自定义列表】模块下面显示新增的列表模块。
- ![369b02ec55b5e0a2b68cda316a35ae45.png](en-resource://database/630:0)
- ![bb0092c847ec0e2437c3d4bf09c50319.png](en-resource://database/632:0)

#### 图表设计
- 登录公司管理员账号，打开【自定义图表】-【图表设计器】模块。
- ![469529b16ba55de32049cd9e41893192.png](en-resource://database/634:0)
1、添加图形
- 拖动页面左侧图形到设计器中即可完成图形添加。
- ![56f7bcd3a69c60ab65508bc13d55061a.png](en-resource://database/636:0)
2、移动图形
- 鼠标选中图形，左键拖动图形，或者按下键盘中的上下左右键即可实现拖动。
3、复制粘贴
- 鼠标选中图形，点击工具栏的复制粘贴按钮，或者按下键盘的ctrl+c和ctrl+v完成复制粘贴。
4、放大缩小
- 鼠标选中图形，在图形周围出现多个小黑框，拖动小黑框完成图形放大缩小，或者使用鼠标滚轮实现放大缩小。
5、旋转
- 鼠标选中图形，在图形上方出现旋转按钮，左右拖动旋转按钮完成图形旋转。
6、删除
- 鼠标选中图形，点击工具栏的删除按钮，或者按下键盘的delete按键即可完成删除。
7、撤销和重做
- ctrl+z和ctrl+y
8、自定义图形
- 图形设计好后，点击工具栏的保存按钮，保存成功后刷新页面，在左侧图形库中显示自定义的图形，拖动即可完成加载。
