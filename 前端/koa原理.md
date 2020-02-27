koa原理

```js
// interceptor.js
module.exports = async function(ctx, next) {
    const { res, req } = ctx;
    const blackList = ['127.0.0.1'];
    const ip = getClientIP(req);
    if (blackList.includes(ip)) {
        //出现在⿊黑名单中将被拒绝 
        ctx.body = "not allowed"; 
        //开课吧web全栈架构师
		//静态⽂文件服务koa-static
  } else {
      await next();
  } };
function getClientIP(req) {
    return ( 
 		req.headers["x-forwarded-for"] || // 判断是否有反向代理理 IP 
        req.connection.remoteAddress || // 判断 connection 的远程 IP 
        req.socket.remoteAddress || // 判断后端的 socket 的 IP
        req.connection.socket.remoteAddress
    ); }
```



部署

```bash
scp docker-compose.yml root@47.98.252.43: /root/source/ #⽂文件
scp -r mini-01 root@47.98.252.43: /root/source/     #⽂文件夹
```

git (实际⼯工作中) 

deploy插件 (debug)

```bash
npm install -g pm2 
pm2 start app.js --watch -i 2 
// watch 监听⽂文件变化 // -i 启动多少个实例例
pm2 stop all pm2 list
pm2 start app.js -i max # 根据机器器CPU核数，开启对应数⽬目的进程
关闭

pm2设置为开机启动

pm2 startup

```

 Add your own code metrics: http://bit.ly/code-metrics
 Use `pm2 logs www [--lines 1000]` to display logs
 Use `pm2 env 5` to display environement variables
 Use `pm2 monit` to monitor CPU and Memory usage www

配置process.yml

```bash
apps:
 - script : app.js
	instances: 2 
    watch  : true 
    env    : 
    	NODE_ENV: production

```

pm2 start process.yml

### nginx

```js

添加静态路路由 
server  {
    listen  80; 
     server_name loaclhost;  那个地址访问的主机
     
     location  / {
     	  root  /www/lhb/lhb/hstc-1/html; 指向的地址
          index index.html index.htm; 按顺序 
     }
    
     location ~ \.(gif|jpg|png)$ {
         root /root/source/taro-node/server/static;  配置静态资源
     }
    
    location /api {
        proxy_pass  http://127.0.0.1:3000;  代理地址
        proxy_redirect     off;
        proxy_set_header   Host             $host;
        proxy_set_header   X-Real-IP        $remote_addr;
        proxy_set_header   X-Forwarded-For 
   $proxy_add_x_forwarded_for; 	
    }
}
```



 ![nginx ååä»£çproxyåæ°è®²è§£](https://s1.51cto.com/images/blog/201808/05/c32a728954d93ee2a4e4fb59c150a15b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=) 

 ![nginx ååä»£çproxyåæ°è®²è§£](https://s1.51cto.com/images/blog/201808/05/6e19d93380daf160967ee80afd2e1b0b.png?x-oss-process=image/watermark,size_16,text_QDUxQ1RP5Y2a5a6i,color_FFFFFF,t_100,g_se,x_10,y_10,shadow_90,type_ZmFuZ3poZW5naGVpdGk=) 

查看nginx配置文件

[root@izuf60iymwle7vizt12c1nz /]# nginx -t
nginx: the configuration file /www/server/nginx/conf/nginx.conf syntax is ok
nginx: configuration file /www/server/nginx/conf/nginx.conf test is successful





### Docker

操作系统层⾯面的虚拟化技术 

隔离的进程独⽴立于宿主和其它的隔离的进程 - 容器器

GO语⾔言开发 





定制⼀一个程序NodeJS镜像

```json
{  
    "name": "myappp",
    "version": "1.0.0",
    "main": "app.js",
    "scripts": {
        "test": "echo \"Error: no test specified\" && exit 1"
    },
    "keywords": [],
    "author": "",
    "license": "ISC",
    "description": "myappp",
    "dependencies": {
        "koa": "^2.7.0"
    }
}
```

app.js

```js
const Koa = require('koa')
const app = new Koa()
app.use(ctx => {
    Math.random() > 0.8 ? abc() : ''
    ctx.body = 'Hello Docker' })
app.listen(3000, () => {
    console.log('app started at http://localhost:3000/')
})
```

```
#Dockerfile
#制定node镜像的版本
FROM node:10-alpine
#移动当前⽬目录下⾯面的⽂文件到app⽬目录下
ADD . /app/ 
#进入到app⽬目录下⾯面，类似cd
WORKDIR /app 
#安装依赖
RUN npm install
#对外暴暴露露的端⼝口
EXPOSE 3000
#程序启动脚本
CMD ["node", "app.js"]
```

# 定制镜像 docker build -t mynode .
# 运行 docker run -p 3000:3000  -d mynode

