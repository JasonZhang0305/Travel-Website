# Black Horse Travel Website 黑马旅游网项目实现

## A fullstack project for practicing programming skills included with font-end, back-end and database.

Main Tools: Idea2023 + JDK8 + Maven
Server: Tomcat 
Frameworks: Bootstrap + Jquery + JdbcTemplate
Database: Mysql + Redis  
Others：HTML+CSS+JS

# 项目简介：
本项目有黑马程序员网校提供，结合Javaweb课程进行学习，可以对基于Java语言的web开发有一个初步的了解。视频链接附在了下面。前端是有预先准备好的资料，可以直接用webapp的包，课程前半部分也会教如何搭建前端页面。此网站是基于Bootstrap和其内置的Jquery制作的，画风比较简约，很容易上手。后台开发简单实现了登陆，注册，退出，路线查询，分类展示，收藏这几个功能。总体代码量不大，但是可以帮助初学者掌握web开发的基本框架。后续可以学习SSM，springboot等框架进行完善。

# 项目目录：
 ![Project Directory](https://drive.google.com/file/d/1IZNZyaXRPnuo2l6b6N_rILMb2eUJUWUl/view?usp=share_link)

视频学习网址：https://www.bilibili.com/video/BV1qv4y1o79t/?spm_id_from=333.337.search-card.all.click&vd_source=126a675e30d3918492f9fe1ca7b624d4

## 三层架构：
1.1 Web层

a) Servlet：前端控制器

b) html：视图。 这个项目是网站项目，要求面向普通客户，需要响应速度快，因此不采用jsp。做后台的办公系统之类的网站时一般使用jsp技术。

c) Filter：过滤器 （过滤器一般用于拦截请求，过滤响应，常见拦截的应用场景有权限检查，日记操作，事务管理等。本项目中只编写了CharacterFilter,用于解决乱码问题）

d) BeanUtils：数据封装

e) Jackson：json序列化工具。Javascript Object Notation 是一种数据格式 因为使用了html那么为了进行数据传输，需要使用json序列化工具。


1.2 Service层

f) Javamail：java发送邮件工具

g) Redis：Nosql内存数据库 响应速度快，单存放于内存中，需要对其进行持久化

h) Jedis：java的redis客户端。 分类部分的数据在每一次页面加载后都会重新请求数据库来加载，对数据库的压力比较大，而且分类的数据不会经常产生变化，所有可以使用redis来缓存这些数据。


1.3 Dao层

i) Mysql：数据库

j) Druid：数据库连接池 Jdbcpool 用于提高数据链接的效率性

k) JdbcTemplate：Spring的jdbc工具 导入jar包，简化书写，方便开发

# 项目导入
配置好所需要的开发环境，加载peom文件，启动服务器即可。
要点！！
1.修改Jdbc的properties：
![DB](https://drive.google.com/file/d/1lZOm39xGXndQwMvzoDnRQ8-6PESA5sbA/view?usp=share_link)
2.创建并连接数据库，所需要的数据在Mysql文件夹下：
 ![DB](https://drive.google.com/file/d/1P4_OENG6cBjU25Sk5cH3crDZCY8FlA7j/view?usp=share_link)
3.在Idea上运行Tomcat：
 ![Tomcat](https://drive.google.com/file/d/1DtYchMYyjRqLujnPGjNG5XtMULAr1Joe/view?usp=share_link)


功能实现：

3.1 基本注册功能流程

 注册时需要验证用户信息。

 3.2 邮箱激活功能

 需要先开启服务然后才能使用，开启后在MailUtils.java类中填上自己的邮箱账号和授权码或者登陆密码，代码中有一个测试代码可以先运行测试。 
 ![Register](https://drive.google.com/file/d/1Fx2a1kuhZAT92GitpPRgTcag-GUrqCf6/view?usp=share_link)


4 登陆和退出

登陆页面流程
![Login](https://drive.google.com/file/d/1Fmk5ggMKgt6NxOdTJTX588NDv-dF9VPl/view?usp=share_link)

主页
![Home](https://drive.google.com/file/d/1D6_m9X-V9Vh2_NNHeIaKvdgJjjJVVM4w/view?usp=share_link)

5 收藏功能

点击收藏会记录收藏次数，需要写与数据库交互的逻辑
![Login](https://drive.google.com/file/d/1uYYDjs3pyF2a-RXxKCXmdi_vnBMHPVLN/view?usp=share_link)

 
6 分类数据展示

 6.1 缓存数据优化

因为分类数据

分类的数据在每一次页面加载后都会重新请求数据库来加载，对数据库的压力比较大，而且分类的数据不会经常产生变化，所有可以使用redis来缓存这个数据。