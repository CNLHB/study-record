## JS

1. JS语言的特点？和C语言、Java比较

   JS是弱类型的语言，

   单线程的解释型语言，不需要预编辑

   面向对象，

   没有Node之前只能运行在浏览器

   #### 比较

   C、Java都是强类型语言、多线程，需要预编译

   C面向过程，

   Java面向对象

   运行在服务端

2. 原始数据类型有哪几种？null对象嘛？

   原始数据类型有7种

   number、string、boolean，symbol、undefined、null、bigint

   null不是对象，但是用typeof判断是“object”

3. 对象类型和原始类型有什么不同之处？函数参数是对象会发生什么问题？

   存储的方式不同，

   原始值

   是存储在栈（stack）中的简单数据段，也就是说，它们的值直接存储在变量访问的位置

   引用值

   是存储在堆（heap）中 对象，也就是说，存储在变量处的值是一个指针（point），指向存储对象的内存处。

   函数参数是对象时会发生地址的引用，当修改传递的对象时，原对象也会发生改变

4. typeof是否能正确判断类型？instanceof能正确判断对象的原理是什么？

   typeof不能正确判断数据类型，只能判断大多数基本数据类型，null不能正确判断，对引用数据类型无法正确判断。

   Instanceof运算符的第一个变量是一个对象，暂时称为A；第二个变量一般是一个函数，暂时称为B。

   Instanceof的判断规则是：沿着A的__proto__这条线来找，同时沿着B的prototype这条线来找，如果两条 线能找到同一个引用，即同一个对象，那么就返回true。如果找到终点还未重合，则返回false。

5. 转换规则：基本数据类型转换为布尔值？基本数据类型转换为数字？基本数据类型和引用数据类型转换为字符

   串？

   == vs ===

   1. 首先会判断两者类型是否**相同**。相同的话就是比大小了
   2. 类型不相同的话，那么就会进行类型转换
   3. 会先判断是否在对比 `null` 和 `undefined`，是的话就会返回 `true`
   4. 判断两者类型是否为 `string` 和 `number`，是的话就会将字符串转换为 `number`
   5. 判断其中一方是否为 `boolean`，是的话就会把 `boolean` 转为 `number` 再进行判断
   6. 判断其中一方是否为 `object` 且另一方为 `string`、`number` 或者 `symbol`，是的话就会把 `object` 转为原始类型再进行判断
   7. ![img](file:///D:/%E6%A1%8C%E9%9D%A2%E6%96%87%E4%BB%B6/Web%20%E5%89%8D%E7%AB%AF%E9%9D%A2%E8%AF%95%E6%8C%87%E5%8D%97%E4%B8%8E%E9%AB%98%E9%A2%91%E8%80%83%E9%A2%98%E8%A7%A3%E6%9E%90/%E6%8E%98%E9%87%91%E5%B0%8F%E5%86%8C%E5%89%8D%E7%AB%AF%E9%9D%A2%E8%AF%95%E4%B9%8B%E9%81%93/%E5%89%8D%E7%AB%AF%E9%9D%A2%E8%AF%95%E4%B9%8B%E9%81%93/3-JS%20%E5%9F%BA%E7%A1%80%E7%9F%A5%E8%AF%86%E7%82%B9%E5%8F%8A%E5%B8%B8%E8%80%83%E9%9D%A2%E8%AF%95%E9%A2%98%EF%BC%88%E4%BA%8C%EF%BC%89_files/167c4a2627fe55f1)
   
   

## CSS

1. CSS的全称？加载CSS的方式

   （Cascading Style Sheets ）层叠样式表

   加载方式

   一、在HTML中直接写在标签的style属性内

   二、在style标签中嵌入到HTML中

   三、通过link标签引入

2. -wekit-、-moz-、-ms-、-o-具体指什么？

   为解决浏览器兼容性问题，一些新的属性要加上特定的浏览器前缀

   -webkit代表safari、chrome私有属性

   -moz-火狐

   -ms代表IE浏览器私有属性

   -o-  代表opera浏览器私有属性

3. CSS选择器的优先级是如何计算的？

   按照选择器来叠加计算，根据选择器权重相加，ID选择器为100，类名10，标签1

4. 盒子模型？IE和标准盒子的区别？

   css盒子模型 又称为框模型（Box Model），包含了元素内容（content）、内边距（padding）、边框（border）、外边距（margin）几个要素

   标准盒模型：margin、border、padding、content,  **width  = content **

   IE 盒子模型的范围也包括 margin、border、padding、content，**width  = content + padding + border **

5. 请阐述块级格式化上下文及其工作原理,那些设置可以生成BFC，BFC的应用？

   创建了一个独立布局，盒子里面的子元素的样式不会影响到外面的元素

   ##### 生成BFC

   ```js
   1）根元素
   2）float属性不为none
   3）position不为static和relative
   4）overflow不为visible
   5）display为inline-block, table-cell, table-caption, flex, inline-flex
   ```

   

   ##### BFC应用

   ```js
   1）防止外边距重叠。
   2）清除浮动的影响
   3）防止文字环绕
   ```

   ##### IFC
   
   ![image-20200318180735512](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20200318180735512.png)

## HTML

1. HTML的全称是什么？在前端中的作用？

   HTML 指的是[超文本标记语言](https://www.baidu.com/s?wd=超文本标记语言&tn=SE_PcZhidaonwhc_ngpagmjz&rsv_dl=gh_pc_zhidao) (Hyper Text Markup Language)

   HTML描述网页的结构，

2. DOCTYPE 有什么用？

   DOCTYPE也就是 *document type* ，文档类型。

   <!DOCTYPE>并不是一个html标签，它被声明在html文档的第一行，用来告诉web浏览器，我们写的这个html文件基于那个html版本，从而浏览器根据不同版本的规则来编写。
    <!DOCTYPE>必须在文档第一行来声明。如果没有声明，或者声明错误，则浏览器会以怪异模式/兼容模式来解析

   在HTML4和HTML5中，声明方式不同。
   在HTML4.01中有三种声明方式，
   **HTML 4.01 Strict**

   **HTML 4.01 Transitional**

   **HTML 4.01 Frameset**

   

3. div、p、span、h1、input、img、ul、li、form、table、

   5个H5。nav、article、header、section、footer

4. meta标签的作用？

   meta标签的可选属性提到了三个，分别是

   http-equiv、name和scheme，新近又出了一个property属性，

   http-equiv属性是添加http头部内容，对一些自定义的或者需要额外添加的发送到浏览器中的http头部内容，我们就可以是使用这个属性。

   #### http-equiv

   ```html
   <meta http-equiv="参数" content="具体的参数值">
   1、用以说明网页制作所使用的文字以及语言。
   <meta http-equiv="charset" content="iso-8859-1">
   2、设置网页的过期时间，一旦过期则必须到服务器上重新获取。需要注意的是必须使用GMT时间格式
   <meta http-equiv="expires" content="31 Dec 2018">
   3、用于设定网页在特定时间内自动刷新并转到新页面
   <meta http-equiv="refresh" contect="5;url=https://www.deannhan.cn">
   4、用于设定禁止浏览器从本地计算机的缓存中访问页面内容
   <meta http-equiv="pragma" contect="no-cache">
   5、用于设定强制页面在窗口中以独立页面显示，防止自己的网页被别人当作一个frame页调用。
   <meta http-equiv="windows-target" contect="_top">
   6、用于设定一个自定义cookie，如果网页过期，那么存盘的cookie将被删除，注意必须使用GMT的时间格式。
   <meta http-equiv="Set-Cookie" content="name=deanhan; expires=Friday,12-Jan-2018 18:18:18 GMT; path=/">
   7、用于设定页面使用的字符集。
   <meta http-equiv="content-Type" content="text/html; charset=utf-8">
   8、用于设定页面进入和离开时的过渡效果，注意被添加的页面不能在一个frame中。
   <meta http-equiv="page-enter" contect="revealTrans(duration=10,transtion=23)">
   <meta http-equiv="page-exit" contect="revealTrans(duration=20，transtion=6)">
   
   ```

   

   #### name属性

   ```html
   <meta name="参数" content="具体的参数值">
   1、keywords
   keywords用来告诉搜索引擎你网页的关键字是什么。
   <meta name="keywords" content="个人博客,个人网站">
   2、description
   description用来告诉搜索引擎你的网站主要内容。
   <meta name="description" content="个人描述">
   3、robots
   robots用来告诉搜索机器人哪些页面需要索引，哪些页面不需要索引。
   <meta name="robots" content="none">
   4、author
   author标注网页的作者
   <meta name="author" content="826554003@qq.com">
   5、generator
   generator用于说明网站的采用的什么软件制作。
   <meta name="generator" content="Sublime"/>
   6、copyright
   copyright用于说明网站版权信息。
   <meta name="copyright" content="xxx">
   7、viewport
   viewport用于说明移动端网站的宽高缩放比例等信息
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   其中content的距离参数如下：
   
   1) width 宽度(数值/device-width)
   
   2) height 高度(数值/device-height)
   
   3) initial-scale 初始缩放比例
   
   4) maximum-scale 最大缩放比例
   
   5) minimum-scale 最小缩放比例
   
   6) user-scalable 是否允许用户缩放(yes/no)
   8、renderer
   用于告诉浏览器使用什么内核进行解析
   <meta name="renderer" content="webkit">
   
   
   ```

   #### scheme

   用于指定要用来翻译属性值的方案。此方案应该在由 标签的 profile 属性指定的概况文件中进行了定义。

   

5. 如何提供包含多种语言内容的页面？在设计开发多语言网站时，需要留心哪些事情？

   解决方案：

   1、简单：每个语言一个网站，还要注意分离用户系统

   优点：简单解决。后顾无忧~

   缺点：维护复杂，制作周期长~

   2、简单的调用谷歌翻译整个页面

   优点：简单、方便。

   缺点：偶尔被墙、机器翻译总是有点语法用词不通顺

   3、真正实现网站的多语言设计

   优点：基本上解决以上所有问题

   缺点：设计复杂，实现麻烦，有些情况下得不偿失
   原文链接：https://blog.csdn.net/seoyundu/article/details/82081265

clone

```js
function deepClone(obj) {
  function isObject(o) {
    return (typeof o === 'object' || typeof o === 'function') && o !== null
  }

  if (!isObject(obj)) {
    //throw new Error('非对象')
     return  obj
    
  }

  let isArray = Array.isArray(obj)
  let newObj = isArray ? [...obj] : { ...obj }
  Reflect.ownKeys(newObj).forEach(key => {
    newObj[key] = isObject(obj[key]) ? deepClone(obj[key]) : obj[key]
  })

  return newObj
}

let obj = {
  a: [1, 2, 3],
  b: {
    c: 2,
    d: 3
  }
}
let newObj = deepClone(obj)
newObj.b.c = 1
console.log(obj.b.c) // 2
```



### Webpack gulp 的区别

## Webpack

[Webpack](https://github.com/webpack/webpack) 是当下最热门的前端资源模块化管理和打包工具。它可以将许多松散的模块按照依赖和规则打包成符合生产环境部署的前端资源。还可以将按需加载的模块进行代码分隔，等到实际需要的时候再异步加载。通过 loader的转换，任何形式的资源都可以视作模块，比如 CommonJs 模块、AMD 模块、ES6 模块、CSS、图片、JSON、Coffeescript、LESS 等。

## Gulp和Webpack功能实现对比

简单介绍了一下Gulp和Webpack的概念性的问题和大环境，接下来进入本文的主题，对比一下Gulp和Webpack的优缺点。将从基本概念、启动本地Server、sass/less预编译、模块化开发、文件合并与压缩、mock数据、版本控制、组件控制八个方面对Gulp和Webpack进行对比。

## 基本概念

首先从概念上，我们可以清楚的看出，Gulp和Webpack的侧重点是不同的。

Gulp侧重于前端开发的 **整个过程** 的控制管理（像是流水线），我们可以通过给gulp配置不通的task（通过Gulp中的gulp.task()方法配置，比如启动server、sass/less预编译、文件的合并压缩等等）来让gulp实现不同的功能，从而构建整个前端开发流程。

Webpack有人也称之为 **模块打包机** ，由此也可以看出Webpack更侧重于模块打包，当然我们可以把开发中的所有资源（图片、js文件、css文件等）都可以看成模块，最初Webpack本身就是为前端JS代码打包而设计的，后来被扩展到其他资源的打包处理。Webpack是通过loader（加载器）和plugins（插件）对资源进行处理的。

另外我们知道Gulp是对整个过程进行控制，所以在其配置文件（gulpfile.js）中配置的每一个task对项目中 **该task配置路径下所有的资源** 都可以管理



### 文件上传

1. 选择文件 file input  accept="image/*"标签

```
 客服端
 FormData数据格式 file
 ajax请求 POST
 传递给服务器 当前文件的BASE64编码（流信息）
 服务端
 接收到客服端传递的file文件
 把文件存储地址返回给客服端
 服务端接受到BASE64信息，吧BASE64转换成具体的格式存储
 
```

2. 创建ajax Content

   ```js
   let fromData = new FromData()
   Content-type: mutilpart/from-data
   Content-type: application/json;charset=utf-8
   
   fromData.append('chunk',file)//追加
   new mutilparty.From().parse()
   
   
   function ajax(method, url, data, callback, flag) {
       //创建ajax对象；
       var xhr = null;
       //非IE浏览器
       if (window.XMLHttpRequest) {
           xhr = new XMLHttpRequest();
   
       } else {
           //兼容IE
           xhr = new ActiveXObject('Microso.XMLHttp');
   
       }
       method = method.toUpperCase();
       if (method == 'GET') {
           xhr.open(method, url + '?' + data, flag);
           xhr.send();
       } else {
           xhr.open(method, url, flag);
           xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");
           xhr.send(data);
       }
       xhr.onreadystatechange = function() {
   
           if (xhr.readyState == 4 && xhr.status == 200) {
   
               callback(JSON.parse(xhr.response));
   
           }
   
       }
   
   }
   
   BASE64
   let fileRead = new FileReader()
   fileRead.readAsDataURL()
   fileRead.onload= function(EV){
       EV.TARGET.RESULT  //BASE64
   }
   
   
   ```

   

3. 切片处理 File对象 Blob.slice

   把大文件切片化 ， HTTP可以多个并发传递

    等五个都上传完，在向服务器发送合并图片的请求

   ```
   xhr.upload.onprogress = setProgress;上传进度
   function setProgress(event) {
             // event.total是需要传输的总字节，event.loaded是已经传输的字节。如果event.lengthComputable不为真，则event.total等于0
             if (event.lengthComputable) {//
                 loaded = event.loaded
                 total = event.total
                 var complete = (event.loaded / event.total * 100).toFixed(1);
                 progress.innerHTML = Math.round(complete) + "%";
                 progress.style.width = complete + '%';
             }
   ```

   

