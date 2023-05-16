# kplayer-Management
## kplayer管理平台
> ### 功能展示
  + 首页
  ![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/bac23270-ea88-492f-9829-2c264978bf27)
  + 资源配置页
  ![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/816310fb-9849-4b4f-a51d-3a92dfa0cfaa)
  + 输出配置页（推流地址管理）
  ![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/deccaea8-febe-40c2-84ec-37fe9fb8a3be)
  + 插件配置页
  ![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/0a5166c4-d543-40b7-992f-b3d7878e4b8d)
> ### 使用技术
springboot + vue + element-ui
> ### 参考文档
https://docs.kplayer.net/v0.5.8/api/plugin.html
## 本地如何部署
> ### 1.配置服务器文件
   + 进入你服务器的kplayer文件夹下
   + 编辑config.json文件
   + 修改里面内容,将 rpc功能打开,或者你直接复制我那部分
```java
    "play": {
    "start_point": 1,
    "play_model": "loop",
    "encode_model": "rtmp",
    "cache_on": false,
    "cache_uncheck": false,
    "skip_invalid_resource": true,
    "fill_strategy": "tile",
          "rpc": {
          "on": true,
          "http_port": 4156,
          "grpc_port": 4157,
          "address": "0.0.0.0"
          }
    },
```
   + 服务器防火墙记得开放4156端口
> ### 2.后端配置

+ 下载压缩文件  kplayerdemo.zip 解压至本地
+ 打开代码运行工具，idea或其他   |没有的或者不会的等待jar包
+ 进入项目，修改maven为你的仓库
+ 修改application.properties 文件
   + myapp.server.url=http://ip:4156    ip为你的服务器地址，端口同上配置config.json文件里rpc的4156
+ 运行KplayerApplication
+ 后端启动端口默认8080

> ### 3.前端配置
+ 确认本地存在node环境 推荐16版本
+ 下载vue-admin压缩文件 解压至本地
+ 打开代码运行工具，hbulider,或vscode
+ 进入项目
```
npm install 
npm run dev 
```
+ 浏览器进入http://localhost:9528/
## 服务器如何部署
> ### 准备工作
+ 服务器安装宝塔面板
+ 安装Node.js版本管理器 并下载v16.13.2版本
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/62c32d1b-f2e9-4671-acfa-406c79195e30)

+ 安装Tomcat 8.5.78
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/53537699-1ec6-43d3-8f81-a4ad8ea5edc7)

+ 为避免服务占用8080导致冲突，我们可以换个端口
   + 开放 9528端口
   + 开放	8677端口
+ 上传文件 将jar文件上传至服务器/home下
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/c1b71596-1621-4cef-813d-1e4e67e9d041)

+ 上传文件 将项目中的application.properties文件上传至/home下
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/7c2c8b55-c5ae-4c47-839d-8105efa2d4a4)

+ application.properties配置如下
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/eca3df12-12f5-47b4-8f56-ea0c7e88bfbb)

```java
myapp.server.url=http://你的服务器ip:4156
spring.mvc.hiddenmethod.filter.enabled=true
server.port=8677
```
+ 上传文件 将项目中的vue-admin文件上传至服务器/www/wwwroot/kplayeradmin下，或者你随意放置，自己记住位置就行
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/33b5af09-88f8-47f2-8cbe-5e7f3bb5a209)

> ### 文件配置
+ 进入你服务器vue-admin文件下，编辑vue.config.js文件
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/67e66fd7-7e5f-4f9e-aa18-ee81afa978fd)

+ 修改以下内容
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/8a982959-73b2-45d0-b2a0-b798d248c2cf)

```java
 proxy: {
          '/dev-api': {
            target: 'http://localhost:8677',
            changeOrigin: true,
            pathRewrite: {
              '^/dev-api': ''
            }
          }
        },
```
+ 进入你服务器vue-admin文件下,编辑项目src下的main.js文件
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/cd948174-2c3b-4001-a662-8926737da0e3)

+ 修改以下内容
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/0cab68af-442e-47f6-b624-93a577eed62b)

```java
Vue.prototype.$apiDev = 'http://服务器ip地址:8677'
```
+ 打开终端，进入你服务器vue-admin文件下
+ 执行以下命令,
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/965ff426-694c-4ea7-88e0-30e86f346437)

```java
npm install 
```
> ### 运行后端服务
+ 打开终端，进入jar包存在路径，也就是/home下
+ 执行以下命令进行测试后端服务
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/6f0ffd03-34ba-4707-ad84-08e4d3cdcb07)

```java
java -jar yuan-0.0.1-SNAPSHOT.jar
```
+ 执行完毕进行测试
+ 打开你浏览器，输入http://服务器ip:8677/resource/list-all
+ 看到出内容就代表后端启动成功
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/d48acde5-1749-4a87-b089-afe465483879)

+ 成功之后可以运行到后台
+ 打开终端，进入jar包存在路径，也就是/home下
+  执行以下命令进行后端后台运行
```java
nohup java -jar yuan-0.0.1-SNAPSHOT.jar &
```
+ 没成功请发送消息到issues
> ### 运行前端服务
+ 打开宝塔左侧网站管理
+ 点击Node项目,选择添加Node项目
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/1c3936f8-0e75-431c-a772-c392485bfe29)
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/3f2dfc74-25e5-4d94-b896-94482e3699ef)

   + 项目目录选择你上传的vue-admin存放的路径
   + 项目名称随意
   + 启动项自己配置 输入npm run dev
   + 运行端口选择 9528
   + 运行用户自己选择
   + node版本选择 v16.13.2
   + 备注随意
   + 绑定域名，添加你的域名或者直接输入ip
   + 点击提交
+ 点击右侧设置，点击左侧项目日志
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/b579fe6b-087b-4add-bae2-705f5c1a1443)

+ 等待一会刷新一下
+ 如果没有执行成功显示如下
![30c515c246c37cb25dc7538223a2bad](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/eb4cbba5-ecae-4994-a6e3-318d5a91cfca)
+ 还是进入vue-admin存放的路径，那么你可以尝试以下命令
 ```
 npm install core-js@3 --save
 ```
+ 再次重启项目将显示正常运行
![image](https://github.com/dooooongyuan/kplayer-Management/assets/128032721/b6c2fa99-8b1d-4936-84cf-caafcf2183e2)

```java
App running at:
  - Local:   http://localhost:9528/ 
  - Network: http://10.0.4.6:9528/

  Note that the development build is not optimized.
  To create a production build, run yarn build.
```
+ 最后打开http://ip地址/#/dashboard 即可进入管理页面



