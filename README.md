# 基于SpringCloud+Hadoop+Vue的企业级网盘系统设计与实现
### 【2019届毕业设计】，【优秀毕业设计】，【华东交通大学】 

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/0.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/00.png)

---

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
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/11.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/12.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/13.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/14.png)


![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/15.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/16.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/17.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/18.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/19.png)


![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/20.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/21.png)

---
## 五、系统展示(前台)
![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/31.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/32.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/33.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/34.png)


![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/35.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/36.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/37.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/38.png)


![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/39.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/40.png)

![img](https://raw.githubusercontent.com/chenxingxing6/cxx-graduation/master/img/41.png)

---

## 六、总结
通过这次设计，使我受益匪浅。在整个开发的过程中，将以前课堂上学到的知识用到了实践中，真正做到了理论与实际相结合。同时，对 Java web 面向对象程序设计语言有了很多了解。并且学习了SpringCloud微服务框架，HDFS分布式存储技术。是对以后到工作岗位，进行真正开发的一个实战演习。但是毕业设计也暴露出自己专业基础的很多不足。比如缺乏综合应用专业知识的能力，对专业基础知识不熟悉。需要在做的过程不断的翻阅相关资料和书籍、百度提问解决不懂得知识。这大大的降低了自己的速度和设计进度。因此，在今后的学习、工作中要尽量弥补自己的不足，大量阅读书籍，使自己不断地进步。

---
## DB
```sql
/*
Navicat MySQL Data Transfer

Source Server         : aliyun
Source Server Version : 50559
Source Host           : 60.205.212.196:3306
Source Database       : cloud_disk

Target Server Type    : MYSQL
Target Server Version : 50559
File Encoding         : 65001

Date: 2019-04-15 23:19:41
*/

SET FOREIGN_KEY_CHECKS=0;

-- ----------------------------
-- Table structure for schedule_job
-- ----------------------------
DROP TABLE IF EXISTS `schedule_job`;
CREATE TABLE `schedule_job` (
  `job_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '任务id',
  `bean_name` varchar(200) DEFAULT NULL COMMENT 'spring bean名称',
  `method_name` varchar(100) DEFAULT NULL COMMENT '方法名',
  `params` varchar(2000) DEFAULT NULL COMMENT '参数',
  `cron_expression` varchar(100) DEFAULT NULL COMMENT 'cron表达式',
  `status` tinyint(4) DEFAULT NULL COMMENT '任务状态  0：正常  1：暂停',
  `remark` varchar(255) DEFAULT NULL COMMENT '备注',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`job_id`)
) ENGINE=InnoDB AUTO_INCREMENT=16 DEFAULT CHARSET=utf8 COMMENT='定时任务';

-- ----------------------------
-- Records of schedule_job
-- ----------------------------
INSERT INTO `schedule_job` VALUES ('13', 'testTask', 'test1', 'aa', '*/5 * * * * ?', '0', '每隔5秒执行一次', '2019-03-17 18:17:45');
INSERT INTO `schedule_job` VALUES ('14', 'testTask', 'test2', null, '*/5 * * * * ?', '1', 'haha', '2019-03-17 18:20:47');

-- ----------------------------
-- Table structure for schedule_job_log
-- ----------------------------
DROP TABLE IF EXISTS `schedule_job_log`;
CREATE TABLE `schedule_job_log` (
  `log_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '任务日志id',
  `job_id` bigint(20) NOT NULL COMMENT '任务id',
  `bean_name` varchar(200) DEFAULT NULL COMMENT 'spring bean名称',
  `method_name` varchar(100) DEFAULT NULL COMMENT '方法名',
  `params` varchar(2000) DEFAULT NULL COMMENT '参数',
  `status` tinyint(4) NOT NULL COMMENT '任务状态    0：成功    1：失败',
  `error` varchar(2000) DEFAULT NULL COMMENT '失败信息',
  `times` int(11) NOT NULL COMMENT '耗时(单位：毫秒)',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`log_id`),
  KEY `job_id` (`job_id`)
) ENGINE=InnoDB AUTO_INCREMENT=273 DEFAULT CHARSET=utf8 COMMENT='定时任务日志';

-- ----------------------------
-- Records of schedule_job_log
-- ----------------------------
INSERT INTO `schedule_job_log` VALUES ('111', '13', 'testTask', 'test1', 'aa', '0', null, '2', '2019-03-17 18:17:55');
INSERT INTO `schedule_job_log` VALUES ('112', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 18:19:03');
INSERT INTO `schedule_job_log` VALUES ('113', '14', 'testTask', 'test1', null, '1', 'java.lang.NoSuchMethodException: com.example.modules.job.task.TestTask.test1()', '0', '2019-03-17 18:21:12');
INSERT INTO `schedule_job_log` VALUES ('114', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:21:30');
INSERT INTO `schedule_job_log` VALUES ('115', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:23:51');
INSERT INTO `schedule_job_log` VALUES ('116', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:24:55');
INSERT INTO `schedule_job_log` VALUES ('117', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:00');
INSERT INTO `schedule_job_log` VALUES ('118', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 18:25:05');
INSERT INTO `schedule_job_log` VALUES ('119', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:10');
INSERT INTO `schedule_job_log` VALUES ('120', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 18:25:15');
INSERT INTO `schedule_job_log` VALUES ('121', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:20');
INSERT INTO `schedule_job_log` VALUES ('122', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 18:25:25');
INSERT INTO `schedule_job_log` VALUES ('123', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:25');
INSERT INTO `schedule_job_log` VALUES ('124', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:30');
INSERT INTO `schedule_job_log` VALUES ('125', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 18:25:30');
INSERT INTO `schedule_job_log` VALUES ('126', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 18:25:35');
INSERT INTO `schedule_job_log` VALUES ('127', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 18:25:35');
INSERT INTO `schedule_job_log` VALUES ('128', '13', 'testTask', 'test1', 'aa', '0', null, '6', '2019-03-17 20:32:25');
INSERT INTO `schedule_job_log` VALUES ('129', '14', 'testTask', 'test2', null, '0', null, '6', '2019-03-17 20:32:25');
INSERT INTO `schedule_job_log` VALUES ('130', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:32:30');
INSERT INTO `schedule_job_log` VALUES ('131', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:32:30');
INSERT INTO `schedule_job_log` VALUES ('132', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:32:35');
INSERT INTO `schedule_job_log` VALUES ('133', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:32:35');
INSERT INTO `schedule_job_log` VALUES ('134', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:32:40');
INSERT INTO `schedule_job_log` VALUES ('135', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:32:40');
INSERT INTO `schedule_job_log` VALUES ('136', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:32:45');
INSERT INTO `schedule_job_log` VALUES ('137', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:32:45');
INSERT INTO `schedule_job_log` VALUES ('138', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:32:50');
INSERT INTO `schedule_job_log` VALUES ('139', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:32:50');
INSERT INTO `schedule_job_log` VALUES ('140', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:32:55');
INSERT INTO `schedule_job_log` VALUES ('141', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:32:55');
INSERT INTO `schedule_job_log` VALUES ('142', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:00');
INSERT INTO `schedule_job_log` VALUES ('143', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:00');
INSERT INTO `schedule_job_log` VALUES ('144', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:33:05');
INSERT INTO `schedule_job_log` VALUES ('145', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:33:05');
INSERT INTO `schedule_job_log` VALUES ('146', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:10');
INSERT INTO `schedule_job_log` VALUES ('147', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:10');
INSERT INTO `schedule_job_log` VALUES ('148', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:33:15');
INSERT INTO `schedule_job_log` VALUES ('149', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:33:15');
INSERT INTO `schedule_job_log` VALUES ('150', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:20');
INSERT INTO `schedule_job_log` VALUES ('151', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:20');
INSERT INTO `schedule_job_log` VALUES ('152', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:25');
INSERT INTO `schedule_job_log` VALUES ('153', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:25');
INSERT INTO `schedule_job_log` VALUES ('154', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:33:30');
INSERT INTO `schedule_job_log` VALUES ('155', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:30');
INSERT INTO `schedule_job_log` VALUES ('156', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:33:35');
INSERT INTO `schedule_job_log` VALUES ('157', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:35');
INSERT INTO `schedule_job_log` VALUES ('158', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:40');
INSERT INTO `schedule_job_log` VALUES ('159', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:40');
INSERT INTO `schedule_job_log` VALUES ('160', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:45');
INSERT INTO `schedule_job_log` VALUES ('161', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:45');
INSERT INTO `schedule_job_log` VALUES ('162', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:50');
INSERT INTO `schedule_job_log` VALUES ('163', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:50');
INSERT INTO `schedule_job_log` VALUES ('164', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:33:55');
INSERT INTO `schedule_job_log` VALUES ('165', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:33:55');
INSERT INTO `schedule_job_log` VALUES ('166', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:34:00');
INSERT INTO `schedule_job_log` VALUES ('167', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:00');
INSERT INTO `schedule_job_log` VALUES ('168', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:34:05');
INSERT INTO `schedule_job_log` VALUES ('169', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:34:05');
INSERT INTO `schedule_job_log` VALUES ('170', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:34:10');
INSERT INTO `schedule_job_log` VALUES ('171', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:10');
INSERT INTO `schedule_job_log` VALUES ('172', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:15');
INSERT INTO `schedule_job_log` VALUES ('173', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:34:15');
INSERT INTO `schedule_job_log` VALUES ('174', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:20');
INSERT INTO `schedule_job_log` VALUES ('175', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:34:20');
INSERT INTO `schedule_job_log` VALUES ('176', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:25');
INSERT INTO `schedule_job_log` VALUES ('177', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:34:25');
INSERT INTO `schedule_job_log` VALUES ('178', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:30');
INSERT INTO `schedule_job_log` VALUES ('179', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:34:30');
INSERT INTO `schedule_job_log` VALUES ('180', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:35');
INSERT INTO `schedule_job_log` VALUES ('181', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:35');
INSERT INTO `schedule_job_log` VALUES ('182', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:40');
INSERT INTO `schedule_job_log` VALUES ('183', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:40');
INSERT INTO `schedule_job_log` VALUES ('184', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:34:45');
INSERT INTO `schedule_job_log` VALUES ('185', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:45');
INSERT INTO `schedule_job_log` VALUES ('186', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:34:50');
INSERT INTO `schedule_job_log` VALUES ('187', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:50');
INSERT INTO `schedule_job_log` VALUES ('188', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:34:55');
INSERT INTO `schedule_job_log` VALUES ('189', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:34:55');
INSERT INTO `schedule_job_log` VALUES ('190', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:35:00');
INSERT INTO `schedule_job_log` VALUES ('191', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:00');
INSERT INTO `schedule_job_log` VALUES ('192', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:05');
INSERT INTO `schedule_job_log` VALUES ('193', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:35:05');
INSERT INTO `schedule_job_log` VALUES ('194', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:35:10');
INSERT INTO `schedule_job_log` VALUES ('195', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:10');
INSERT INTO `schedule_job_log` VALUES ('196', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:15');
INSERT INTO `schedule_job_log` VALUES ('197', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:35:15');
INSERT INTO `schedule_job_log` VALUES ('198', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:20');
INSERT INTO `schedule_job_log` VALUES ('199', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:35:20');
INSERT INTO `schedule_job_log` VALUES ('200', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:25');
INSERT INTO `schedule_job_log` VALUES ('201', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:35:25');
INSERT INTO `schedule_job_log` VALUES ('202', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:30');
INSERT INTO `schedule_job_log` VALUES ('203', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:35');
INSERT INTO `schedule_job_log` VALUES ('204', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:40');
INSERT INTO `schedule_job_log` VALUES ('205', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:45');
INSERT INTO `schedule_job_log` VALUES ('206', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:35:50');
INSERT INTO `schedule_job_log` VALUES ('207', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:35:55');
INSERT INTO `schedule_job_log` VALUES ('208', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:00');
INSERT INTO `schedule_job_log` VALUES ('209', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:05');
INSERT INTO `schedule_job_log` VALUES ('210', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:10');
INSERT INTO `schedule_job_log` VALUES ('211', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:15');
INSERT INTO `schedule_job_log` VALUES ('212', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:20');
INSERT INTO `schedule_job_log` VALUES ('213', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:25');
INSERT INTO `schedule_job_log` VALUES ('214', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:30');
INSERT INTO `schedule_job_log` VALUES ('215', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:35');
INSERT INTO `schedule_job_log` VALUES ('216', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:40');
INSERT INTO `schedule_job_log` VALUES ('217', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:45');
INSERT INTO `schedule_job_log` VALUES ('218', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:36:50');
INSERT INTO `schedule_job_log` VALUES ('219', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:36:55');
INSERT INTO `schedule_job_log` VALUES ('220', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:37:00');
INSERT INTO `schedule_job_log` VALUES ('221', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:05');
INSERT INTO `schedule_job_log` VALUES ('222', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:10');
INSERT INTO `schedule_job_log` VALUES ('223', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:37:15');
INSERT INTO `schedule_job_log` VALUES ('224', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:20');
INSERT INTO `schedule_job_log` VALUES ('225', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:37:25');
INSERT INTO `schedule_job_log` VALUES ('226', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:30');
INSERT INTO `schedule_job_log` VALUES ('227', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:37:35');
INSERT INTO `schedule_job_log` VALUES ('228', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:40');
INSERT INTO `schedule_job_log` VALUES ('229', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:45');
INSERT INTO `schedule_job_log` VALUES ('230', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:50');
INSERT INTO `schedule_job_log` VALUES ('231', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:37:55');
INSERT INTO `schedule_job_log` VALUES ('232', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:00');
INSERT INTO `schedule_job_log` VALUES ('233', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:05');
INSERT INTO `schedule_job_log` VALUES ('234', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:10');
INSERT INTO `schedule_job_log` VALUES ('235', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:15');
INSERT INTO `schedule_job_log` VALUES ('236', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:20');
INSERT INTO `schedule_job_log` VALUES ('237', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:25');
INSERT INTO `schedule_job_log` VALUES ('238', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:30');
INSERT INTO `schedule_job_log` VALUES ('239', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:35');
INSERT INTO `schedule_job_log` VALUES ('240', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:40');
INSERT INTO `schedule_job_log` VALUES ('241', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:38:45');
INSERT INTO `schedule_job_log` VALUES ('242', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:50');
INSERT INTO `schedule_job_log` VALUES ('243', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:38:55');
INSERT INTO `schedule_job_log` VALUES ('244', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:39:00');
INSERT INTO `schedule_job_log` VALUES ('245', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:39:05');
INSERT INTO `schedule_job_log` VALUES ('246', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:39:10');
INSERT INTO `schedule_job_log` VALUES ('247', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:39:15');
INSERT INTO `schedule_job_log` VALUES ('248', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:39:20');
INSERT INTO `schedule_job_log` VALUES ('249', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:39:25');
INSERT INTO `schedule_job_log` VALUES ('250', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:39:30');
INSERT INTO `schedule_job_log` VALUES ('251', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:39:35');
INSERT INTO `schedule_job_log` VALUES ('252', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:39:40');
INSERT INTO `schedule_job_log` VALUES ('253', '13', 'testTask', 'test1', 'aa', '0', null, '5', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('254', '14', 'testTask', 'test2', null, '0', null, '3', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('255', '13', 'testTask', 'test1', 'aa', '0', null, '5', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('256', '14', 'testTask', 'test2', null, '0', null, '6', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('257', '14', 'testTask', 'test2', null, '0', null, '4', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('258', '13', 'testTask', 'test1', 'aa', '0', null, '3', '2019-03-17 20:40:26');
INSERT INTO `schedule_job_log` VALUES ('259', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:40:30');
INSERT INTO `schedule_job_log` VALUES ('260', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:40:30');
INSERT INTO `schedule_job_log` VALUES ('261', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:40:35');
INSERT INTO `schedule_job_log` VALUES ('262', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:40:35');
INSERT INTO `schedule_job_log` VALUES ('263', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:40:40');
INSERT INTO `schedule_job_log` VALUES ('264', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:40:40');
INSERT INTO `schedule_job_log` VALUES ('265', '14', 'testTask', 'test2', null, '0', null, '0', '2019-03-17 20:40:45');
INSERT INTO `schedule_job_log` VALUES ('266', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:40:45');
INSERT INTO `schedule_job_log` VALUES ('267', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:40:50');
INSERT INTO `schedule_job_log` VALUES ('268', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:40:50');
INSERT INTO `schedule_job_log` VALUES ('269', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:40:55');
INSERT INTO `schedule_job_log` VALUES ('270', '13', 'testTask', 'test1', 'aa', '0', null, '0', '2019-03-17 20:40:55');
INSERT INTO `schedule_job_log` VALUES ('271', '14', 'testTask', 'test2', null, '0', null, '1', '2019-03-17 20:41:00');
INSERT INTO `schedule_job_log` VALUES ('272', '13', 'testTask', 'test1', 'aa', '0', null, '1', '2019-03-17 20:41:00');

-- ----------------------------
-- Table structure for sys_config
-- ----------------------------
DROP TABLE IF EXISTS `sys_config`;
CREATE TABLE `sys_config` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `param_key` varchar(50) DEFAULT NULL COMMENT 'key',
  `param_value` varchar(2000) DEFAULT NULL COMMENT 'value',
  `status` tinyint(4) DEFAULT '1' COMMENT '状态   0：隐藏   1：显示',
  `remark` varchar(500) DEFAULT NULL COMMENT '备注',
  PRIMARY KEY (`id`),
  UNIQUE KEY `param_key` (`param_key`)
) ENGINE=InnoDB AUTO_INCREMENT=3 DEFAULT CHARSET=utf8 COMMENT='系统配置信息表';

-- ----------------------------
-- Records of sys_config
-- ----------------------------
INSERT INTO `sys_config` VALUES ('1', 'CLOUD_STORAGE_CONFIG_KEY', '{\"type\":1,\"qiniuDomain\":\"http://ppkn5nh6t.bkt.clouddn.com\",\"qiniuPrefix\":\"upload\",\"qiniuAccessKey\":\"YLKWjJFNCjYHiVw6-E7RnqscoVfgiHpzqdBSn-HW\",\"qiniuSecretKey\":\"FpQmCJcePJ-HfGJHSAcf55O6di6yQ0FtrbNkdwyF\",\"qiniuBucketName\":\"disk\",\"aliyunDomain\":\"\",\"aliyunPrefix\":\"\",\"aliyunEndPoint\":\"\",\"aliyunAccessKeyId\":\"\",\"aliyunAccessKeySecret\":\"\",\"aliyunBucketName\":\"\",\"qcloudDomain\":\"\",\"qcloudPrefix\":\"\",\"qcloudSecretId\":\"\",\"qcloudSecretKey\":\"\",\"qcloudBucketName\":\"\"}', '1', '云存储配置信息');

-- ----------------------------
-- Table structure for sys_dept
-- ----------------------------
DROP TABLE IF EXISTS `sys_dept`;
CREATE TABLE `sys_dept` (
  `dept_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `parent_id` bigint(20) DEFAULT NULL COMMENT '上级部门ID，一级部门为0',
  `name` varchar(50) DEFAULT NULL COMMENT '部门名称',
  `order_num` int(11) DEFAULT NULL COMMENT '排序',
  `del_flag` tinyint(4) DEFAULT '0' COMMENT '是否删除  -1：已删除  0：正常',
  PRIMARY KEY (`dept_id`)
) ENGINE=InnoDB AUTO_INCREMENT=35 DEFAULT CHARSET=utf8 COMMENT='部门管理';

-- ----------------------------
-- Records of sys_dept
-- ----------------------------
INSERT INTO `sys_dept` VALUES ('1', '9', '普通用户', '0', '-1');
INSERT INTO `sys_dept` VALUES ('6', '9', '普通会员', '0', '-1');
INSERT INTO `sys_dept` VALUES ('7', '0', 'IT内部人员', '0', '-1');
INSERT INTO `sys_dept` VALUES ('8', '9', '超级会员', '0', '-1');
INSERT INTO `sys_dept` VALUES ('9', '34', '总裁室', '0', '0');
INSERT INTO `sys_dept` VALUES ('10', '34', '产品研发中心', '0', '0');
INSERT INTO `sys_dept` VALUES ('11', '34', '营销中心', '0', '0');
INSERT INTO `sys_dept` VALUES ('12', '34', '金融事业中心', '0', '0');
INSERT INTO `sys_dept` VALUES ('13', '34', '创新事业中心', '0', '0');
INSERT INTO `sys_dept` VALUES ('14', '10', '平台架构部', '0', '0');
INSERT INTO `sys_dept` VALUES ('15', '10', '基础产品技术部', '0', '0');
INSERT INTO `sys_dept` VALUES ('16', '10', '开放平台技术部', '0', '0');
INSERT INTO `sys_dept` VALUES ('17', '10', '项目管理部', '0', '0');
INSERT INTO `sys_dept` VALUES ('18', '11', '运营支持部', '0', '0');
INSERT INTO `sys_dept` VALUES ('19', '11', '工程实施部', '0', '0');
INSERT INTO `sys_dept` VALUES ('20', '11', '直销业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('21', '11', '商家代运营', '0', '0');
INSERT INTO `sys_dept` VALUES ('22', '12', '数据技术部', '0', '0');
INSERT INTO `sys_dept` VALUES ('23', '12', '平台金融部', '0', '0');
INSERT INTO `sys_dept` VALUES ('24', '12', '数字金融', '0', '0');
INSERT INTO `sys_dept` VALUES ('25', '12', '国际业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('26', '13', '智慧商圈业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('27', '13', '智慧小店业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('28', '13', '新零售', '0', '0');
INSERT INTO `sys_dept` VALUES ('29', '13', '智慧门店业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('30', '13', '智慧园区业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('31', '13', '行业合作部', '0', '0');
INSERT INTO `sys_dept` VALUES ('32', '13', '线上销售部', '0', '0');
INSERT INTO `sys_dept` VALUES ('33', '13', '分销业务部', '0', '0');
INSERT INTO `sys_dept` VALUES ('34', '0', '杭州二维火科技有限公司', '0', '0');

-- ----------------------------
-- Table structure for sys_dict
-- ----------------------------
DROP TABLE IF EXISTS `sys_dict`;
CREATE TABLE `sys_dict` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `name` varchar(100) NOT NULL COMMENT '字典名称',
  `type` varchar(100) NOT NULL COMMENT '字典类型',
  `code` varchar(100) NOT NULL COMMENT '字典码',
  `value` varchar(1000) NOT NULL COMMENT '字典值',
  `order_num` int(11) DEFAULT '0' COMMENT '排序',
  `remark` varchar(255) DEFAULT NULL COMMENT '备注',
  `del_flag` tinyint(4) DEFAULT '0' COMMENT '删除标记  -1：已删除  0：正常',
  PRIMARY KEY (`id`),
  UNIQUE KEY `type` (`type`,`code`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8 COMMENT='数据字典表';

-- ----------------------------
-- Records of sys_dict
-- ----------------------------
INSERT INTO `sys_dict` VALUES ('1', '性别', 'sex', '0', '女', '0', null, '0');
INSERT INTO `sys_dict` VALUES ('2', '性别', 'sex', '1', '男', '1', null, '0');
INSERT INTO `sys_dict` VALUES ('3', '性别', 'sex', '2', '未知', '3', null, '0');

-- ----------------------------
-- Table structure for sys_disk
-- ----------------------------
DROP TABLE IF EXISTS `sys_disk`;
CREATE TABLE `sys_disk` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `company_name` varchar(200) DEFAULT NULL COMMENT '企业名字',
  `company_id` bigint(20) NOT NULL COMMENT '企业ID,dept_id',
  `name` varchar(100) DEFAULT NULL COMMENT '文件名',
  `is_valid` tinyint(4) NOT NULL DEFAULT '1' COMMENT '是否有效',
  `create_user` varchar(32) DEFAULT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8 COMMENT='企业网盘目录';

-- ----------------------------
-- Records of sys_disk
-- ----------------------------
INSERT INTO `sys_disk` VALUES ('1', '杭州二维火科技有限公司', '34', '文件', '1', '1', '1554218919971');
INSERT INTO `sys_disk` VALUES ('2', '杭州二维火科技有限公司', '34', '图片', '1', '1', '1554221258564');
INSERT INTO `sys_disk` VALUES ('3', '杭州二维火科技有限公司', '34', '视频', '1', '1', '1554222667625');
INSERT INTO `sys_disk` VALUES ('4', '杭州二维火科技有限公司', '34', '音乐', '1', '1', '1554222674617');
INSERT INTO `sys_disk` VALUES ('5', '杭州二维火科技有限公司', '34', '文档', '1', '1', '1554222680995');

-- ----------------------------
-- Table structure for sys_log
-- ----------------------------
DROP TABLE IF EXISTS `sys_log`;
CREATE TABLE `sys_log` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) DEFAULT NULL COMMENT '用户名',
  `operation` varchar(50) DEFAULT NULL COMMENT '用户操作',
  `method` varchar(200) DEFAULT NULL COMMENT '请求方法',
  `params` varchar(5000) DEFAULT NULL COMMENT '请求参数',
  `time` bigint(20) NOT NULL COMMENT '执行时长(毫秒)',
  `ip` varchar(64) DEFAULT NULL COMMENT 'IP地址',
  `create_date` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=647 DEFAULT CHARSET=utf8 COMMENT='系统日志';

-- ----------------------------
-- Records of sys_log
-- ----------------------------
INSERT INTO `sys_log` VALUES ('601', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '5392', '0:0:0:0:0:0:0:1', '2019-04-12 12:39:19');
INSERT INTO `sys_log` VALUES ('602', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '74', '0:0:0:0:0:0:0:1', '2019-04-12 12:48:17');
INSERT INTO `sys_log` VALUES ('603', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '85', '0:0:0:0:0:0:0:1', '2019-04-12 12:55:16');
INSERT INTO `sys_log` VALUES ('604', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '5371', '0:0:0:0:0:0:0:1', '2019-04-12 15:29:19');
INSERT INTO `sys_log` VALUES ('605', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-12 15:30:18');
INSERT INTO `sys_log` VALUES ('606', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '5398', '0:0:0:0:0:0:0:1', '2019-04-13 13:10:53');
INSERT INTO `sys_log` VALUES ('607', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '84', '34', '0:0:0:0:0:0:0:1', '2019-04-13 13:12:47');
INSERT INTO `sys_log` VALUES ('608', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '88', '218', '0:0:0:0:0:0:0:1', '2019-04-13 13:12:56');
INSERT INTO `sys_log` VALUES ('609', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '87', '205', '0:0:0:0:0:0:0:1', '2019-04-13 13:13:11');
INSERT INTO `sys_log` VALUES ('610', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '86', '203', '0:0:0:0:0:0:0:1', '2019-04-13 13:13:23');
INSERT INTO `sys_log` VALUES ('611', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '85', '204', '0:0:0:0:0:0:0:1', '2019-04-13 13:13:37');
INSERT INTO `sys_log` VALUES ('612', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '84', '204', '0:0:0:0:0:0:0:1', '2019-04-13 13:13:46');
INSERT INTO `sys_log` VALUES ('613', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '33', '0:0:0:0:0:0:0:1', '2019-04-13 13:13:54');
INSERT INTO `sys_log` VALUES ('614', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '78', '190', '0:0:0:0:0:0:0:1', '2019-04-13 13:14:24');
INSERT INTO `sys_log` VALUES ('615', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '77', '174', '0:0:0:0:0:0:0:1', '2019-04-13 13:14:36');
INSERT INTO `sys_log` VALUES ('616', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '70', '174', '0:0:0:0:0:0:0:1', '2019-04-13 13:14:46');
INSERT INTO `sys_log` VALUES ('617', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '33', '0:0:0:0:0:0:0:1', '2019-04-13 13:15:28');
INSERT INTO `sys_log` VALUES ('618', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '33', '0:0:0:0:0:0:0:1', '2019-04-13 13:15:28');
INSERT INTO `sys_log` VALUES ('619', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-13 13:15:52');
INSERT INTO `sys_log` VALUES ('620', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-13 13:15:53');
INSERT INTO `sys_log` VALUES ('621', 'admin', '删除菜单', 'com.example.modules.sys.controller.SysMenuController.delete()', '57', '172', '0:0:0:0:0:0:0:1', '2019-04-13 13:19:45');
INSERT INTO `sys_log` VALUES ('622', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-13 13:19:52');
INSERT INTO `sys_log` VALUES ('623', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-13 13:20:07');
INSERT INTO `sys_log` VALUES ('624', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '33', '0:0:0:0:0:0:0:1', '2019-04-13 13:20:08');
INSERT INTO `sys_log` VALUES ('625', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '5360', '0:0:0:0:0:0:0:1', '2019-04-13 13:21:13');
INSERT INTO `sys_log` VALUES ('626', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '5378', '0:0:0:0:0:0:0:1', '2019-04-13 16:39:00');
INSERT INTO `sys_log` VALUES ('627', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '93', '0:0:0:0:0:0:0:1', '2019-04-13 17:32:24');
INSERT INTO `sys_log` VALUES ('628', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '116', '0:0:0:0:0:0:0:1', '2019-04-13 22:02:12');
INSERT INTO `sys_log` VALUES ('629', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '47', '0:0:0:0:0:0:0:1', '2019-04-14 13:11:01');
INSERT INTO `sys_log` VALUES ('630', 'admin', '保存用户', 'com.example.modules.front.controller.AppUserController.save()', '{\"userId\":6,\"username\":\"front1\",\"password\":\"123456\",\"email\":\"front1@qq.com\",\"mobile\":\"18379643981\",\"status\":1,\"type\":1,\"createTime\":\"Apr 14, 2019 1:11:38 PM\",\"deptId\":26,\"deptName\":\"智慧商圈业务部\"}', '216', '0:0:0:0:0:0:0:1', '2019-04-14 13:11:39');
INSERT INTO `sys_log` VALUES ('631', 'admin', '修改用户', 'com.example.modules.front.controller.AppUserController.update()', '{\"userId\":4,\"username\":\"front\",\"imgPath\":\"https://static.vilson.xyz/cover.png\",\"salt\":\"\",\"email\":\"front@qq.com\",\"mobile\":\"18379643980\",\"status\":1,\"type\":1,\"createTime\":\"Dec 30, 2018 10:45:24 PM\",\"deptId\":13,\"deptName\":\"创新事业中心\"}', '129', '0:0:0:0:0:0:0:1', '2019-04-14 13:11:50');
INSERT INTO `sys_log` VALUES ('632', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '37', '0:0:0:0:0:0:0:1', '2019-04-14 13:13:30');
INSERT INTO `sys_log` VALUES ('633', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '110', '0:0:0:0:0:0:0:1', '2019-04-14 14:02:48');
INSERT INTO `sys_log` VALUES ('634', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '108', '0:0:0:0:0:0:0:1', '2019-04-14 22:10:03');
INSERT INTO `sys_log` VALUES ('635', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '35', '0:0:0:0:0:0:0:1', '2019-04-14 22:12:24');
INSERT INTO `sys_log` VALUES ('636', 'admin', '恢复定时任务', 'com.example.modules.job.controller.ScheduleJobController.resume()', '[13]', '116', '0:0:0:0:0:0:0:1', '2019-04-14 22:32:59');
INSERT INTO `sys_log` VALUES ('637', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-14 22:44:26');
INSERT INTO `sys_log` VALUES ('638', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:01');
INSERT INTO `sys_log` VALUES ('639', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:08');
INSERT INTO `sys_log` VALUES ('640', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:08');
INSERT INTO `sys_log` VALUES ('641', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:11');
INSERT INTO `sys_log` VALUES ('642', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:11');
INSERT INTO `sys_log` VALUES ('643', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '34', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:16');
INSERT INTO `sys_log` VALUES ('644', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-14 22:46:18');
INSERT INTO `sys_log` VALUES ('645', 'admin', '获取首页信息', 'com.example.modules.sys.controller.SysServerController.getIndexInfo()', null, '107', '0:0:0:0:0:0:0:1', '2019-04-14 22:47:22');
INSERT INTO `sys_log` VALUES ('646', 'admin', '获取服务器信息', 'com.example.modules.sys.controller.SysServerController.getInfo()', null, '0', '0:0:0:0:0:0:0:1', '2019-04-14 22:47:25');

-- ----------------------------
-- Table structure for sys_menu
-- ----------------------------
DROP TABLE IF EXISTS `sys_menu`;
CREATE TABLE `sys_menu` (
  `menu_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `parent_id` bigint(20) DEFAULT NULL COMMENT '父菜单ID，一级菜单为0',
  `name` varchar(50) DEFAULT NULL COMMENT '菜单名称',
  `url` varchar(200) DEFAULT NULL COMMENT '菜单URL',
  `perms` varchar(500) DEFAULT NULL COMMENT '授权(多个用逗号分隔，如：user:list,user:create)',
  `type` int(11) DEFAULT NULL COMMENT '类型   0：目录   1：菜单   2：按钮',
  `icon` varchar(50) DEFAULT NULL COMMENT '菜单图标',
  `order_num` int(11) DEFAULT NULL COMMENT '排序',
  PRIMARY KEY (`menu_id`)
) ENGINE=InnoDB AUTO_INCREMENT=105 DEFAULT CHARSET=utf8 COMMENT='菜单管理';

-- ----------------------------
-- Records of sys_menu
-- ----------------------------
INSERT INTO `sys_menu` VALUES ('1', '0', '系统管理', null, null, '0', 'fa fa-cog', '3');
INSERT INTO `sys_menu` VALUES ('2', '49', '后台用户', 'modules/sys/user.html', null, '1', 'fa fa-user', '1');
INSERT INTO `sys_menu` VALUES ('3', '54', '用户角色', 'modules/sys/role.html', null, '1', 'fa fa-user-secret', '2');
INSERT INTO `sys_menu` VALUES ('4', '1', '菜单管理', 'modules/sys/menu.html', null, '1', 'fa fa-th-list', '3');
INSERT INTO `sys_menu` VALUES ('5', '55', 'SQL监控', 'druid/sql.html', null, '1', 'fa fa-bug', '0');
INSERT INTO `sys_menu` VALUES ('6', '1', '定时任务', 'modules/job/schedule.html', null, '1', 'fa fa-tasks', '5');
INSERT INTO `sys_menu` VALUES ('7', '6', '查看', null, 'sys:schedule:list,sys:schedule:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('8', '6', '新增', null, 'sys:schedule:save', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('9', '6', '修改', null, 'sys:schedule:update', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('10', '6', '删除', null, 'sys:schedule:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('11', '6', '暂停', null, 'sys:schedule:pause', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('12', '6', '恢复', null, 'sys:schedule:resume', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('13', '6', '立即执行', null, 'sys:schedule:run', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('14', '6', '日志列表', null, 'sys:schedule:log', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('15', '2', '查看', null, 'sys:user:list,sys:user:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('16', '2', '新增', null, 'sys:user:save,sys:role:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('17', '2', '修改', null, 'sys:user:update,sys:role:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('18', '2', '删除', null, 'sys:user:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('19', '3', '查看', null, 'sys:role:list,sys:role:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('20', '3', '新增', null, 'sys:role:save,sys:menu:perms', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('21', '3', '修改', null, 'sys:role:update,sys:menu:perms', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('22', '3', '删除', null, 'sys:role:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('23', '4', '查看', null, 'sys:menu:list,sys:menu:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('24', '4', '新增', null, 'sys:menu:save,sys:menu:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('25', '4', '修改', null, 'sys:menu:update,sys:menu:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('26', '4', '删除', null, 'sys:menu:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('27', '1', '参数管理', 'modules/sys/config.html', 'sys:config:list,sys:config:info,sys:config:save,sys:config:update,sys:config:delete', '1', 'fa fa-sun-o', '6');
INSERT INTO `sys_menu` VALUES ('29', '50', '系统日志', 'modules/sys/log.html', 'sys:log:list', '1', 'fa fa-file-text-o', '7');
INSERT INTO `sys_menu` VALUES ('30', '1', '文件上传', 'modules/oss/oss.html', 'sys:oss:all', '1', 'fa fa-file-image-o', '6');
INSERT INTO `sys_menu` VALUES ('31', '53', '部门管理', 'modules/sys/dept.html', null, '1', 'fa fa-file-code-o', '1');
INSERT INTO `sys_menu` VALUES ('32', '31', '查看', null, 'sys:dept:list,sys:dept:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('33', '31', '新增', null, 'sys:dept:save,sys:dept:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('34', '31', '修改', null, 'sys:dept:update,sys:dept:select', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('35', '31', '删除', null, 'sys:dept:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('36', '1', '字典管理', 'modules/sys/dict.html', null, '1', 'fa fa-bookmark-o', '6');
INSERT INTO `sys_menu` VALUES ('37', '36', '查看', null, 'sys:dict:list,sys:dict:info', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('38', '36', '新增', null, 'sys:dict:save', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('39', '36', '修改', null, 'sys:dict:update', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('40', '36', '删除', null, 'sys:dict:delete', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('41', '0', '其他管理', null, null, '0', 'fa fa-cog', '3');
INSERT INTO `sys_menu` VALUES ('43', '0', '网盘管理', null, null, '0', 'fa fa-cog', '2');
INSERT INTO `sys_menu` VALUES ('49', '0', '用户管理', null, null, '0', 'fa fa-user', '1');
INSERT INTO `sys_menu` VALUES ('50', '0', '日志管理', null, null, '0', 'fa fa-file-text-o', '2');
INSERT INTO `sys_menu` VALUES ('51', '41', '接口文档', '/swagger/index.html', null, '1', 'fa fa-file', '0');
INSERT INTO `sys_menu` VALUES ('52', '0', '数据大盘', 'main.html', null, '1', 'fa fa-tachometer', '0');
INSERT INTO `sys_menu` VALUES ('53', '0', '部门管理', null, null, '0', 'fa fa-id-card-o', '1');
INSERT INTO `sys_menu` VALUES ('54', '0', '角色管理', null, null, '0', 'fa fa-user-secret', '1');
INSERT INTO `sys_menu` VALUES ('55', '0', '系统监控', null, null, '0', 'fa fa-bar-chart', '3');
INSERT INTO `sys_menu` VALUES ('56', '55', 'Hadoop监控', 'hadoop.html', null, '1', 'fa fa-eye', '0');
INSERT INTO `sys_menu` VALUES ('58', '49', '前台用户', 'modules/front/user.html', null, '1', 'fa fa-user', '0');
INSERT INTO `sys_menu` VALUES ('59', '58', '查询', null, 'front:user:list,front:user:info', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('60', '58', '新增', null, 'front:user:save', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('61', '58', '修改', null, 'front:user:update', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('62', '58', '删除', null, '', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('63', '29', '清除', null, 'sys:log:delete', '2', null, '0');
INSERT INTO `sys_menu` VALUES ('89', '55', 'Eureka注册中心', 'http://localhost:8761/', null, '1', null, '0');
INSERT INTO `sys_menu` VALUES ('90', '55', '服务监控', 'http://localhost:9010', null, '1', null, '0');
INSERT INTO `sys_menu` VALUES ('91', '41', '文件预览', 'http://193.112.27.123:8012/index', null, '1', null, '0');
INSERT INTO `sys_menu` VALUES ('92', '43', '企业网盘', 'modules/front/disk.html', null, '1', null, '0');
INSERT INTO `sys_menu` VALUES ('93', '55', '服务器连接', 'http://193.112.27.123:2222/ssh/host/193.112.27.123', null, '1', 'fa fa-link', '0');
INSERT INTO `sys_menu` VALUES ('94', '55', '服务器监控', 'modules/sys/server.html', null, '1', 'fa fa-video-camera', '0');
INSERT INTO `sys_menu` VALUES ('99', '95', '删除', '', 'front:sysnotice:delete', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('100', '1', '通知公告', 'modules/sys/sysnotice.html', null, '1', 'fa fa-file-code-o', '6');
INSERT INTO `sys_menu` VALUES ('101', '100', '查看', null, 'sys:sysnotice:list,sys:sysnotice:info', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('102', '100', '新增', null, 'sys:sysnotice:save', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('103', '100', '修改', null, 'sys:sysnotice:update', '2', null, '6');
INSERT INTO `sys_menu` VALUES ('104', '100', '删除', null, 'sys:sysnotice:delete', '2', null, '6');

-- ----------------------------
-- Table structure for sys_notice
-- ----------------------------
DROP TABLE IF EXISTS `sys_notice`;
CREATE TABLE `sys_notice` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '公告ID',
  `notice_title` varchar(100) NOT NULL COMMENT '公告标题',
  `notice_type` tinyint(4) NOT NULL COMMENT '公告类型（1通知 2公告）',
  `notice_content` varchar(500) NOT NULL COMMENT '公告内容',
  `status` tinyint(1) DEFAULT '0' COMMENT '公告状态（0正常 1关闭）',
  `create_user` varchar(32) NOT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  `op_user` varchar(32) DEFAULT NULL COMMENT '更新者',
  `op_time` bigint(20) DEFAULT NULL COMMENT '更新时间',
  `last_ver` smallint(6) NOT NULL DEFAULT '0' COMMENT '版本号',
  `remark` varchar(255) DEFAULT '' COMMENT '备注',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8 COMMENT='通知公告表';

-- ----------------------------
-- Records of sys_notice
-- ----------------------------
INSERT INTO `sys_notice` VALUES ('3', '有奖征文|程序员/媛 恋爱、结婚这件小事', '2', '春暖花开，芬芳四溢，CSDN博客特举行“程序员（媛）恋爱/结婚”为主题的征文活动，大声说出你们的爱', '0', '1', '1554597292431', '1', '1555148028368', '0', '');
INSERT INTO `sys_notice` VALUES ('6', '你为什么还不努力？', '2', '你比他好一点，他不会承认你，反而会嫉妒你，只有你比他好很多，他才会承认你，然后还会很崇拜你，所以要做，就一定要比别人做得好很多!', '0', '1', '1555044026091', '1', '1555148120134', '0', '');

-- ----------------------------
-- Table structure for sys_oss
-- ----------------------------
DROP TABLE IF EXISTS `sys_oss`;
CREATE TABLE `sys_oss` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `url` varchar(200) DEFAULT NULL COMMENT 'URL地址',
  `create_date` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=17 DEFAULT CHARSET=utf8 COMMENT='文件上传';

-- ----------------------------
-- Records of sys_oss
-- ----------------------------
INSERT INTO `sys_oss` VALUES ('6', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190407/66820b363a2640b9a952d82373c38988.png', '2019-04-07 11:38:18');
INSERT INTO `sys_oss` VALUES ('7', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190410/dbf66652effa4b309d98b00946043690.jpeg', '2019-04-10 19:20:36');
INSERT INTO `sys_oss` VALUES ('8', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190413/5698ed795d334ca5b57d2f5cc0e6d04d.jpeg', '2019-04-13 16:39:04');
INSERT INTO `sys_oss` VALUES ('10', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190413/fe9a2bfe649748dbbe36706dd75afc31.jpeg', '2019-04-13 16:39:29');
INSERT INTO `sys_oss` VALUES ('11', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/8a0b1492de1f42db976ad3dd516c12fb.jpeg', '2019-04-14 12:15:27');
INSERT INTO `sys_oss` VALUES ('12', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/48399b28525f477c9e47aed619a1d5d6.jpeg', '2019-04-14 12:18:06');
INSERT INTO `sys_oss` VALUES ('13', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/cb3fa17ecd8546689e939362616a4542.jpeg', '2019-04-14 12:21:03');
INSERT INTO `sys_oss` VALUES ('14', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/0ba138fa34784d7c87c0221a68fc58b4.jpeg', '2019-04-14 12:22:04');
INSERT INTO `sys_oss` VALUES ('15', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/66c0519c70f74ddebea2c47142836b86.jpeg', '2019-04-14 12:22:29');
INSERT INTO `sys_oss` VALUES ('16', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/d7bb19a0f02b4d65b28959a896ad8111.jpeg', '2019-04-14 13:13:22');

-- ----------------------------
-- Table structure for sys_role
-- ----------------------------
DROP TABLE IF EXISTS `sys_role`;
CREATE TABLE `sys_role` (
  `role_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `role_name` varchar(100) DEFAULT NULL COMMENT '角色名称',
  `remark` varchar(100) DEFAULT NULL COMMENT '备注',
  `dept_id` bigint(20) DEFAULT NULL COMMENT '部门ID',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`role_id`)
) ENGINE=InnoDB AUTO_INCREMENT=4 DEFAULT CHARSET=utf8 COMMENT='角色';

-- ----------------------------
-- Records of sys_role
-- ----------------------------
INSERT INTO `sys_role` VALUES ('1', '超级管理员', '最高权限', '34', '2018-07-31 19:27:42');
INSERT INTO `sys_role` VALUES ('2', '管理员', '权限比较少', '9', '2018-07-31 19:28:58');
INSERT INTO `sys_role` VALUES ('3', 'IT经理', 'IT用户使用', '34', '2018-12-30 22:42:15');

-- ----------------------------
-- Table structure for sys_role_dept
-- ----------------------------
DROP TABLE IF EXISTS `sys_role_dept`;
CREATE TABLE `sys_role_dept` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `role_id` bigint(20) DEFAULT NULL COMMENT '角色ID',
  `dept_id` bigint(20) DEFAULT NULL COMMENT '部门ID',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=79 DEFAULT CHARSET=utf8 COMMENT='角色与部门对应关系';

-- ----------------------------
-- Records of sys_role_dept
-- ----------------------------
INSERT INTO `sys_role_dept` VALUES ('54', '1', '34');
INSERT INTO `sys_role_dept` VALUES ('55', '1', '9');
INSERT INTO `sys_role_dept` VALUES ('56', '1', '10');
INSERT INTO `sys_role_dept` VALUES ('57', '1', '11');
INSERT INTO `sys_role_dept` VALUES ('58', '1', '12');
INSERT INTO `sys_role_dept` VALUES ('59', '1', '13');
INSERT INTO `sys_role_dept` VALUES ('70', '3', '34');
INSERT INTO `sys_role_dept` VALUES ('71', '3', '9');
INSERT INTO `sys_role_dept` VALUES ('72', '3', '10');
INSERT INTO `sys_role_dept` VALUES ('73', '3', '14');
INSERT INTO `sys_role_dept` VALUES ('74', '3', '11');
INSERT INTO `sys_role_dept` VALUES ('75', '3', '12');
INSERT INTO `sys_role_dept` VALUES ('76', '3', '13');
INSERT INTO `sys_role_dept` VALUES ('78', '2', '34');

-- ----------------------------
-- Table structure for sys_role_menu
-- ----------------------------
DROP TABLE IF EXISTS `sys_role_menu`;
CREATE TABLE `sys_role_menu` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `role_id` bigint(20) DEFAULT NULL COMMENT '角色ID',
  `menu_id` bigint(20) DEFAULT NULL COMMENT '菜单ID',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=1499 DEFAULT CHARSET=utf8 COMMENT='角色与菜单对应关系';

-- ----------------------------
-- Records of sys_role_menu
-- ----------------------------
INSERT INTO `sys_role_menu` VALUES ('1073', '1', '1');
INSERT INTO `sys_role_menu` VALUES ('1074', '1', '4');
INSERT INTO `sys_role_menu` VALUES ('1075', '1', '23');
INSERT INTO `sys_role_menu` VALUES ('1076', '1', '24');
INSERT INTO `sys_role_menu` VALUES ('1077', '1', '25');
INSERT INTO `sys_role_menu` VALUES ('1078', '1', '26');
INSERT INTO `sys_role_menu` VALUES ('1079', '1', '6');
INSERT INTO `sys_role_menu` VALUES ('1080', '1', '7');
INSERT INTO `sys_role_menu` VALUES ('1081', '1', '8');
INSERT INTO `sys_role_menu` VALUES ('1082', '1', '9');
INSERT INTO `sys_role_menu` VALUES ('1083', '1', '10');
INSERT INTO `sys_role_menu` VALUES ('1084', '1', '11');
INSERT INTO `sys_role_menu` VALUES ('1085', '1', '12');
INSERT INTO `sys_role_menu` VALUES ('1086', '1', '13');
INSERT INTO `sys_role_menu` VALUES ('1087', '1', '14');
INSERT INTO `sys_role_menu` VALUES ('1088', '1', '27');
INSERT INTO `sys_role_menu` VALUES ('1089', '1', '30');
INSERT INTO `sys_role_menu` VALUES ('1090', '1', '36');
INSERT INTO `sys_role_menu` VALUES ('1091', '1', '37');
INSERT INTO `sys_role_menu` VALUES ('1092', '1', '38');
INSERT INTO `sys_role_menu` VALUES ('1093', '1', '39');
INSERT INTO `sys_role_menu` VALUES ('1094', '1', '40');
INSERT INTO `sys_role_menu` VALUES ('1095', '1', '41');
INSERT INTO `sys_role_menu` VALUES ('1096', '1', '51');
INSERT INTO `sys_role_menu` VALUES ('1097', '1', '91');
INSERT INTO `sys_role_menu` VALUES ('1098', '1', '43');
INSERT INTO `sys_role_menu` VALUES ('1099', '1', '64');
INSERT INTO `sys_role_menu` VALUES ('1100', '1', '65');
INSERT INTO `sys_role_menu` VALUES ('1101', '1', '66');
INSERT INTO `sys_role_menu` VALUES ('1102', '1', '67');
INSERT INTO `sys_role_menu` VALUES ('1103', '1', '68');
INSERT INTO `sys_role_menu` VALUES ('1104', '1', '69');
INSERT INTO `sys_role_menu` VALUES ('1106', '1', '71');
INSERT INTO `sys_role_menu` VALUES ('1107', '1', '72');
INSERT INTO `sys_role_menu` VALUES ('1108', '1', '73');
INSERT INTO `sys_role_menu` VALUES ('1109', '1', '74');
INSERT INTO `sys_role_menu` VALUES ('1110', '1', '75');
INSERT INTO `sys_role_menu` VALUES ('1111', '1', '76');
INSERT INTO `sys_role_menu` VALUES ('1119', '1', '92');
INSERT INTO `sys_role_menu` VALUES ('1120', '1', '49');
INSERT INTO `sys_role_menu` VALUES ('1121', '1', '2');
INSERT INTO `sys_role_menu` VALUES ('1122', '1', '15');
INSERT INTO `sys_role_menu` VALUES ('1123', '1', '16');
INSERT INTO `sys_role_menu` VALUES ('1124', '1', '17');
INSERT INTO `sys_role_menu` VALUES ('1125', '1', '18');
INSERT INTO `sys_role_menu` VALUES ('1126', '1', '58');
INSERT INTO `sys_role_menu` VALUES ('1127', '1', '59');
INSERT INTO `sys_role_menu` VALUES ('1128', '1', '60');
INSERT INTO `sys_role_menu` VALUES ('1129', '1', '61');
INSERT INTO `sys_role_menu` VALUES ('1130', '1', '50');
INSERT INTO `sys_role_menu` VALUES ('1131', '1', '29');
INSERT INTO `sys_role_menu` VALUES ('1132', '1', '63');
INSERT INTO `sys_role_menu` VALUES ('1133', '1', '52');
INSERT INTO `sys_role_menu` VALUES ('1134', '1', '53');
INSERT INTO `sys_role_menu` VALUES ('1135', '1', '31');
INSERT INTO `sys_role_menu` VALUES ('1136', '1', '32');
INSERT INTO `sys_role_menu` VALUES ('1137', '1', '33');
INSERT INTO `sys_role_menu` VALUES ('1138', '1', '34');
INSERT INTO `sys_role_menu` VALUES ('1139', '1', '35');
INSERT INTO `sys_role_menu` VALUES ('1140', '1', '54');
INSERT INTO `sys_role_menu` VALUES ('1141', '1', '3');
INSERT INTO `sys_role_menu` VALUES ('1142', '1', '19');
INSERT INTO `sys_role_menu` VALUES ('1143', '1', '20');
INSERT INTO `sys_role_menu` VALUES ('1144', '1', '21');
INSERT INTO `sys_role_menu` VALUES ('1145', '1', '22');
INSERT INTO `sys_role_menu` VALUES ('1146', '1', '55');
INSERT INTO `sys_role_menu` VALUES ('1147', '1', '5');
INSERT INTO `sys_role_menu` VALUES ('1148', '1', '56');
INSERT INTO `sys_role_menu` VALUES ('1150', '1', '89');
INSERT INTO `sys_role_menu` VALUES ('1151', '1', '90');
INSERT INTO `sys_role_menu` VALUES ('1325', '3', '1');
INSERT INTO `sys_role_menu` VALUES ('1326', '3', '27');
INSERT INTO `sys_role_menu` VALUES ('1327', '3', '30');
INSERT INTO `sys_role_menu` VALUES ('1328', '3', '43');
INSERT INTO `sys_role_menu` VALUES ('1329', '3', '64');
INSERT INTO `sys_role_menu` VALUES ('1330', '3', '65');
INSERT INTO `sys_role_menu` VALUES ('1331', '3', '66');
INSERT INTO `sys_role_menu` VALUES ('1332', '3', '67');
INSERT INTO `sys_role_menu` VALUES ('1333', '3', '68');
INSERT INTO `sys_role_menu` VALUES ('1334', '3', '69');
INSERT INTO `sys_role_menu` VALUES ('1336', '3', '71');
INSERT INTO `sys_role_menu` VALUES ('1337', '3', '72');
INSERT INTO `sys_role_menu` VALUES ('1338', '3', '73');
INSERT INTO `sys_role_menu` VALUES ('1339', '3', '74');
INSERT INTO `sys_role_menu` VALUES ('1340', '3', '75');
INSERT INTO `sys_role_menu` VALUES ('1341', '3', '76');
INSERT INTO `sys_role_menu` VALUES ('1349', '3', '92');
INSERT INTO `sys_role_menu` VALUES ('1350', '3', '29');
INSERT INTO `sys_role_menu` VALUES ('1351', '3', '55');
INSERT INTO `sys_role_menu` VALUES ('1352', '3', '5');
INSERT INTO `sys_role_menu` VALUES ('1353', '3', '56');
INSERT INTO `sys_role_menu` VALUES ('1355', '3', '89');
INSERT INTO `sys_role_menu` VALUES ('1356', '3', '90');
INSERT INTO `sys_role_menu` VALUES ('1357', '3', '93');
INSERT INTO `sys_role_menu` VALUES ('1358', '3', '94');
INSERT INTO `sys_role_menu` VALUES ('1429', '2', '1');
INSERT INTO `sys_role_menu` VALUES ('1430', '2', '4');
INSERT INTO `sys_role_menu` VALUES ('1431', '2', '23');
INSERT INTO `sys_role_menu` VALUES ('1432', '2', '24');
INSERT INTO `sys_role_menu` VALUES ('1433', '2', '25');
INSERT INTO `sys_role_menu` VALUES ('1434', '2', '26');
INSERT INTO `sys_role_menu` VALUES ('1435', '2', '6');
INSERT INTO `sys_role_menu` VALUES ('1436', '2', '7');
INSERT INTO `sys_role_menu` VALUES ('1437', '2', '8');
INSERT INTO `sys_role_menu` VALUES ('1438', '2', '9');
INSERT INTO `sys_role_menu` VALUES ('1439', '2', '10');
INSERT INTO `sys_role_menu` VALUES ('1440', '2', '11');
INSERT INTO `sys_role_menu` VALUES ('1441', '2', '12');
INSERT INTO `sys_role_menu` VALUES ('1442', '2', '13');
INSERT INTO `sys_role_menu` VALUES ('1443', '2', '14');
INSERT INTO `sys_role_menu` VALUES ('1444', '2', '27');
INSERT INTO `sys_role_menu` VALUES ('1445', '2', '30');
INSERT INTO `sys_role_menu` VALUES ('1446', '2', '36');
INSERT INTO `sys_role_menu` VALUES ('1447', '2', '37');
INSERT INTO `sys_role_menu` VALUES ('1448', '2', '38');
INSERT INTO `sys_role_menu` VALUES ('1449', '2', '39');
INSERT INTO `sys_role_menu` VALUES ('1450', '2', '40');
INSERT INTO `sys_role_menu` VALUES ('1451', '2', '100');
INSERT INTO `sys_role_menu` VALUES ('1452', '2', '101');
INSERT INTO `sys_role_menu` VALUES ('1453', '2', '102');
INSERT INTO `sys_role_menu` VALUES ('1454', '2', '103');
INSERT INTO `sys_role_menu` VALUES ('1455', '2', '104');
INSERT INTO `sys_role_menu` VALUES ('1456', '2', '43');
INSERT INTO `sys_role_menu` VALUES ('1457', '2', '64');
INSERT INTO `sys_role_menu` VALUES ('1458', '2', '65');
INSERT INTO `sys_role_menu` VALUES ('1459', '2', '66');
INSERT INTO `sys_role_menu` VALUES ('1460', '2', '67');
INSERT INTO `sys_role_menu` VALUES ('1461', '2', '68');
INSERT INTO `sys_role_menu` VALUES ('1462', '2', '69');
INSERT INTO `sys_role_menu` VALUES ('1464', '2', '71');
INSERT INTO `sys_role_menu` VALUES ('1465', '2', '72');
INSERT INTO `sys_role_menu` VALUES ('1466', '2', '73');
INSERT INTO `sys_role_menu` VALUES ('1467', '2', '74');
INSERT INTO `sys_role_menu` VALUES ('1468', '2', '75');
INSERT INTO `sys_role_menu` VALUES ('1469', '2', '76');
INSERT INTO `sys_role_menu` VALUES ('1477', '2', '92');
INSERT INTO `sys_role_menu` VALUES ('1478', '2', '49');
INSERT INTO `sys_role_menu` VALUES ('1479', '2', '58');
INSERT INTO `sys_role_menu` VALUES ('1480', '2', '59');
INSERT INTO `sys_role_menu` VALUES ('1481', '2', '60');
INSERT INTO `sys_role_menu` VALUES ('1482', '2', '61');
INSERT INTO `sys_role_menu` VALUES ('1483', '2', '62');
INSERT INTO `sys_role_menu` VALUES ('1484', '2', '50');
INSERT INTO `sys_role_menu` VALUES ('1485', '2', '29');
INSERT INTO `sys_role_menu` VALUES ('1486', '2', '52');
INSERT INTO `sys_role_menu` VALUES ('1487', '2', '31');
INSERT INTO `sys_role_menu` VALUES ('1488', '2', '32');
INSERT INTO `sys_role_menu` VALUES ('1489', '2', '33');
INSERT INTO `sys_role_menu` VALUES ('1490', '2', '34');
INSERT INTO `sys_role_menu` VALUES ('1491', '2', '55');
INSERT INTO `sys_role_menu` VALUES ('1492', '2', '5');
INSERT INTO `sys_role_menu` VALUES ('1493', '2', '56');
INSERT INTO `sys_role_menu` VALUES ('1495', '2', '89');
INSERT INTO `sys_role_menu` VALUES ('1496', '2', '90');
INSERT INTO `sys_role_menu` VALUES ('1497', '2', '93');
INSERT INTO `sys_role_menu` VALUES ('1498', '2', '94');

-- ----------------------------
-- Table structure for sys_schedule
-- ----------------------------
DROP TABLE IF EXISTS `sys_schedule`;
CREATE TABLE `sys_schedule` (
  `job_id` bigint(20) NOT NULL AUTO_INCREMENT COMMENT '任务id',
  `bean_name` varchar(200) DEFAULT NULL COMMENT 'spring bean名称',
  `method_name` varchar(100) DEFAULT NULL COMMENT '方法名',
  `params` varchar(2000) DEFAULT NULL COMMENT '参数',
  `cron_expression` varchar(100) DEFAULT NULL COMMENT 'cron表达式',
  `status` tinyint(4) DEFAULT NULL COMMENT '任务状态  0：正常  1：暂停',
  `remark` varchar(255) DEFAULT NULL COMMENT '备注',
  `is_valid` tinyint(10) NOT NULL,
  `last_ver` tinyint(10) NOT NULL,
  `create_time` bigint(20) NOT NULL DEFAULT '0' COMMENT '创建时间',
  `op_time` bigint(20) NOT NULL DEFAULT '0' COMMENT '修改时间',
  PRIMARY KEY (`job_id`),
  KEY `idx_status` (`status`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='定时任务';

-- ----------------------------
-- Records of sys_schedule
-- ----------------------------

-- ----------------------------
-- Table structure for sys_user
-- ----------------------------
DROP TABLE IF EXISTS `sys_user`;
CREATE TABLE `sys_user` (
  `user_id` bigint(20) NOT NULL AUTO_INCREMENT,
  `username` varchar(50) NOT NULL COMMENT '用户名',
  `img_path` varchar(100) NOT NULL DEFAULT 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/d7bb19a0f02b4d65b28959a896ad8111.jpeg',
  `password` varchar(100) DEFAULT NULL COMMENT '密码',
  `salt` varchar(20) DEFAULT NULL COMMENT '盐',
  `email` varchar(100) DEFAULT NULL COMMENT '邮箱',
  `mobile` varchar(100) DEFAULT NULL COMMENT '手机号',
  `type` tinyint(4) DEFAULT NULL COMMENT '0：管理员 1：前台用户',
  `status` tinyint(4) DEFAULT NULL COMMENT '状态  0：禁用   1：正常',
  `dept_id` bigint(20) DEFAULT NULL COMMENT '部门ID',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`user_id`),
  UNIQUE KEY `username` (`username`)
) ENGINE=InnoDB AUTO_INCREMENT=7 DEFAULT CHARSET=utf8 COMMENT='系统用户';

-- ----------------------------
-- Records of sys_user
-- ----------------------------
INSERT INTO `sys_user` VALUES ('1', 'admin', 'https://chenxingxing6.github.io/img/header.jpg', 'e1153123d7d180ceeb820d577ff119876678732a68eef4e6ffc0b1f06a01f91b', 'YzcmCZNvbXocrsz9dm8e', 'root@renren.io', '13612345678', '0', '1', '34', '2016-11-11 11:11:11');
INSERT INTO `sys_user` VALUES ('2', 'user', '', '288670b43b826eeeb4696bdacbafb6a290a579492f6b1d614c060055dd40e360', '0HA3eDK0OS2TXIRK5CN8', '123@qq.com', '18376543765', '0', '1', '10', '2018-07-31 19:29:30');
INSERT INTO `sys_user` VALUES ('3', 'test', '', '2a82a436f50b8ecbb9548cdde178c574965c8e25337ded5f7bcaf848ebae9a17', 'Hww2SwK1WF0eWUrRHRPV', '1527072012@qq.com', '18379643981', '0', '1', '13', '2018-12-30 22:45:24');
INSERT INTO `sys_user` VALUES ('4', 'front', 'https://static.vilson.xyz/cover.png', '123456', '', 'front@qq.com', '18379643980', '1', '1', '13', '2018-12-30 22:45:24');
INSERT INTO `sys_user` VALUES ('5', 'front2', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/66c0519c70f74ddebea2c47142836b86.jpeg', '123456', null, 'lanxinghua@2dfire.com', '18379643982', '1', '1', '26', '2019-03-17 16:47:19');
INSERT INTO `sys_user` VALUES ('6', 'front1', 'http://ppkn5nh6t.bkt.clouddn.com/upload/20190414/d7bb19a0f02b4d65b28959a896ad8111.jpeg', '123456', null, 'front1@qq.com', '18379643981', '1', '1', '26', '2019-04-14 13:11:38');

-- ----------------------------
-- Table structure for sys_user_role
-- ----------------------------
DROP TABLE IF EXISTS `sys_user_role`;
CREATE TABLE `sys_user_role` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `user_id` bigint(20) DEFAULT NULL COMMENT '用户ID',
  `role_id` bigint(20) DEFAULT NULL COMMENT '角色ID',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=23 DEFAULT CHARSET=utf8 COMMENT='用户与角色对应关系';

-- ----------------------------
-- Records of sys_user_role
-- ----------------------------
INSERT INTO `sys_user_role` VALUES ('15', '1', '2');
INSERT INTO `sys_user_role` VALUES ('21', '3', '3');
INSERT INTO `sys_user_role` VALUES ('22', '2', '2');

-- ----------------------------
-- Table structure for tb_disk_file
-- ----------------------------
DROP TABLE IF EXISTS `tb_disk_file`;
CREATE TABLE `tb_disk_file` (
  `id` bigint(20) NOT NULL AUTO_INCREMENT,
  `disk_id` bigint(20) DEFAULT NULL COMMENT '用户ID',
  `file_id` bigint(20) DEFAULT NULL COMMENT '文件ID',
  `is_valid` tinyint(4) NOT NULL DEFAULT '1' COMMENT '是否有效',
  `create_user` varchar(32) DEFAULT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=27 DEFAULT CHARSET=utf8 COMMENT='企业共享网盘和文件对应关系';

-- ----------------------------
-- Records of tb_disk_file
-- ----------------------------
INSERT INTO `tb_disk_file` VALUES ('10', '2', '1114006406769410048', '1', '1', '1554434799846');
INSERT INTO `tb_disk_file` VALUES ('11', '5', '1114018473761046528', '1', '1', '1554437677322');
INSERT INTO `tb_disk_file` VALUES ('12', '1', '1114018706649776128', '1', '1', '1554437732108');
INSERT INTO `tb_disk_file` VALUES ('13', '2', '1114019201443430400', '1', '1', '1554437850057');
INSERT INTO `tb_disk_file` VALUES ('14', '2', '1114019422630051840', '1', '1', '1554437903222');
INSERT INTO `tb_disk_file` VALUES ('16', '5', '1114019937132740608', '1', '1', '1554438025481');
INSERT INTO `tb_disk_file` VALUES ('17', '5', '1114020034914549760', '1', '1', '1554438048870');
INSERT INTO `tb_disk_file` VALUES ('20', '3', '1114021696110592000', '1', '1', '1554438445037');
INSERT INTO `tb_disk_file` VALUES ('21', '4', '1114022323305840640', '1', '1', '1554438596848');
INSERT INTO `tb_disk_file` VALUES ('23', '1', '1114124474074005504', '1', '1', '1554462949187');
INSERT INTO `tb_disk_file` VALUES ('24', '1', '1114126315042111488', '1', '1', '1554463388670');
INSERT INTO `tb_disk_file` VALUES ('25', '1', '1114020034914549760', '1', '5', '1555234431542');
INSERT INTO `tb_disk_file` VALUES ('26', '1', '1114020034914549760', '1', '5', '1555234478447');

-- ----------------------------
-- Table structure for tb_file
-- ----------------------------
DROP TABLE IF EXISTS `tb_file`;
CREATE TABLE `tb_file` (
  `id` bigint(20) NOT NULL COMMENT '文件ID',
  `parent_id` bigint(20) DEFAULT '0' COMMENT '文件父ID',
  `original_name` varchar(200) DEFAULT NULL COMMENT '原版文件名 x9Bx98.pptx',
  `name` varchar(100) DEFAULT NULL COMMENT '文件名 42759866854752.pptx',
  `original_path` varchar(200) DEFAULT NULL COMMENT '原版文件路径 /file/',
  `path` varchar(100) DEFAULT NULL COMMENT '文件路径 /39166745223986/42759866854752.pptx',
  `length` varchar(100) DEFAULT NULL COMMENT '文件长度 73.1',
  `type` tinyint(4) DEFAULT NULL COMMENT '文件类型  0：目录  1：文件',
  `view_flag` tinyint(4) DEFAULT NULL COMMENT '是否可用看',
  `is_valid` tinyint(4) NOT NULL DEFAULT '1' COMMENT '是否有效',
  `create_user` varchar(32) DEFAULT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  `op_user` varchar(32) DEFAULT NULL COMMENT '更新者',
  `op_time` bigint(20) DEFAULT NULL COMMENT '更新时间',
  `last_ver` smallint(6) NOT NULL DEFAULT '0' COMMENT '版本号',
  `download_num` int(11) NOT NULL DEFAULT '0' COMMENT '下载数量',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户与文件对应关系';

-- ----------------------------
-- Records of tb_file
-- ----------------------------
INSERT INTO `tb_file` VALUES ('1109752275888242688', '0', 'aa', '22434641249440', '/aa', '/22434641249440', '0', '0', '0', '1', '1', '1553420535429', '1', '1553420535429', '0', '0');
INSERT INTO `tb_file` VALUES ('1109756642225815552', '0', 'bb', '23475667550304', '/bb', '/23475667550304', '0', '0', '0', '1', '1', '1553421576446', '1', '1553421576446', '0', '0');
INSERT INTO `tb_file` VALUES ('1110575982755971072', '0', 'cc', '4182564718374', '/cc', '/4182564718374', '0', '0', '0', '1', '1', '1553616922451', '1', '1553616922451', '0', '0');
INSERT INTO `tb_file` VALUES ('1110577403521925120', '0', 'dd', '4521303593704', '/dd', '/4521303593704', '0', '0', '0', '1', '1', '1553617261189', '1', '1553619058810', '0', '0');
INSERT INTO `tb_file` VALUES ('1110768124900147200', '0', 'ee', '3015795554704', '/ee', '/3015795554704', '0', '0', '0', '1', '1', '1553662732710', '1', '1553662744865', '0', '0');
INSERT INTO `tb_file` VALUES ('1110777257007251456', '1109756642225815600', 'b11', '5193058369259', '/1', '/5193058369259', '0', '0', '0', '1', '1', '1553664909972', '5', '1555232359469', '0', '0');
INSERT INTO `tb_file` VALUES ('1113731890847678464', '0', '学生在网络学习系统中的表现-文献.doc', '24191530366782.doc', 'originalDir', '24191530366782.doc', '107.05K', '1', '1', '1', '1', '1554369349574', '1', '1554369349574', '0', '0');
INSERT INTO `tb_file` VALUES ('1113733726732288000', '0', '学生在网络学习系统中的表现-文献.doc', '24600243590169.doc', 'originalDir', '24600243590169.doc', '107.05K', '1', '1', '1', '1', '1554369833153', '1', '1554369833153', '0', '0');
INSERT INTO `tb_file` VALUES ('1113736443366211584', '0', '学生在网络学习系统中的表现-文献.doc', '25276943757982.doc', '/', '/25276943757982.doc', '107.05K', '1', '1', '1', '1', '1554370434978', '1', '1554370434978', '0', '0');
INSERT INTO `tb_file` VALUES ('1113771253459582976', '0', '开题报告-祝一鸣.doc', '33576396287929.doc', '/', '/33576396287929.doc', '36.50K', '1', '1', '1', '1', '1554378734351', '1', '1554462411136', '0', '0');
INSERT INTO `tb_file` VALUES ('1113789953386479616', '0', '学生在网络学习系统中的表现-文献.doc', '34547136442823.doc', '/', '/34547136442823.doc', '107.05K', '1', '1', '1', '1', '1554383192761', '1', '1554383192761', '0', '0');
INSERT INTO `tb_file` VALUES ('1113807580095840256', '0', '学生在网络学习系统中的表现-文献.doc', '38748639816795.doc', '/', '/38748639816795.doc', '107.05K', '1', '1', '1', '1', '1554387395297', '1', '1554387395297', '0', '0');
INSERT INTO `tb_file` VALUES ('1114006406769410048', '0', 'aaaa.jpg', '4655231803367.jpg', '/', '/4655231803367.jpg', '104.29K', '1', '1', '1', '1', '1554434799269', '1', '1554434799269', '0', '0');
INSERT INTO `tb_file` VALUES ('1114018473761046528', '0', '接收函.pdf', '7532255965812.pdf', '/', '/7532255965812.pdf', '143.84K', '1', '1', '1', '1', '1554437676264', '1', '1554437676264', '0', '0');
INSERT INTO `tb_file` VALUES ('1114018706649776128', '0', 'aa.html', '7587781083959.html', '/', '/7587781083959.html', '10.99K', '1', '1', '1', '1', '1554437731789', '1', '1554437731789', '0', '0');
INSERT INTO `tb_file` VALUES ('1114019201443430400', '0', 'timg.jpeg', '7705750620698.jpeg', '/', '/7705750620698.jpeg', '12.15K', '1', '1', '1', '1', '1554437849757', '1', '1554437849757', '0', '0');
INSERT INTO `tb_file` VALUES ('1114019422630051840', '0', '冯提莫.gif', '7758486702962.gif', '/', '/7758486702962.gif', '1.09M', '1', '1', '1', '1', '1554437902492', '1', '1554462521080', '0', '0');
INSERT INTO `tb_file` VALUES ('1114019855914237952', '0', '陈星星-申请华东交大2019届优秀毕业生.xls', '7861789692832.xls', '/', '/7861789692832.xls', '19.00K', '1', '1', '1', '1', '1554438005795', '1', '1554438005795', '0', '0');
INSERT INTO `tb_file` VALUES ('1114019937132740608', '0', '新建文本文档.txt', '7881153883406.txt', '/', '/7881153883406.txt', '3.03K', '1', '1', '1', '1', '1554438025159', '1', '1554438025159', '0', '0');
INSERT INTO `tb_file` VALUES ('1114020034914549760', '0', '陈星星第5周日志.docx', '7904467397193.docx', '/', '/7904467397193.docx', '64.57K', '1', '1', '1', '1', '1554438048472', '5', '1555232369757', '0', '0');
INSERT INTO `tb_file` VALUES ('1114020557772292096', '0', '毕业设计共性问题及说明（刘向）.docx', '8029127158639.docx', '/', '/8029127158639.docx', '30.66K', '1', '1', '1', '1', '1554438173131', '1', '1554438173131', '0', '0');
INSERT INTO `tb_file` VALUES ('1114020578156609536', '0', '2019届选题审批汇总表.xls', '8033987989726.xls', '/', '/8033987989726.xls', '26.50K', '1', '1', '1', '1', '1554438177991', '1', '1554438177991', '0', '0');
INSERT INTO `tb_file` VALUES ('1114021696110592000', '0', 'Nextcloud.mp4', '8300531064475.mp4', '/', '/8300531064475.mp4', '451.58K', '1', '1', '1', '1', '1554438444532', '1', '1554438444532', '0', '0');
INSERT INTO `tb_file` VALUES ('1114022323305840640', '0', 'Auld_Lang_Syne-Sissel_Kyrkjebo.mp3', '8450066804036.mp3', '/', '/8450066804036.mp3', '6.04M', '1', '1', '1', '1', '1554438594067', '1', '1554438594067', '0', '0');
INSERT INTO `tb_file` VALUES ('1114123995474558976', '0', '祝一鸣-开题报告-文献以及翻译.zip', '21657518382659.zip', '/', '/21657518382659.zip', '49.81K', '1', '1', '1', '1', '1554462834601', '1', '1554462834601', '0', '0');
INSERT INTO `tb_file` VALUES ('1114124474074005504', '0', 'easyUpload.zip', '21771625843228.zip', '/', '/21771625843228.zip', '135.67K', '1', '1', '1', '1', '1554462948708', '1', '1554462948708', '0', '0');
INSERT INTO `tb_file` VALUES ('1114126315042111488', '0', 'README111.txt', '22210551268435.txt', '/', '/22210551268435.txt', '1.44K', '1', '1', '1', '1', '1554463387629', '5', '1555225533654', '0', '0');
INSERT INTO `tb_file` VALUES ('1117408266112991232', '0', 'sysnotice_menu.sql', '35848220188314.sql', '/', '/35848220188314.sql', '970.00B', '1', '1', '1', '6', '1555245869905', '6', '1555245870581', '0', '0');
INSERT INTO `tb_file` VALUES ('1117409354761371648', '0', 'timg.jpeg', '36108688943313.jpeg', '/', '/36108688943313.jpeg', '22.25K', '1', '1', '1', '6', '1555246125294', '6', '1555246125294', '0', '0');
INSERT INTO `tb_file` VALUES ('1117410716551217152', '0', 'timg.jpeg', '36433366131128.jpeg', '/', '/36433366131128.jpeg', '22.25K', '1', '1', '1', '6', '1555246449970', '6', '1555246449970', '0', '0');

-- ----------------------------
-- Table structure for tb_follow
-- ----------------------------
DROP TABLE IF EXISTS `tb_follow`;
CREATE TABLE `tb_follow` (
  `id` bigint(20) NOT NULL COMMENT 'ID',
  `from_user_id` bigint(20) DEFAULT NULL COMMENT '用户ID',
  `to_user_id` bigint(20) DEFAULT NULL COMMENT '被关注用户ID',
  `is_valid` tinyint(4) NOT NULL DEFAULT '1' COMMENT '是否有效',
  `create_user` varchar(32) DEFAULT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  `op_user` varchar(32) DEFAULT NULL COMMENT '更新者',
  `op_time` bigint(20) DEFAULT NULL COMMENT '更新时间',
  `last_ver` smallint(6) NOT NULL DEFAULT '0' COMMENT '版本号',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='关注用户表';

-- ----------------------------
-- Records of tb_follow
-- ----------------------------
INSERT INTO `tb_follow` VALUES ('1117307998776066048', '5', '4', '1', '5', '1555221960144', '5', '1555221960144', '0');

-- ----------------------------
-- Table structure for tb_share
-- ----------------------------
DROP TABLE IF EXISTS `tb_share`;
CREATE TABLE `tb_share` (
  `id` bigint(20) NOT NULL COMMENT 'ID',
  `from_user_id` bigint(20) DEFAULT NULL COMMENT '用户ID',
  `from_user_name` varchar(100) DEFAULT NULL COMMENT '用户名',
  `to_user_id` bigint(20) DEFAULT NULL COMMENT '被关注用户ID',
  `to_user_name` varchar(100) DEFAULT NULL COMMENT '用户名',
  `file_id` bigint(20) DEFAULT NULL COMMENT '被关注用户ID',
  `file_name` varchar(100) DEFAULT NULL COMMENT '文件名',
  `expired_time` bigint(20) DEFAULT NULL COMMENT '过期时间',
  `is_valid` tinyint(4) NOT NULL DEFAULT '1' COMMENT '是否有效',
  `create_user` varchar(32) DEFAULT NULL COMMENT '登录者',
  `create_time` bigint(20) DEFAULT NULL COMMENT '登录时间',
  `op_user` varchar(32) DEFAULT NULL COMMENT '更新者',
  `op_time` bigint(20) DEFAULT NULL COMMENT '更新时间',
  `last_ver` smallint(6) NOT NULL DEFAULT '0' COMMENT '版本号',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='分享表';

-- ----------------------------
-- Records of tb_share
-- ----------------------------
INSERT INTO `tb_share` VALUES ('2', '2', 'b', '5', 'a', '1114020034914549760', 'aaa.docx', '111', '1', '1', '111', '1', '1111', '0');
INSERT INTO `tb_share` VALUES ('1117357005116276736', '5', 'front2', '6', 'front1', '1114020034914549760', '陈星星第5周日志.docx', '1555320044248', '1', '5', '1555233644291', '5', '1555233644291', '0');
INSERT INTO `tb_share` VALUES ('1117421342174478336', '6', 'front1', '6', 'front1', '1117410991466872832', 'README.txt', '1555335383402', '1', '6', '1555248983437', '6', '1555248983437', '0');
INSERT INTO `tb_share` VALUES ('1117423207134003200', '6', 'front1', '6', 'front1', '1117410991466872832', 'README.txt', '1555335828066', '1', '6', '1555249428066', '6', '1555249428066', '0');

-- ----------------------------
-- Table structure for tb_user_file
-- ----------------------------
DROP TABLE IF EXISTS `tb_user_file`;
CREATE TABLE `tb_user_file` (
  `id` bigint(20) NOT NULL,
  `user_id` bigint(20) DEFAULT NULL COMMENT '用户ID',
  `file_id` bigint(20) DEFAULT NULL COMMENT '文件ID',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='用户与文件对应关系';

-- ----------------------------
-- Records of tb_user_file
-- ----------------------------
INSERT INTO `tb_user_file` VALUES ('22', '5', '1114020034914549760');
INSERT INTO `tb_user_file` VALUES ('1109752276039237632', '1', '1109752275888242688');
INSERT INTO `tb_user_file` VALUES ('1109756642531999744', '1', '1109756642225815552');
INSERT INTO `tb_user_file` VALUES ('1110575983078932480', '1', '1110575982755971072');
INSERT INTO `tb_user_file` VALUES ('1110577404142682112', '1', '1110577403521925120');
INSERT INTO `tb_user_file` VALUES ('1110768125244080128', '1', '1110768124900147200');
INSERT INTO `tb_user_file` VALUES ('1110777257305047040', '1', '1110777257007251456');
INSERT INTO `tb_user_file` VALUES ('1110777257305047041', '5', '1110777257007251456');
INSERT INTO `tb_user_file` VALUES ('1110777257305047042', '5', '1114020034914549760');
INSERT INTO `tb_user_file` VALUES ('1117410720724549632', '6', '1117410716551217152');

```





