# kplayer-Management
## kplayer管理平台
> ### 使用技术
springboot + vue + element-ui
> ### 参考文档
https://docs.kplayer.net/v0.5.8/api/plugin.html
## 如何部署
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


