---
title: cnpm搭建公司内部模块管理
date: 2016-05-09 23:49:17
tags:
- npm
categories: 包管理
---

参考资料：
> http://segmentfault.com/a/1190000000368906
> http://blog.fens.me/nodejs-cnpm-npm/
> http://www.cnblogs.com/wyzfzu/p/4149310.html
> http://www.tuicool.com/articles/JZNzY3j
> 
> https://docs.npmjs.com/getting-started/scoped-packages

*本人是在windows7上搭建，上面地址有linux上搭建方法请参考*

**获取代码**

    git clone git://github.com/fengmk2/cnpmjs.org.git $HOME/cnpmjs.org
	
	cd $HOME/cnpmjs.org
	
	或者：git clone https://github.com/cnpm/cnpmjs.org.git

**创建MySQL表**

1.在mysql中先创建数据库cnpmjs

    drop database if exists cnpmjs;
    create database cnpmjs;

2.打开C:\Users\Administrator\cnpmjs.org\docs

    use cnpmjs;
    source C:\Users\Administrator\cnpmjs.org\docs
    show tables;
**数据库表执行完成后，修改C:\Users\Administrator\cnpmjs.org\config下的index.js配置文件**


- 注释掉bindingHost: '127.0.0.1,其他电脑也可以访问
- 配置登录用户名

```
admins: {
	// name: email
	admin: 'admin@cnpmjs.org'
}
```

- database:

```
	db: 'cnpmjs',
    username: 'root',
    password: 'root',
    dialect: 'mysql',
    host: '127.0.0.1',
    port: 3306,
```

- registry配置

```
enablePrivate: true,
scopes: [ '@cnpm', '@cnpmtest', '@cnpm-test' ],
```

- sync配置

```
synoModel: 'exist'
```

**升级node,npm**

1.node最新版本在官网下载升级

[http://nodejs.cn/](http://nodejs.cn/ "http://nodejs.cn/")

2.npm通过下面命令即可升级

`npm install npm -g`

**安装项目依赖包**

1.打开cmd

2.切换到C:\Users\Administrator\cnpmjs.org目录

`cd /dC:\Users\Administrator\cnpmjs.org`

3.执行：`npm install`命令，nodejs 会根据package.json进行依赖包的安装

**一切准备完成，启动程序**

`cd /dC:\Users\Administrator\cnpmjs.org`

1.启动

`node dispatch.js`

2.通过浏览器访问，CNPM服务：http://localhost:7002

**从npm下载模块**

在页面搜索`log4js`模块

然后点击页面sync链接即可同步到本地

**安装使用模块**

1.安装cnpm模块`npm install cnpm -g`

2.指定私有库

查看`cnpm config list`


设置`cnpm config set registry http://localhost:7001`

3.使用`cnpm install -g log4js`

**上传私有模块**

1.用户（配置文件中的）
```
admins: {
	admin: 'admin@cnpmjs.org'
}
```

2.设置密码

`cnpm adduser --registry=http://localhost:7001`

`Username:admin`

`password:admin`

`Email:admin@cnpmjs.org`

3.用上面密码登录

`cnpm login --registry=http://localhost:7001`

4.设置scope(配置文件中）

`scopes: [ '@cnpm', '@cnpmtest', '@cnpm-test' ]`


5.生成自己的模块

- 新建目录：C:\Users\Administrator\self-test-module
- cd /dC:\Users\Administrator\self-test-module

`cnpm init --scope=cnpmtest`

- package.json文件已经生成

- 自己写一个index.js

- 发布：`cnpm publish`

6.这样在页面就可以搜到self-test-module模块

`cnpm install self-test-module`安装

程序中使用：

`require('@cnpmtest/self-test-module'`