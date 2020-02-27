### Koa实战 - Restful API

Koa实战 - Restful API

 课程目标

 编写RESTful API 

文件上传

 表单校验

 图形验证码

 发送短信

 案例：用户注册

### 目标 
掌握Koa中编写Restful风格API 掌握Koa中文件上传、表单验证、图形验证码、发送短信等常见任务

### 编写RESTful API

编写RESTful API 
Representational State Transfer翻译过来是"表现层状态转化"，它是一种互联网软件的架构原则。因此复合 REST风格的Web API设计，就称它为RESTful API

 RESTful特征：

 每一个URI代表一种资源(Resources)，比如： http://kaikeba.com/courses ；

 客户端和服务器之间，传递这种资源的某种表现层，比如： http://kaikeba.com/courses/web ；

 客户端通过HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"，比如：POST http://kaikeba.com/courses URL设计 HTTP动词：

表示一个动作 GET：读取（Read） 

POST：新建（Create） 

PUT：更新（Update） 

PATCH：更新（Update），部分更新

DELETE：删除（Delete） 

宾语：表示动作的目标对象 是一个名词

### 状态码 状态码要精确： 

1xx ：相关信息 

2xx ：操作成功 

3xx ：重定向 

4xx ：客户端错误 

5xx ：服务器错误 

### 服务器响应 

返回JSON

```js

//不推荐 HTTP/1.1 200 OK Content-Type: application/json
 
{  "ok":0,  "data": { "error": "期待2个参数，实际收到1个。" } }


//推荐 HTTP/1.1 400 Bad Request Content-Type: application/json
 
{  "error": "不合法的附件",  "detail": { "uname": "用户名为必填项" } }
```





### 解决跨域： npm i koa2-cors

```js
var Koa = require('koa');
var cors = require('koa2-cors');
 
var app = new Koa();
app.use(cors());
```

### 文件上传 
安装koa-multer：

 npm i koa-multer -S 

配置：./routes/users.js

```js
const upload = require("koa-multer")({ dest: "./public/images" });
router.post("/upload", upload.single("file"), ctx => {
    console.log(ctx.req.file);
    // 注意数据存储在原始请求中
    console.log(ctx.req.body);
    // 注意数据存储在原始请求中
    ctx.body = "上传成功";
});
```

### 表单校验 
安装koa-bouncer： npm i -S koa-bouncer 配置：app.js

```js
// 为koa上下文扩展一些校验方法
app.use(bouncer.middleware());


router.post("/", ctx => {  try {
    // 校验开始 
    ctx 
        .validateBody("uname")
        .required("要求提供用户名")
        .isString()
        .trim() 
        .isLength(6, 16, "用户名长度为6~16位");
 


```





### 图形验证码 

安装trek-captcha：

 npm i trek-captcha -S

使用：./routes/api.js

```js
const captcha = require("trek-captcha");
router.get("/captcha", async ctx => {
    const { token, buffer } = await captcha({ size: 4 });
    ctx.body = buffer;
});
```

图片显示，upload-avatar.html

```js
<!-- 验证码 -->
 <img src="/api/captcha" id="captcha" /> 
<script>document.getElementById('captcha').onclick = function() {
     captcha.src = "/users/captcha?r=" + Date.now();
 };
</script>
```

发送短信 
秒滴短信API

 安装依赖： npm i -S moment md5 axios 

接口编写，./routes/api.js

```js
router.get("/sms", async function(ctx) {
  // 生成6位随机数字验证码
    let code = ran(6);
 
  // 构造参数
   const to = ctx.query.to; // 目标手机号码
   const accountSid = "3324eab4c1cd456e8cc7246176def24f"; // 账号id
   const authToken = "b1c4983e2d8e45b9806aeb0a634d79b1"; // 令牌
   const templateid = "613227680"; // 短信内容模板id
   const param = `${code},1`; // 短信参数
   const timestamp = moment().format("YYYYMMDDHHmmss");
   const sig = md5(accountSid + authToken + timestamp); // 签名
   try {    // 发送post请求
       const resp = await axios.post(      	          "https://api.miaodiyun.com/20150822/industrySMS/sendSMS",
 qs.stringify({ to, accountSid, timestamp, sig, templateid, param }), 
  { headers: { "Content-Type": "application/x-www-form-urlencoded" } }
  );
      if (resp.data.respCode === "00000") {
          // 短信发送成功，存储验证码到session，过期时间1分钟
          const expires = moment()
          	.add(1, "minutes")
          	.toDate();
          ctx.session.smsCode = { to, code, expires };
                ctx.body = {ok:1}
      } else {
          ctx.body = {ok:0, message: resp.data.respDesc}
      }  } catch (e) {
          ctx.body = {ok:0, message: e.message}
      }
});
```

![image-20191118183505193](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191118183505193.png)

![image-20191118183531096](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191118183531096.png)





```js

//给所有请求加中间件
//1.在框架和插件中使用中间件

//编写中间件
//我们先来通过编写一个简单的中间件，来看看中间件的写法。

// app/middleware/middlewareOne.js

// app/middleware/middlewareOne.js
module.exports = (options, app) => {
　　return async function middlewarreone(ctx, next) {
　　　　const url = ctx.request.url;
　　　　await next();
　　　　ctx.body = `获取到的ip是:${url}`;
　　}
};
// config/config.default.js
exports.middleware = ['middlewareOne']; // 数组的顺序为中间件执行的顺序


//给单个请求加中间件
'use strict';
 
/**
 * @param {Egg.Application} app - egg application
 */
module.exports = app => {
  const {
    router,
    controller
  } = app;
  const isUrl = app.middleware.middlewarreone({params: '888',});
  router.get('/', controller.home.index);
  router.post('/login', controller.home.login);
  router.post('/data',isUrl, controller.data.index);
  router.post('/upload', controller.upload.upload);
 
  router.get('/search', controller.data.search);
};
```

短信服务

```js
/*
 * @Descripttion:
 * @version: 0.1.0
 * @Author: Seven
 * @Date: 2019-09-15 10:34:59
 * @LastEditors: sueRimn
 * @LastEditTime: 2019-09-16 17:39:10
 */

module.exports = {
  dbs: "mongodb://47.101.196.193:27017/studt",
  redis: {
    get host() {
      return "127.0.0.1";
    },
    get port() {
      return 6379;
    }
  },
  //1
  // jyiclvcdonvibaeb
  //2
  // ekhmqtayqxmxbaag
  //3授权码
  //vzhyhrzqibsxfdhb
  smtp: {
    get host() {
      return "smtp.qq.com";
    },
    get user() {
      return "1348844909@qq.com";
    },
    get pass() {
      return "vzhyhrzqibsxfdhb";
    },
    get code() {
      return () => {
        return Math.random()
          .toString(16)
          .slice(2, 6)
          .toUpperCase();
      };
    },
    get expire() {
      return () => {
        return new Date().getTime() + 60 * 60 * 1000;
      };
    }
  }
};

//使用
router.post("/verify", async (ctx, next) => {
  let username = ctx.request.body.username;
  console.log(username,ctx.request.body.email)
  const saveExpire = await Store.hget(`nodemail:${username}`, "expire");
  // saveExpire && new Date().getTime() - saveExpire < 0
  if (false) {
    ctx.body = {
      code: -1,
      msg: "验证请求过于频繁，1分钟内1次"
    };
    return false;
  }


  let transporter = nodeMailer.createTransport({
    service: "qq",
    host:465,
    auth: {
      user: Email.smtp.user,
      pass: Email.smtp.pass
    }
  });
  let ko = {
    code: Email.smtp.code(),
    expire: Email.smtp.expire(),
    email: ctx.request.body.email,
    user: ctx.request.body.username
  };
  let  em=  `"认证邮件" <${Email.smtp.user}>`
  let mailOptions = {
    from: em,
    to: ko.email,
    subject: "《JAVA大数据》注册码",
    html: `您在《慕课网JAVA大数据课程实战》课程中注册，您的邀请码是${ko.code}`
  };


  await transporter.sendMail(mailOptions, (error, info) => {
    if (error) {
        ctx.body = {
          code: -1,
          msg: "验证码已发送，可能会有延时，有效期1分钟"
        };
      return console.log(error);
    } else {
      Store.hmset(
        `nodemail:${ko.user}`,
        "code",
        ko.code,
        "expire",
        ko.expire,
        "email",
        ko.email
      );
    }
  });

  ctx.body = {
    code: 0,
    msg: "验证码已发送，可能会有延时，有效期1分钟"
  };
});
```

