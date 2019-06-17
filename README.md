#### 博客搭建步骤

1. 初始化工程
```js
npm install -g hexo-cli // 安装命令行工具

hexo init blog          // 生成blog工程
```

2. git服务新建分支: osc-pages
```js
// 启动Gitee Pages服务报错: 
// 部署失败
// 错误信息: no implicit conversion of Hash into String

// hexo deploy之后, 再次开启Gitee Pages服务正常
```

3. 修改_config.yml配置文件

4. 生成静态页面
```
hexo generate
```

5. 启动本地服务访问
```
hexo server
```

6. 部署到git
```js
hexo deploy
// 命令执行异常, 缺少部署模块
// ERROR Deployer not found: git
npm install --save hexo-deployer-git
```