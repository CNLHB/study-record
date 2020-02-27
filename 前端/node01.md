### 并发处理

- 多进程-C
- 多进程Java
- 异步IO-js
- 协程 -lua openresty go



与前端的不同

JS核心语法

前端BOM DOM

后端fs http even os buffer global process



js

```js
const { promisify } = require("util") //包装
const readFile = promisify(fs.readFile)
fs.readFile('./笔记.md', (err, data) => {
    if (err) throw err;
    console.log(data);
});
```

Buffer 开辟缓存空间

```js

```

大量if else

推到数组里面

然后for of 遍历

```js
const http = require('http')
const url = require('url')

let router = []

class Application {
    get(path, handler) {
        router.push({
            path,
            method: 'get',
            handler
        })
    }
    listen() {
        const server = http.createServer((req, res) => {
            const { pathname } = url.parse(req.url, true)
            // for (const item of router) {
            //     const { path, method, handler } = item
            //     if (pathname == path && req.method.toLowerCase() == method) {
            //         return handler(req, res)
            //     }
            // }
            return router
                .find(v => pathname === v.path && req.method.toLowerCase() == v.method)
                .handler(req,res)
        })
        server.listen(...arguments)
    }
    
}
module.exports = function createApplication(){
    return new Application()
}
```



### 网络编程

HTTP HTTPS HTTP2 websocket

![image-20191117160335498](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191117160335498.png)

一般只会应用到tcp/ip的上两层



```js
// npm i lib-qqwry
//npm包
//获取ip地址 
/**
 * @getClientIP
 * @desc 获取用户 ip 地址
 * @param {Object} req - 请求
 */
function getClientIP(req) {
    return req.headers['x-forwarded-for'] || // 判断是否有反向代理 IP
        req.connection.remoteAddress || // 判断 connection 的远程 IP
        req.socket.remoteAddress || // 判断后端的 socket 的 IP
        req.connection.socket.remoteAddress;
};
```

靠近server端叫反向代理



### 聊天IM

```js
const net = require('net')
const chatServer = net.createServer()
clientList = [] chatServer.on('connection', function (client) {
    client.write('Hi!\n');
    clientList.push(client)
    client.on('data', function (data) {
        clientList.forEach(v => {
            v.write(data)
        })
    })
})
chatServer.listen(9000)


```



### 数据持久化

对象关系映射ORM

```js
(async () => {

    // 1:N关系
    const Sequelize = require("sequelize");

    // 建立连接
    const sequelize = new Sequelize("kaikeba", "root", "example", {
        host: "localhost",
        dialect: "mysql",
    });

    const Fruit = sequelize.define("fruit", { name: Sequelize.STRING });
    const Category = sequelize.define("category", { name: Sequelize.STRING });
    Fruit.FruitCategory = Fruit.belongsToMany(Category, {
        through: "FruitCategory"
    });

    // 插入测试数据
    sequelize.sync({ force: true }).then(async () => {
        await Fruit.create(
            {
                name: "香蕉",
                categories: [{ id: 1, name: "热带" }, { id: 2, name: "温带" }]
            },
            {
                include: [Fruit.FruitCategory]
            }
        );
        // 多对多联合查询
        const fruit = await Fruit.findOne({
            where: { name: "香蕉" }, // 通过through指定条件、字段等
            include: [{ model: Category, through: { attributes: ['id', 'name'] } }]
        });
    })

})()


```



业务程序

veni,vidi,vici.我来我见我征服

keyStone  

定义数据模型==>生成对应的增删改查接口，管理界面，等等