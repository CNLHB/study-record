### React

1、不能直接修改state，没有用

2、批量执行

快速进入开发环境

网上关于介绍如何搭建React+webpack的文章很多，小编也写过一篇《一起学React | 快速搭建React+webpack 开发环境》，感兴趣的同学可以看下，但是作为初学者，小编还是建议快速进入开发环境才是最重要的。通过以下命令可以快速搭建开发环境：

npm install -g create-react-app

create-react-app demo

cd demo

npm start

安装成功后，就会自动启动浏览器，看到如下界面，是不是很简单呢？

虚拟DOM

在React中，render执行的结果得到的并不是真正的DOM节点，结果仅仅是轻量级的JavaScript对象，我们称之为virtual DOM。

虚拟DOM是React的一大亮点，具有batching(批处理)和高效的Diff算法。这让我们可以无需担心性能问题而”毫无顾忌”的随时“刷新”整个页面，由虚拟 DOM来确保只对界面上真正变化的部分进行实际的DOM操作。

React 从来没有说过 “React 比原生操作 DOM 快”。React给我们的保证是，在不需要手动优化的情况下，它依然可以给我们提供过得去的性能。

React掩盖了底层的 DOM 操作，可以用更声明式的方式来描述我们目的，从而让代码更容易维护。

不是框架

相对Angular、Ember等框架，React显得很轻，只能算一个函数库，React专注让用户通过组件构建用户界面。关于服务器数据交互，动画效果的实现都是通过第三方插件实现，所以你能很轻松的把jquery等相关插件集成。

HTML，CSS，JS构成组件

多年来，我们一直将HTML,CSS,JS分开写，放在不同的文件夹里，维护这些文件，大家是什么感受呢？

我们写React组件时，虽然也能分开写，但是小编还是建议大家写在一起，虽然这样写很奇怪，但是习惯后，你会体会到这样写逻辑更加清晰，更加符合组件化的思想。

仅仅是Javascript

不像其他框架，我们不用去学习Typescript或者特有模板语法糖，我们依然能很轻松的使用Javascript完成相关的逻辑，减轻了学习压力，例如以下代码：

```
<select value={this.state.value} onChange={this.handleChange}>    {somearray.map(element => <option value={element.value}>        {element.text}</option>)}</select>
```

JSX

React 使用 JSX 来替代常规的 JavaScript。

JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。

我们不需要一定使用 JSX，但它有以下优点：

1. JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
2. 它是类型安全的，在编译过程中就能发现错误。
3. 使用 JSX 编写模板更加简单快速。

JSX示例代码入下，看起来类似 HTML：

```
ReactDOM.render(<h1>Hello, world!</h1>,document.getElementById('example'));
```

JavaScript 表达式

```
ReactDOM.render(<div> <h1>{1+1}</h1> </div> ,document.getElementById('example'));
```

样式

```
var myStyle = {fontSize: 100, color: '#FF0000'};ReactDOM.render(<h1 style = {myStyle}>前端达人</h1>,document.getElementById('example'));
```

注释

```
ReactDOM.render(<div>  <h1>前端达人</h1>        {/*注释...*/}</div>,document.getElementById('example'));
```

数组

```
var arr =    [  <h1>菜鸟教程</h1>,<h2>学的不仅是技术，更是梦想！</h2>    ];ReactDOM.render( <div>{arr}</div>,document.getElementById('example'));
```

state与props

state 和 props 主要的区别在于 props 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

使用 Props

```
var HelloMessage = React.createClass({render: function() {return <h1>Hello {this.props.name}</h1>;}});ReactDOM.render(<HelloMessage name="Runoob" />,document.getElementById('example'));
```

使用state

React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。

以下实例中创建了 LikeButton 组件，getInitialState 方法用于定义初始状态，也就是一个对象，这个对象可以通过 this.state 属性读取。当用户点击组件，导致状态变化，this.setState 方法就修改状态值，每次修改以后，自动调用 this.render 方法，再次渲染组件。

```
<script type="text/babel">    var LikeButton = React.createClass({    getInitialState: function() {return {liked: false};},    handleClick: function(event) {this.setState({liked: !this.state.liked});},    render: function() {var text = this.state.liked ? '喜欢' : '不喜欢';return (<p onClick={this.handleClick}>    你<b>{text}</b>我。点我切换状态。</p>    );}});    ReactDOM.render(<LikeButton />,document.getElementById('example')    );</script>
```



组件生命周期

组件的生命周期可分成三个状态：

Mounting：已插入真实 DOM

Updating：正在被重新渲染

Unmounting：已移出真实 DOM

生命周期的方法有：

1. componentWillMount 在渲染前调用,在客户端也在服务端。
2. componentDidMount : 在第一次渲染后调用，只在客户端。之后组件已经生成了对应的DOM结构，可以通过this.getDOMNode()来进行访问。 如果你想和其他JavaScript框架一起使用，可以在这个方法中调用setTimeout, setInterval或者发送AJAX请求等操作(防止异部操作阻塞UI)。
3. componentWillReceiveProps 在组件接收到一个新的prop时被调用。这个方法在初始化render时不会被调用。
4. shouldComponentUpdate 返回一个布尔值。在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
   可以在你确认不需要更新组件时使用。
5. componentWillUpdate在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。
6. componentDidUpdate 在组件完成更新后立即调用。在初始化时不会被调用。
7. componentWillUnmount在组件从 DOM 中移除的时候立刻被调用。

React 表单与事件

在实例中小编设置了输入框 input 值value = {this.state.data}。在输入框值发生变化时我们可以更新 state。我们可以使用 onChange 事件来监听 input 的变化，并修改 state。

```
var HelloMessage = React.createClass({getInitialState: function() {return {value: 'Hello Runoob!'};    },handleChange: function(event) {this.setState({value: event.target.value});    },render: function() {var value = this.state.value;return(<div><input type="text" value={value} onChange={this.handleChange} /><h4>{value}</h4></div>)  }});ReactDOM.render(  <HelloMessage />,  document.getElementById('example'));
```

React Refs

React 支持一种非常特殊的属性 Ref ，你可以用来绑定到 render() 输出的任何组件上。

这个特殊的属性允许你引用 render() 返回的相应的支撑实例（ backing instance ）。这样就可以确保在任何时间总是拿到正确的实例。

你可以通过使用 this 来获取当前 React 组件，或使用 ref 来获取组件的引用，实例如下：

```
var MyComponent = React.createClass({handleClick: function() {// 使用原生的 DOM API 获取焦点        this.refs.myInput.focus();    },render: function() {//  当组件插入到 DOM 后，ref 属性添加一个组件的引用于到 this.refs    return (<div><input type="text" ref="myInput" /><input    type="button" value="点我输入框获取焦点"    onClick={this.handleClick}            /></div>        );    }});ReactDOM.render( <MyComponent />,document.getElementById('example'));
```



React 组件 API

关于 React 组件 API 常用的有以下7个：

1. 设置状态：setState
2. 替换状态：replaceState
3. 设置属性：setProps
4. 替换属性：replaceProps
5. 强制更新：forceUpdate
6. 获取DOM节点：findDOMNode
7. 判断组件挂载状态：isMounted

关于API的介绍，限于文章篇，就不在这里介绍了，感兴趣的同学可以查看以下链接：

http://itbilu.com/javascript/react/EkACBdqKe.html

React AJAX

由于React没有提供ajax服务端数据的相关请求，你可以使用第三方库来实现Xhr、Fetch、Superagent、Axios、Jquery。





React 组件的数据可以通过 componentDidMount 方法中的 Ajax 来获取，当从服务端获取数据库可以将数据存储在 state 中，再用 this.setState 方法重新渲染 UI。



当使用异步加载数据时，在组件卸载前使用 componentWillUnmount 来取消未完成的请求。



以下实例演示了获取 Github 用户最新 gist 共享描述:

```js
var UserGist = React.createClass({  getInitialState: function() {return {username: '',lastGistUrl: ''    };  },componentDidMount: function() {this.serverRequest = $.get(this.props.source, function (result) {var lastGist = result[0];this.setState({username: lastGist.owner.login,lastGistUrl: lastGist.html_url                });        }.bind(this)); },componentWillUnmount: function() {this.serverRequest.abort();        },render: function() {return (<div> {this.state.username} 用户最新的 Gist 共享地址：<a href={this.state.lastGistUrl}>                {this.state.lastGistUrl}</a></div>        );  }});ReactDOM.render(<UserGist source="https://api.github.com/users/octocat/gists" />,    mountNode);
```

你可能不需要Redux

首先明确一点，Redux 是一个有用的架构，但不是非用不可。事实上，大多数情况，你可以不用它，只用 React 就够了。

曾经有人说过这样一句话。

"如果你不知道是否需要 Redux，那就是不需要它。"

Redux 的创造者 Dan Abramov 又补充了一句。

"只有遇到 React 实在解决不了的问题，你才需要 Redux 。"

简单说，如果你的UI层非常简单，没有很多互动，Redux 就是不必要的，用了反而增加复杂性。

#### react生命周期

![image-20191112191326213](C:\Users\TR\AppData\Roaming\Typora\typora-user-images\image-20191112191326213.png)



```js
react生命周期及其它注意事件
/** react中组件里的render函数可以找到组件的this
* 在render方法里调用函数时函数是可以找到this的，react中组件里的方法函数里不能找到组件的this需要在render中绑定this,具体应该是点击事件里的函数
* react中状态管理放在组件的constructor里管理
* setState（）设置state的,就会重新渲染render方法重新渲染
* 插值不能用for和if,可以用map
* 组件中必须继承react中的component,组件的首字母必须是大写的
* 生命周期分三个阶段，一个挂载阶段，一个是更新阶段，一个是卸载阶段
* 挂载阶段：constructor()构造函数，在创建组件的时候调用一次
* 挂载：componentWillMount()在组件即将被挂载的时候调用一次
* 一些组件启动的动作，包括像 Ajax 数据的拉取操作、一些定时器的启动等，就可以放在 componentWillMount 里面进行，例如 Ajax：
* 挂载:render()渲染
* 挂载：componentDidMount()在组件被挂载完成的时候调用一次，可以在这里使用refs,例如动画的启动
* 卸载阶段：(组件从页面中移除)* componentWillUnmount即将卸载没有卸载完成,组件对应的 DOM 元素从页面中删除之前调用
* 更新阶段：(注意：组件一但建成进入更新阶段后不会再走constructor方法里了)
* “更新阶段”。说白了就是 setState 导致 React.js 重新渲染组件并且把组件的变化应用到 DOM 元素上的过程，这是一个组件的变化过程。* React.js 当中可以直接通过 setState 的方式重新渲染组件，渲染的时候可以把新的 props 传递给子组件，从而达到页面更新的效果。
* componentWillReceiveProps(nextProps)组件从父组件接收到新的 props 之前调用。,父组件的更新会触发子组件的这个函数,nextProps父组件更新的时候带来的数据
* shouldComponentUpdate(nextProps,nextState),你可以通过这个方法控制组件是否重新渲染。如果返回 false 组件就不会重新渲染。是否需要重新渲染，Return false/true
* componentWillUpdate(nextProps,nextState),即将更新,组件开始重新渲染之前调用。
* render渲染
* componentDidUpdate(prevProps,PrevState)完成更新,组件重新渲染并且把更改变更到真实的 DOM 以后调用
* 尽量不要在render里去改状态(setState)，尽量在相应的生命周期里去改
*** 
*/
```

 

 

react的redux共分几个部分各个部分的原理如下：

**provider :** 它做的事情就是与context建立联系，把传进来的store放到context里，并把所有组件当成自己的子组件，这样所有组件都可以经过connect之后都可以取到react-redux里的值( `Provider` 做的事情也很简单，它就是一个容器组件，会把嵌套的内容原封不动作为自己的子组件渲染出来。它还会把外界传给它的 `props.store` 放到 context，这样子组件 `connect` 的时候都可以获取到。)

**store:** 它就像是一个指挥部，会暴漏出来所有供外使用的方法，里面会写好各方法的处理逻辑，及调用顺序( getState, dispatch, subscribe)

**dispatch:** 它是处理state数据，也就是你传进来的想要改变的state里的值也就是形参action，它会把你传进来的action交给reducer去处理，reducer处理后调用渲染方法根据最新数据渲染页面(要改哪些数据以及指令类型)

**reducer:**它是根据action(也是你的指令的类型，它根据你传的类型去判断 它要干啥，要改哪个数据)去判断哪此数据需要更新(把要更新的数据复制出来一份去替换旧的，这样对象地址就不一样了，可以判断旧数据是否更新)，从而反回最新的数据，也就是根据浅拷贝的原因，把想改变的数据用新对象替换，如果不用新对象替换引用类型地址没有变视为不更新

**subscribe:**渲染页面，也就是里面调用的setState，调用它后，就会调用render方法重新渲染，根据最新的数据

**connect(高阶组件):通过高阶组件与原生的context通信，**它就是将最新的数据绑定要传进来的组件上，使被传进来的组件可以取到最新的state数据，也就是所谓的被包装组件

`Connect` 会去 context 里面取出 store。把 store 里面的数据取出来通过 `props` 传给 传进来的函数

```
connect
connect中mapStateTopProps参数的作用:(高阶组件的入参)
mapStateTopProps 相当于告知了 Connect 应该如何去 store 里面取数据，然后可以把这个函数的返回结果传给被包装的组件,还需要告诉高级组件我们需要什么数据，高阶组件才能正确地去取数据。
connect中mapDispatchToProps参数的作用:
来告诉它我们的组件需要如何触发 dispatch。我们把这个参数叫 mapDispatchToProps
 
```

 

2018年9月12日 学习react总结 
1、在setState里更改state里的值，如何在当前组件，当前方法里取到最新的值: 
   (1)setState里加入第二个参数，为回调函数，在此回调内可以取到最新值 
   (2)在render生拿周期里直接取值 
   (3)加setTimeOut 
2、不能在子组件里直接改props里的值，解决办法可以存在变量里，或在父组件里改 
3、使用map之前进行非空判断以防报错 
4、写行间样式用鸵峰式写法 
5、在子组件使用props里的值时要先定义下初始值

