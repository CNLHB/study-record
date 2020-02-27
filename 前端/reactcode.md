```js

import React, { Component } from "react";

export default class StateTest extends Component {
  state = {
    counter: 1
  };

  componentDidMount() {
    //   请不要直接修改状态值
    //   this.state.counter += 1;

    // 2.批量执行
    // this.setState(obj, cb)
    // this.setState(fn, cb)
    this.setState(prevState => ({
      counter: prevState.counter + 1
    }));

    this.setState(prevState => ({
      counter: prevState.counter + 1
    }));

    this.setState(prevState => ({
      counter: prevState.counter + 1
    }));
  }

  render() {
    return <div>{this.state.counter}</div>;
  }
}

```

```js
import React, { Component } from "react";
export default class Lifecycle extends Component {
  constructor(props) {
    super(props);
    // 常用于初始化状态
    console.log("1.组件构造函数执行");
  }
  componentWillMount() {
    // 此时可以访问状态和属性，可进行api调用等
    console.log("2.组件将要挂载");
  }
  componentDidMount() {
    // 组件已挂载，可进行状态更新操作
    console.log("3.组件已挂载");
  }
  componentWillReceiveProps() {
    // 父组件传递的属性有变化，做相应响应
    console.log("4.将要接收属性传递");
  }
  shouldComponentUpdate() {
    // 组件是否需要更新，需要返回布尔值结果，优化点
    console.log("5.组件是否需要更新？");
    return true;
  }
  componentWillUpdate() {
    // 组件将要更新，可做更新统计
    console.log("6.组件将要更新");
  }
  componentDidUpdate() {
    // 组件更新
    console.log("7.组件已更新");
  }
  componentWillUnmount() {
    // 组件将要卸载, 可做清理工作
    console.log("8.组件将要卸载");
  }
  render() {
    console.log("组件渲染");
    return <div>生命周期探究</div>;
  }
}

```

```js
import React from "react";

// 函数类型的组件
export function Welcome1(props) {
  return <div>Welcome1, {props.name}</div>;
}

// 基于类的组件
export class Welcome2 extends React.Component {
  render() {
    return <div>Welcome2, {this.props.name}</div>;
  }
}

```

```js
import React, { Component } from 'react'

export default class Clock extends Component {
    // 状态固定名字
  state = {
      date: new Date()
  }

  componentDidMount(){
      this.timer = setInterval(() => {
          this.setState({
              date: new Date()
          })
      }, 1000);
  }

  componentWillUnmount(){
      clearInterval(this.timer);
  }

  render() {
    return (
      <div>
        {this.state.date.toLocaleTimeString()}
      </div>
    )
  }
}

```

```js
import React, { Component } from "react";

export default class CartSample extends Component {
  //   状态初始化一般放在构造器中
  constructor(props) {
    super(props);

    this.state = {
      goods: [
        { id: 1, text: "web全栈架构师" },
        { id: 2, text: "python全栈架构师" }
      ],
      text: "",
      cart: []
    };

    this.addGood = this.addGood.bind(this);
  }

  //   回调函数声明为箭头函数
  textChange = e => {
    this.setState({ text: e.target.value });
  };

  addGood() {
    this.setState(prevState => {
      return {
        goods: [
          ...prevState.goods,
          {
            id: prevState.goods.length + 1,
            text: prevState.text
          }
        ]
      };
    });
  }

  //   加购函数
  addToCart = good => {
    // 创建新购物车
    const newCart = [...this.state.cart];
    const idx = newCart.findIndex(c => c.id === good.id);
    const item = newCart[idx];
    if (item) {
      newCart.splice(idx, 1, { ...item, count: item.count + 1 });
    } else {
      newCart.push({ ...good, count: 1 });
    }
    // 更新
    this.setState({ cart: newCart });
  };

  //   处理数量更新
  add = good => {
    // 创建新购物车
    const newCart = [...this.state.cart];
    const idx = newCart.findIndex(c => c.id === good.id);
    const item = newCart[idx];
    newCart.splice(idx, 1, { ...item, count: item.count + 1 });

    // 更新
    this.setState({ cart: newCart });
  };

  minus = good => {
    // 创建新购物车
    const newCart = [...this.state.cart];
    const idx = newCart.findIndex(c => c.id === good.id);
    const item = newCart[idx];

    newCart.splice(idx, 1, { ...item, count: item.count - 1 });

    // 更新
    this.setState({ cart: newCart });
  };

  render() {
    //   const title = this.props.title ? <h1>this.props.title</h1> : null;
    return (
      <div>
        {/* 条件渲染 */}
        {this.props.title && <h1>{this.props.title}</h1>}

        {/* 列表渲染 */}
        <div>
          <input
            type="text"
            value={this.state.text}
            onChange={this.textChange}
          />
          <button onClick={this.addGood}>添加商品</button>
        </div>
        <ul>
          {this.state.goods.map(good => (
            <li key={good.id}>
              {good.text}
              <button onClick={() => this.addToCart(good)}>加购</button>
            </li>
          ))}
        </ul>

        {/* 购物车 */}
        <Cart data={this.state.cart} minus={this.minus} add={this.add} />
      </div>
    );
  }
}

function Cart({ data, minus, add }) {
  return (
    <table>
      <tbody>
        {data.map(d => (
          <tr key={d.id}>
            <td>{d.text}</td>
            <td>
              <button onClick={() => minus(d)}>-</button>
              {d.count}
              <button onClick={() => add(d)}>+</button>
            </td>
            {/* <td>{d.price*d.count}</td> */}
          </tr>
        ))}
      </tbody>
    </table>
  );
}
//直接传递方法给子组件
//this.props.parent.getChildrenMsg(this, this.state.msg)子组件向父组件传值
//父组件中通过this.refs.children或者this.refs[children]获取到一整个子组件实例
```

# react的最新生命周期

## 缘由

react打算在17版本退出Async/Rendering，提出一种可能被打断的声明周期，而可以被打断的阶段正是实际dom挂载之前的虚拟dom构建阶段，也就是要被去掉的三个生命周期。

旧的：

componentWillMount，componentWillReceiveProps，componentWillUpdate

新的：

static getDerivedStateFromProps，getSnapshotBeforeUpdate

生命周期一旦被打断，恢复时会再跑一次之前的生命周期，componentWillMount，componentWillReceiveProps，componentWillUpdate不能保证只在挂载/拿到props/状态变化的时候刷新了一次，所以会被标记为不安全。

## 两个新生命周期

### static getDerivedStateFromProps

**触发时间**：在组件构建之后，虚拟dom之后，实际dom挂载之前。以及每次获取新的props之后。

每次接受新的props都会返回一个对象作为新的state，如果null则不需要更新state。

配合componentDidUpdate，能够componentWillReceiveProps的所有用法。

***componentDidUpdate** 在组件完成更新后立即调用。在初始化时不会被调用*

```javascript
class Example extends React.Component {  
    static getDerivedStateFromProps(nextProps, prevState) {
        //do somthing
    }
}
```

## getSnapshotBeforeUpdate

**触发时间**：update发生的时候，在render之后，在组件dom渲染之前。

返回一个值，作为**componentDidUpdate**的第三个参数。

配合**componentDidUpdate**，可以覆盖componentWillUpdate的所有用法。

***componentWillUpdate**在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用。*

```javascript
class Example extends React.Component {  
    getSnapshotBeforeUpdate(prevProps, prevState) { 
        //do somthing 
    }
}
```

## 用法：

请求数据--fetch data

在componentDidMount请求异步加载的数据。

在componentWillMount请求的数据在render就能拿到，但其实render在willMount之后几乎是马上被调用的，根本等不到数据的回来，同样需要render一次加载中的空状态。

根据props更新state--updating state based on props

用getDerivedStateFromProps（nextProps，prevState），将传入的props更新到state上。

来代替componentWillReceiveProps(nextProps, nextState)，willReceiveProps经常被误用，导致了一些问题，因此该方法将不被推荐使用。

 ![img](https://img-blog.csdnimg.cn/20181113163949486.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5MjUy,size_16,color_FFFFFF,t_70) 

 旧版本的生命周期图，红色框线的是将会被移除的。 

 ![img](https://img-blog.csdnimg.cn/20181113164030692.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5MjUy,size_16,color_FFFFFF,t_70) 

