# go-fly
基于GO语言实现的web客服即时通讯与客服管理系统。

1.使用gin http框架实现restful风格的API和template包的模板语法进行展示界面

2.使用jwt-go配合gin中间件实现无状态的jwt登陆认证

3.数据库实现的rbac权限配合gin中间件实现权限控制

4.通过cobra进行命令行参数解析和执行对应的功能

5.使用go modoule解决依赖问题

6.使用swagger实现文档展示

7.使用go-imap实现邮件的列表展示和读取

8.使用go-smtp实现发送邮件

9.使用github.com/gorilla/websocket实现即时通讯

10.使用gorm配合mysql实现数据存储

11.前端使用elementUI和Vue展示界面

11.充分实践了struct，interface，map，slice，for range,groutine和channel管道等基础知识

### 项目预览

![Image text](https://gitee.com/taoshihan/go-fly/raw/master/static/images/newintro1.jpg)

![Image text](https://img2020.cnblogs.com/blog/726254/202009/726254-20200902141707515-1201702349.jpg)

![Image text](https://gitee.com/taoshihan/go-fly/raw/master/static/images/newintro2.jpg)

![Image text](https://img2020.cnblogs.com/blog/726254/202009/726254-20200902141736713-1155907367.jpg)

![Image text](https://gitee.com/taoshihan/go-fly/raw/master/static/images/newintro3.jpg)


### 安装使用


#### 1. 先安装和运行mysql >=5.7版本 , 创建gofly数据库.
 
    create database gofly charset utf8;
   
   在config目录mysql.json中配置数据库
```php
{
	"Server":"127.0.0.1",
	"Port":"3306",
	"Database":"gofly",
	"Username":"go-fly",
	"Password":"go-fly"
}
```
#### 2. 二进制文件运行

   1) 下载地址 

        github: https://github.com/taoshihan1991/go-fly/releases/download/0.2.3/gofly-0.2.3.zip
   
        gitee(国内): https://gitee.com/taoshihan/go-fly/attach_files/608635/download/gofly-0.2.3.zip
   
   2) 文件解压缩 
   
        windows系统下,在cmd命令行,进入项目解压后目录; linux系统下创建目录执行如下 
        
            linux服务器:
            mkdir go-fly
            cd go-fly
            wget https://gitee.com/taoshihan/go-fly/attach_files/608635/download/gofly-0.2.3.zip
            unzip gofly-0.2.3.zip
            chmod 0777 -R ./
        
        导入数据库( 注意:会删除表并且清空数据 ) 
        
            windows: go-fly.exe install
            
            linux: ./go-fly install

        运行项目
        
            linux:   ./go-fly server [可选 -p 8082 -d]
           
            windows: go-fly.exe server [可选 -p 8082]
        
   3) 参数说明
    
        -p 指定端口
        
        -d linux下是否以daemon守护进程运行
        
        -h 查看帮助 
        
#### 3. 源码运行

1. 基于go module使用

   go env -w GO111MODULE=on
   
   go env -w GOPROXY=https://goproxy.cn,direct
   
   在任意目录 git clone https://github.com/taoshihan1991/go-fly.git
   
   进入go-fly 目录

2. 源码运行 go run go-fly.go server

3. 源码打包 go build go-fly.go 会生成go-fly可以执行文件

4. 导入数据库(会删除表清空数据) ./go-fly install

5. 二进制文件运行
 
   linux:   ./go-fly server [可选 -p 8082 -d]
   
   windows: go-fly.exe server [可选 -p 8082 -d]


#### 4. 在线访问

   http://127.0.0.1:8081
   
### nginx部署

访问：https://gofly.sopans.com

参考支持https的部署示例 , 注意反向代理的端口号和证书地址

```php
server {
       listen 443 ssl http2;
        ssl on;
        ssl_certificate   conf.d/cert/4263285_gofly.sopans.com.pem;
        ssl_certificate_key  conf.d/cert/4263285_gofly.sopans.com.key;
        ssl_session_timeout 5m;
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
        ssl_prefer_server_ciphers on;
        #listen          80; 
        server_name  gofly.sopans.com;
        access_log  /var/log/nginx/gofly.sopans.com.access.log  main;
        location / {
                proxy_pass http://127.0.0.1:8081;
                    proxy_http_version 1.1;
                    proxy_set_header X-Real-IP $remote_addr;
                    proxy_set_header Upgrade $http_upgrade;
                    proxy_set_header Connection "upgrade";
                    proxy_set_header Origin "";
        }
}
server{
       listen 80;
        server_name  gofly.sopans.com;
        access_log  /var/log/nginx/gofly.sopans.com.access.log  main;
        location / {
                proxy_pass http://127.0.0.1:8081;
                    proxy_http_version 1.1;
                    proxy_set_header X-Real-IP $remote_addr;
                    proxy_set_header Upgrade $http_upgrade;
                    proxy_set_header Connection "upgrade";
                    proxy_set_header Origin "";
        }
}
```

### 生成文档

1. 需要先安装swag
2. 在根目录swag init -g go-fly.go
### 感谢赞助
2021年02月19日 **辉  1000元

2021年02月04日 **宏  10.24元

2021年02月03日 pony  188元

2021年01月22日 **~  1000元(多商户)

2021年01月20日 **生  8.88元

2021年01月17日 **白  8.88元

2021年01月13日 **~  500元(多商户)

2020年12月31日 **强  8.88元

2020年12月24日 **松  8.88元

2020年12月23日 **渊  10元

2020年12月16日 **彬  8.8元

2020年11月30日 **宇  88元

### 打赏作者
欢迎使用爱发电赞赏作者

https://afdian.net/@taoshihan

欢迎使用支付宝赞赏


![Image text](https://gofly.sopans.com/static/upload/2020December/9d736faeba2e9967a5dcc1c489f85541.png)

### 版权声明

当前项目仅支持个人测试使用,赞赏并联系作者后可以获取完整技术支持