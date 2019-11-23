# 基于SpringCloud+Hadoop+Vue的企业级网盘系统设计与实现
### 【2019届毕业设计】，【优秀毕业设计】，【华东交通大学】 

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/0.png)

## 一、应用组成  
> 前端：vue-projectManage   
后台：mycloud-admin   
提供前端服务：mycloud  ps:springcloud实现   
文件在线预览服务：file-online-preview   

github地址：    
> 1.vue-projectManage:https://github.com/chenxingxing6/vue-projectManage     
2.mycloud-admina:https://github.com/chenxingxing6/mycloud-admin   
3.mycloud:https://github.com/chenxingxing6/mycloud   
4.file-online-preview:https://github.com/chenxingxing6/file-online-preview      

---

## 二、总体设计
#### 2.1 运行环境
```lua
编程语言：Java、Mybatis、Spring、SpringBoot、SpringCloud、Node、Vue  
开发环境：Windows 10 + Mysql   
开发工具：WebStorm、IDEA编译器、Git、Maven  
应用部署服务器：SpringBoot内置Tomcat插件     
Node服务器：Node v10.15.3  
数据库：Mysql v5.5.59  
缓存服务：Redis v2.8.9  
代码仓库管理系统：GitHub  
服务器环境：处理器Core i5以上 
```

#### 2.2 基本处理流程
企业网盘系统的使用者分为企业普通员工和企业管理员，所以进行的基本处理流程是不一样的。企业普通员工进入本系统前台主界面后看到的是首页数据大盘，系统右上角有用户的头像和系统公告通知。在首页顶部的位置有个欢迎用户功能，此模块会根据用户登录的时间，人性化的对用户进行打招呼，比如用户深夜的时候登陆系统，该提示语会提醒“已经深夜了，你还在加班吗，请注意休息！”。当用户点击我的网盘模块后，系统首先会请求一次接口，展示自己网盘里面的文件，该用户可以对文件进行相关的操作。在分享模块中，用户可以选择不同的tab栏，分别对已共享、已接收的文件进行查看。当用户进入存储库模块时，单击不同的文档分类以查看已分类的文档，可以对文件进行查询，预览和下载。系统管理员发布通知后，系统前台会在系统右上角进行消息条数的提醒，点击消息红点后，会出现通知下拉列表框，再点击下拉列表里面的查看更多，可以进入更多模块下的系统公告列表页面，在该页面里面，用户可以通过标题关键字，公告发布的时间范围进行搜索，在更多模块下用户可以动态切换系统主题，然后让用户无感知的记录用户行为，当用户退出登录后重新登录，系统的主题还是用户退出登录时所选择的主题。  
管理员和超级管理员成功登入系统后台后，默认会调到Index页面去，在该首页，我们可以看到登录用户、服务器运行相关信息。在数据大盘模块，可以看到最近上传文件的数量，以及最近一段时间的上传曲线图。系统超级管理员可以管理系统所有的功能和所有用户，如果需要控制系统用户能访问的菜单，系统管理员只需更改相关角色所拥有的菜单列表。


![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/1.png)


#### 2.3 模块结构
基于SpringCloud+Hadoop+Vue企业网盘系统主要分为前台和后台两大模块，前台模块分为首页，网盘，分享，资源库，关注用户，系统公告模块，不同的功能模块拥有的功能也是不相同的。此外，所需权限也不同。后台模块分为用户、部门、角色、网盘、日志、系统监控、接口文档、定时任务模块。在网络磁盘管理模块中，管理员可以上传、删除和修改文档，管理员还可以在线查看多媒体资源，如Word文档、视频、音乐、图片。

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/2.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/3.png)


#### 2.4 内部微服务调用流程图
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/4.png)


---
## 三、系统架构
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)


数据库：20张表
```lua
1.sys_config: 系统配置信息表
2.sys_dept: 部门管理
3.sys_dict: 数据字典表
4.sys_disk: 企业网盘
5.sys_log: 系统日志
6.sys_menu: 菜单管理
7.sys_notice: 通知公告表
8.sys_oss: 文件上传
9.sys_role: 角色
10.sys_role_dept: 角色与部门对应关系
11.sys_role_menu: 角色与菜单对应关系
12.sys_user: 系统用户
13.sys_user_role: 用户与角色对应关系
14.schedule_job: 定时任务
15.schedule_job_log: 定时任务日志
16.tb_user_file: 用户与文件对应关系
17.tb_file: 文件
18.tb_disk_file: 企业共享网盘和文件对应关系
19.tb_follow: 关注用户表
20.tb_share: 分享表
```

---

## 四、系统展示(后台)
4.1 系统后台管理主界面
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/11.png)

4.2 系统后台添加用户
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/12.png)

4.3 系统后台修改部门
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/13.png)

4.4 系统后台修改角色
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/14.png)


4.5 系统后台企业网盘管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/15.png)

4.6 系统后台企业网盘管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/16.png)

4.7 系统后台菜单管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/17.png)

4.8 系统后台公告发布
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/18.png)


4.9 系统后台数据库监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/19.png)


4.10 系统后台Hadoop集群监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/20.png)

4.11 系统后台微服务监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/21.png)

---
## 五、系统展示(前台)
5.1 系统后台管理主界面
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

5.2 系统后台添加用户
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

5.3 系统后台修改部门
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

5.4 系统后台修改角色
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)


4.5 系统后台企业网盘管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

4.6 系统后台企业网盘管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

4.7 系统后台菜单管理
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

4.8 系统后台公告发布
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)


4.9 系统后台数据库监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)


4.10 系统后台Hadoop集群监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

4.11 系统后台微服务监控
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/5.png)

---






