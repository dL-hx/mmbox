# Mobx 学习进阶

[TOC]

项目代码

https://github.com/dL-hx/react-redux-guide

简单可扩展的状态管理

+ 1. Mobx简介

  > 背景,浏览器兼容性

+ 2. 开发前的准备

  > 如何支持装饰器语法.

+ 3. Mobx+React

  > 如何结合使用

+ 4. Mobx异步

  > 异步更新本地状态

+ 5. Mobx数据监测

  > 数据检测方法

+ 6. 综合案例

## 一 Redux核心

### 1.1 Redux介绍

javascript 状态容器,  提供可预测化的状态管理

**让状态容易维护**

```js
const state={
    modelOpen:'yes', // 弹窗展示或隐藏
    btnClicked:'no', // 按钮是否点击
    btnActiveClass:'active',
    page:5,
    size:10
}
```

### 1 Redux 核心

### 1.3 Redux核心概念及工作流程

![image-20211224225331658](README.assets/image-20211224225331658.png)



**dispatch**: view 需要通过dispatch派发 action对象,更新store 数据,从而更新页面view

**subscribe**: 订阅数据,更新视图



### 1.4 Redux计数器案例

![image-20211224225331658](README.assets/计数器案例.png)

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button id="plus">+</button>
    <span id='count'>0</span>
    <button id="minus">-</button>

    <script src="redux.min.js"></script>
    <script>


        // 3. 存储默认状态
        var initialState = {count: 0} 
        // 2. 创建reducer函数
        function reducer(state=initialState, actions) {
            console.log('actions', actions);
            var type= actions.type
            if(type==='increment'){
                return {
                    count:state.count+1
                };
            }


            if(type==='decrement'){
                 return {
                    count:state.count-1
                 };
            }

            
            return state;
        }
        // 1. 创建store对象
        var store = Redux.createStore(reducer)


        // 获取store对象中存储的状态
        console.log(store.getState());
        
        // 4.定义action
        var increment = {type:'increment'}
        var decrement = {type:'decrement'}


        // 5.获取按钮 给按钮添加点击事件
        document.getElementById('plus').onclick=function(){
            // console.log(1);
            // 6. 触发action
            store.dispatch(increment)
        }

        document.getElementById('minus').onclick=function(){
            // console.log(1);
            store.dispatch(decrement)
        }

        // 7.订阅store
        store.subscribe(()=>{
            // 获取store对象中存储的状态
            // console.log(store.getState());
            
            // 将获取到的数据进行订阅赋值
            document.getElementById('count').innerHTML=store.getState().count

        })

    </script>
</body>
</html>
```



### 1.5 Redux核心Api

```js
// 创建Store 状态容器
const store = Redux.createStore(reducer)

// 创建用于处理状态的 reducer 函数
function reducer(state = initialState, action){}

// 获取状态
store.getState();

// 订阅状态
store.subscribe(function(){});

// 触发Action(由dispatch 触发action  )
store.dispatch({type:'description...'})
```





## Redux解决了什么问题



## 二 React + Redux

### 2.1 在React 中不使用Redux 时遇到的问题



1. **在React中组件通信的数据流是单向的,**

2. **顶层组件可以通过props属性向下层组件传递数据,**

3. **而下层组件不能向上层组件传递数据,**

4. **要想实现下层组件修改数据, 需要上层组件传递修改数据的方法到下层组件**
5. **当项目越来越大时候,组件之间传递数据变得越来越困难.**



![image-20211226204608546](README.assets/image-20211226204608546-16405232629061.png)

 

### 2.2 在React 中加入Redux 好处

**使用Redux管理数据, 由于Store独立于组件, 使得数据管理独立于组件, 解决了组件与组件之间传递数据困难的问题.**

![image-20211226204608546](README.assets/image-20211226205017599.png)



 

## 在React 中使用 Redux

### 2.3 下载Redux

安装 redux , react-redux  这两个模块

```bash
$	npm install redux react-redux
```

 

### 2.4 Redux工作流程

1. 组件通过dispatch方法触发Action
2. Store 接收Action并将Action分发给Reducer
3. Reducer 根据Action类型对状态进行更改并将更改后的状态返回给Store
4. 组件订阅了Store中的状态, Store中的状态更新会同步到组件

![image-20211226212455174](README.assets/image-20211226212455174.png)



[nvm环境配置](https://www.bilibili.com/video/BV12h411z7Kq?from=search&seid=6898323572004308878&spm_id_from=333.337.0.0)

配合博客安装:https://www.mintimate.cn/2021/07/26/nvmNode/

相关博文:

https://segmentfault.com/a/1190000040688010

```js
NPM配置淘宝镜像
临时使用

npm install --registry https://registry.npm.taobao.org
 

全局使用

npm config set registry https://registry.npm.taobao.org
查看全局配置

npm config get registry
恢复全局配置

npm config set registry https://registry.npmjs.org
 

通过CNPM使用

npm install -g cnpm --registry=https://registry.npm.taobao.org
```





创建项目

``` bash
$	npm install create-react-app -g
$   create-react-app react-redux-guide
$   cd react-redux-guide/
$   npm start

//项目目录
|____react-redux-guide
|____README.md
|____node_modules/
| |____package.json
|____.gitignore
|____public
| |____favicon.ico
| |____index.html
|____src
| |____App.js

| |____index.js


```



 在浏览器中打开 [http://localhost:3000/](https://link.segmentfault.com/?enc=v9ECHhrO%2BHBORN62Gi3fpQ%3D%3D.2P5E2cFGk%2Fmrcgslvd3vQP71pxc4TBVhpFo3qXkyzB4%3D) ，即可显示

![image-20211226231635102](README.assets/image-20211226231635102.png)

// src\App.js

```jsx
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

import { createStore } from "redux";

const initialState = {
  count: 0,
};

function reducer(state = initialState, actions) {
  switch (actions.type) {
    case "increment": // 数值 + 1 ,返回一个新对象
      return {
        count: state.count + 1
      }

    case "decrement":
      return {
        count: state.count - 1
      }
    default:
      return state;
  }


}

const increment = { type: "increment" };
const decrement = { type: "decrement" };

const store = createStore(reducer);

function Counter() {
  return (
    <div>
      <button onClick={() => store.dispatch(increment)}>+</button>
      <span>{store.getState().count}</span>
      <button onClick={() => store.dispatch(decrement)}>-</button>
    </div>
  );
}

// 必须要订阅订阅数据更新,返回一个新的组件
store.subscribe(()=>{// 订阅数据返回新的数值
  ReactDOM.render(<Counter />, document.getElementById("root"));
})



// console.log("store", store.getState());

ReactDOM.render(<Counter />, document.getElementById("root"));

```



发现遇到一些问题, 

1.  **store部分代码写了两次,  如何分离store**
2. **分离后如何拿到store对象, 将是解决的问题**

https://github.com/dL-hx/react-redux-guide

feat/1.0.0分支



## Provider组件与connect方法

https://github.com/dL-hx/react-redux-guide

feat/1.1.0分支



### 2.5 connect方法两个参数



mapStateToProps，

mapDispatchToProps，

1.1 Provider组件与connect方法

为了使react 和 redux进行结合 ，需要通过 react-redux 模块实现连接





```
connect 作用
1. 帮助订阅store
2. 当store中状态发生变化，  会重新渲染组件

3. 获取store中的状态， 将状态映射到props属性中映射给组件
4. 获取dispatch方法， 触发action 
```

connect方法两个参数意义
mapStateToProps，
mapDispatchToProps，

``` jsx
import React from "react";
import { connect } from "react-redux";
import {increment, decrement} from './../../index'

// function Counter(props) {
// 解构操作
function Counter({count, addCount, minusCount, dispatch}) {
  console.log(count);
  
  return (
    <div>
      {/* <button onClick={() => store.dispatch(increment)}>+</button> */}
      {/* <button onClick={() => dispatch(increment)}>+</button> */}
      {/* <button onClick={() => addCount()}>+</button> */}
      <button onClick={addCount}>+</button>
      {/* <span>{store.getState().count}</span> */}
      <span>{count}</span>
      {/* <button onClick={() => store.dispatch(decrement)}>-</button> */}
      {/* <button onClick={() => minusCount()}>-</button> */}
      <button onClick={minusCount}>-</button>
    </div>
  );
}


const mapStateToProps = (state)=>{
  return {
    // a:'b',
    count:state.count
  }
}



const mapDispatchToProps = (dispatch)=>{
  
  return {
    // addCount:function (data) {
    //   dispatch(increment)
    // },

    // 简化后如下
    addCount(data) {
      dispatch(increment)
    },

    minusCount(data) {
      dispatch(decrement)
    },


    dispatch
  }
}


export default connect(mapStateToProps,mapDispatchToProps )(Counter);
```



## bindActionsCreators方法

### 2.6 bindActionsCreators方法

https://github.com/dL-hx/react-redux-guide

feat/1.2.0分支



 目的： 调用方法生成函数， 优化如下代码

```js
const mapDispatchToProps = (dispatch)=>{
  
  return {
    // addCount:function (data) {
    //   dispatch(increment)
    // },

    // 简化后如下
    addCount(data) {
      dispatch(increment)
    },

    minusCount(data) {
      dispatch(decrement)
    },


    dispatch
  }
}
```

优化后

```js
import { bindActionCreators } from "redux";


const mapDispatchToProps = (dispatch) => ({
  // 用于生成函数
  ...bindActionCreators(
    {
      addCount() {
        return increment;
      },

      minusCount() {
        return decrement;
      },
    },
    dispatch
  ),
  
});
```

等价于

```js

const mapDispatchToProps = (dispatch) => ({
  // 用于生成函数
  ...bindActionCreators(
    {
      addCount() {
        return {type:'increment'};
      },

      minusCount() {
        return {type:'decrement'};
      },
    },
    dispatch
  ),
});
```





``` js
import * as counterActions  from './../../store/actions/counter.actions'


const mapDispatchToProps = (dispatch) => ({
  // 用于生成函数
  ...bindActionCreators(counterActions, dispatch),
});
```



一个action简化如下

``` js
const mapDispatchToProps = (dispatch) =>
(bindActionCreators(counterActions, dispatch));

```


### 2.7 代码重构

https://github.com/dL-hx/react-redux-guide

feat/1.3.0分支

App.js

```js
import React from "react";
import ReactDOM from "react-dom";
// import App from "./App";
import Counter from "./components/Counter";

import {store} from "./store";

// import { createStore } from "redux";
import { Provider } from "react-redux";

/* 
react-redux 
  Provider: 将store放到全局中，  组件都能拿到的地方
  connect
*/


ReactDOM.render(
  // 通过Provider 组件， 将store 放到了全局组件可以够得到的地方
  <Provider store={store}>
    <Counter />
  </Provider>,
  document.getElementById("root")
);

```



1.将reducer函数， 创建store代码放到store代码中

store
```js
import { createStore } from "redux";
import reducer from './reducers/counter.reducer'

export const store = createStore(reducer);

```

const

const/counter.const.js

```js
export const INCREMENT= "increment"
export const DECREMENT= "decrement"

```

reducers

reducers/counter.reducer.js


```js
import { INCREMENT ,DECREMENT } from "../const/counter.const";

const initialState = {
    count: 0,
  };

function reducer(state = initialState, actions) {
      switch (actions.type) {
        case INCREMENT: // 数值 + 1 ,返回一个新对象
          return {
            count: state.count + 1,
          };
    
        case DECREMENT:
          return {
            count: state.count - 1,
          };
        default:
          return state;
      }
}

export default reducer
    
```

actions

actions/counter.action.js

``` js
export const INCREMENT= "increment"
export const DECREMENT= "decrement"

```


2. 将action类型代码拆分为常量，防止写错
INCREMENT, DECREMENT



## Action传递参数

### 2.8 Redux使用步骤

为action传递参数

#### 1. 传递参数

点击按钮时候数值 + 5

``` jsx
<button onClick={()=>addCount(5)}> + 1</button>
```



#### 2.接收参数, 传递reducer

```jsx
export const addCount = payload =>({type:INCREMENT, payload });
```



#### 3. reducer根据接收到的数据进行处理

``` jsx
export default (state, actions)=>{
    switch(actions.type){
        case INCREMENT:
            return {count: state.count + actions.payload }
    }
}
```

https://github.com/dL-hx/react-redux-guide

feat/1.4.0分支



## Redux弹出框

https://github.com/dL-hx/react-redux-guide

feat/1.5.0分支



reducers/counter.reducer.js

```js
import { INCREMENT, DECREMENT } from "../const/counter.const";
import { SHOW_MODAL, HIDE_MODAL } from "../const/modal.const";

const initialState = {
  count: 0,
  show: false,
};

function reducer(state = initialState, actions) {
  switch (actions.type) {
    case INCREMENT: // 数值 + 1 ,返回一个新对象
      return {
        ...state,
        // count: state.count + 1,
        count: state.count + actions.payload,
      };

    case DECREMENT:
      return {
        ...state,
        // count: state.count - 1,
        count: state.count - actions.payload,
      };

    // 这里需要保存原有的state,进行拷贝
    case SHOW_MODAL:
      return {
        ...state,
        show: true,
      };

    case HIDE_MODAL:
      return {
        ...state,
        show: false,
      };
    default:
      return state;
  }
}

export default reducer;

```

modal.actions.js

```js
import { SHOW_MODAL, HIDE_MODAL } from "../const/modal.const";

export const show = () => ({ type: SHOW_MODAL });
export const hide = () => ({ type: HIDE_MODAL });
```

components/Modal/index.js

```js
import React from "react";
import { connect } from "react-redux";
import { bindActionCreators } from "redux";
import * as modalActions from "./../../store/actions/modal.actions";

function Modal(props) {
  
  const styles = {
    width: 200,
    height: 200,
    position: "absolute",
    left: "50%",
    top: "50%",
    // marginLeft 等于,负的 自己盒子W的一半
    // -200/2 = -100
    marginLeft: -100,
    // marginTop 等于,负的 自己盒子H的一半
    // -200/2 = -100
    marginTop: -100,
    backgroundColor: "skyblue",
    display: props.vist ? "block" : "none",
  };

  return (
    <div>
      <button onClick={()=>props.show()}>显示</button>
      <button onClick={()=>props.hide()}>隐藏</button>
      {/*  {
             props.show&&<div style={styles}></div>
        } */}
      <div style={styles}></div>
    </div>
  );
}

// export default Modal;
const mapStateToProps = (state) => {
  return {
    vist: state.show,
  };
};

const mapDispatchToProps=(dispatch)=>{
    return bindActionCreators(modalActions, dispatch)
}

export default connect(mapStateToProps, mapDispatchToProps)(Modal);

```



## **拆分Reducer**

https://github.com/dL-hx/react-redux-guide



feat/1.6.0分支



既匹配了counter的reducer,又匹配了modal的reducer,看如何拆分reducer,又能将其进行组合



### 1. 拆分reducer

counter.reducer.js

modal.reducer.js

### 2. 合并reducer

combineReducers

``` js
 import { combineReducers } from 'redux'
```

reducers/root.reducer.js

``` js
// root reducer 用来reducer的合并
 import { combineReducers } from 'redux'

//  1. 拆分reducer
 import CounterReducer from './counter.reducer'
 import ModalReducer from './modal.reducer'

 // 2. 合并reducer
 // {counter:{count:0}, model:{show:false}}
export default combineReducers({
    counter: CounterReducer,
    modal: ModalReducer,
})
```



\src\store\index.js

``` js
import { createStore } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from './reducers/root.reducer'

export const store = createStore(RootReducer);
```



调用时候修改如下

``` js
const mapStateToProps = (state) => {
  return {
    vist: state.modal.show,
  };
};
```



``` js
const mapStateToProps = (state) => {
  return {
    // a:'b',
    count: state.counter.count,
  };
};
```

## 中间件概念介绍

## 三  Redux 中间件

### 3.1 什么是中间件?

1. **中间件允许我们扩展redux应用程序**
2. **中间件是一个函数,  扩展增强redux能力**
3. **组件优先被中间件处理**
4. **增强action的处理能力**



### 3.2 加入了中间件的Redux工作流?

中间件中处理action,处理完成后交给reducer

![image-20211229004518065](README.assets/image-20211229004518065.png)

## 开发Redux中间件

https://github.com/dL-hx/react-redux-guide

feat/1.7.0分支



### 3.3 开发Redux中间件

开发中间件的模板代码

```js
export default store => next =>action=> {}
```

### 3.4 注册中间件

将开发好的中间件需要 为store注册,  这个中间件才会生效

> 中间件在开发完成以后只有被注册才能在Redux的工作流程中生效

./store/index.js

```js
import {createStore, applyMiddleware } from 'redux';
import logger from './middlewares/logger';

createStore(reducer, applyMiddleware( 
    logger
));
```



```
//项目目录
|____react-redux-guide
|____src
| |____...
| |____store
| 	|____actions
| 	|____const
+ 	|____middleware
+ 		|____logger.js
| 	|____reducers
| 	|____index.js



```

./middleware/logger.js

``` js
// 导出中间件的模板代码
export default function (store) {
    return function (next) {
        return function (action) {
            // 在这里执行自己的逻辑
        }
    }
}
```

===> 简化为

箭头函数的写法简化

``` js
export default (store) => (next) => (action) => {
    // 在这里执行自己的逻辑
};
```

1. 定义中间件

``` js
export default (store) => (next) => (action) => {
    // 在这里执行自己的逻辑

    // 输出store
    console.log(store);

    // 输出这个action
    console.log(action);

    // <调用>next 方法
    // 目的: 将这个action 传递给 reducer,
    // 并将action 传递给reducer
    next(action);
    
};
```

2. 注册中间件

./store/index.js

``` js
import { createStore, applyMiddleware } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from "./reducers/root.reducer";

// 引入中间件
import logger from "./middleware/logger";

// 注册中间件
export const store = createStore(RootReducer, applyMiddleware(logger));

```

发现中间件组件已经被注册.

![image-20211229150353376](README.assets/image-20211229150353376.png)



多个中间件的注册,   多中间件的执行顺序

./middleware/test

``` js
export default (store) => (next) => (action) => {
    console.log('test 中间件被执行了');
    next(action) // 需要传递给下一个中间件,让reducer接收,否则代码卡到这里不会向下执行
};
```



``` js
import { createStore, applyMiddleware } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from "./reducers/root.reducer";

// 引入中间件
import logger from "./middleware/logger";
import test from "./middleware/test";

// 注册中间件-------------(执行顺序取决于这里的注册顺序)
export const store = createStore(RootReducer, applyMiddleware(
    logger,
    test
));

```

![image-20211229175738163](README.assets/image-20211229175738163.png)



## 中间件开发实例

![image-20211229192809362](README.assets/image-20211229192809362.png)

https://github.com/dL-hx/react-redux-guide

feat/1.8.0分支



延迟相加/延迟弹窗展示

通过中间件完成

>  **在redux工作流中加入异步操作**

在修改时候,不会修改中间件代码,这样设计比较灵活.

.\store\middleware\thunk.js

```js
export default store =>next => action =>{
    // 1.当前这个中间件函数不关心你想执行什么样的异步操作,  只关心你是不是异步操作

    // 2. 如果是异步操作,  触发action, 传递为一个函数

    // 3. 如果是同步操作,传递action 对象

    // 4. 异步操作写在你传递进来的函数

    // 5. 当前这个中间件函数在调用你传递的函数时候,  将dispatch 传递过去

    // 6. 在函数中,通过dispatch 派发action --->reducer保存数据

    // 让action自己决定什么时候,进行dispatch 数据
    if(typeof action === 'function'){
        return action(store.dispatch)
    }

    next(action)



    // if(action.type==='increment'||action.type==='decrement'){
    //     setTimeout(()=>{
    //         next(action)// 延迟两秒后生效
    //     },2000)
    // }
}
```





```js
import { createStore, applyMiddleware } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from "./reducers/root.reducer";

// 引入中间件
import logger from "./middleware/logger";
import test from "./middleware/test";
import thunk from "./middleware/thunk";

// 注册中间件
export const store = createStore(RootReducer, applyMiddleware(
    logger,
    test,
    thunk
));

```

.\store\actions\modal.actions.js

``` js
// 让弹出框延迟显示

export const show_async = ()=> (dispatch)=>{
    setTimeout(()=>{
        dispatch(show())
    },2000)
}
```

.\store\actions\counter.actions.js

```js
import { INCREMENT ,DECREMENT } from "../const/counter.const";
//---------------=> action 对象
export const addCount = (payload)=> ({type:INCREMENT, payload })

export const addCount_async = (payload)=> (dispatch)=>{
    setTimeout(()=>{
        // 两秒后派发dispatch ,到reducer 处理
        dispatch(addCount(payload))
        // 等价于这个
        // dispatch({type:INCREMENT, payload })
    },2000)
}
```

组件代码调用

```js
  <button onClick={()=>addCount_async(5)}>+ 5 </button>
```

```js
  <button onClick={()=>props.show_async()}>显示</button>
```





## 四.Redux常用中间件

https://github.com/dL-hx/react-redux-guide

feat/1.9.0分支



## Redux-thunk

### 4.1 redux-thunk

> 允许在redux操作过程中加入异步操作

#### 4.1.1 redux-thunk 下载

``` shell
$	npm install redux-thunk --save
```

使用插件就不需要我们去手写中间件了

#### 4.1.2 引入redux-thunk

``` js
import thunk from 'redux-thunk';
```

#### 4.1.3 注册redux-thunk

```js
import thunk from 'redux-thunk';

// 注册中间件
export const store = createStore(RootReducer, applyMiddleware(thunk));

```

#### 4.1.4 使用redux-thunk中间件

```js
const loadPosts = () => async dispatch =>{
    const posts = await axios.get('/api/posts').then(response=>response.data)
    dispatch({type:LOAD_POST_SUCCESS, payload:posts })
}

```

action中调用如下

.\store\actions\counter.actions.js

``` js

export const addCount_async = (payload)=> (dispatch)=>{
    setTimeout(()=>{
        // 两秒后派发dispatch ,到reducer 处理
        dispatch(addCount(payload))
        // 等价于这个
        // dispatch({type:INCREMENT, payload })
    },2000)
}


```

## redux-saga

https://github.com/dL-hx/react-redux-guide

feat/2.0.0分支

### 4.2 redux-saga

文档学习:

https://redux-saga-in-chinese.js.org/docs/introduction/BeginnerTutorial.html

API_DOC:

https://redux-saga-in-chinese.js.org/docs/api/

#### 4.2.1 redux-saga解决的问题

>  redux-saga可以**将异步操作从Action Creater文件中抽离出来**, 放在一个单独的文件中.

比redux-thunk 更好用,功能类似

#### 4.2.2 redux-saga 下载

``` shell
$	npm install redux-saga --save
```

#### 4.2.3 创建redux-saga 中间件

``` js
import createSagaMiddleware from 'redux-saga';
const sagaMiddleware = createSagaMiddleware();
```

sagaMiddleware注册给store

#### 4.2.4 注册redux-saga

```  js
createStore(RootReducer, applyMiddleware(sagaMiddleware));
```

#### 4.2.5 使用saga接收action执行异步操作

https://github.com/dL-hx/react-redux-guide

feat/2.0.0分支

```js
import {takeEvery, put} from 'redux-saga/effects';// 引入两个异步方法

function* load_post(){
    const {data} = yield axios.get('/api/posts.json');
    // put: 用来触发另外一个action,当异步操作时候,  触发action reducer,保存状态
    yield put(load_posts_success(data))
}

// saga:文件中,  要求默认导出一个generater 函数
export default function* postSaga(){
    // takeEvery:用来接收action,通过takeEvery方法接收组件触发的action
    
    // 接收到的action类型string,    接收这个action 需要执行的方法
    yield takeEvery(LOAD_POSTS, load_posts)
}
```



#### 4.2.6 启动saga

> 目的:这样做,所写的saga文件才会被加入到redux的工作流中.

```js
import postSaga from './store/sagas/post.saga';

sagaMiddleware.run(postSaga)
```

.\store\index.js

```js
import { createStore, applyMiddleware } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from "./reducers/root.reducer";

import createSagaMiddleware from 'redux-saga'

import counterSaga from './sagas/counter.saga';


// 创建sagaMiddleware,创建中间件
const sagaMiddleware = createSagaMiddleware()

// 注册redux-saga
export const store = createStore(RootReducer, applyMiddleware(sagaMiddleware));

// 启动counterSaga, 这样才会加入redux工作流中
sagaMiddleware.run(counterSaga)

```



.\store\actions\counter.actions.js

``` js
import { INCREMENT ,DECREMENT , INCREMENT_ASYNC } from "../const/counter.const";
//---------------=> action 对象
export const addCount = (payload)=> ({type:INCREMENT, payload })

...

+ export const addCount_async = ()=> ({type: INCREMENT_ASYNC })

```



.\store\sagas\counter.saga.js

``` js
import { takeEvery, put , delay } from "redux-saga/effects"; // 引入两个异步方法
import { addCount } from "../actions/counter.actions";
import { INCREMENT_ASYNC } from "../const/counter.const";
// takeEvery 接收action
// put 触发action


function* addCount_async_fn(){
   // 执行异步操作
   // 注意: 在generater函数中,   延迟不能使用setTimeout

   // 1. 暂停延迟2s
   yield delay(2000)
   // 2. put 触发action,更新了reducer
   yield put(addCount(10))
}



// saga文件默认要求: 导出一个generater函数
export default function* counterSaga() {
  // 接收action
  // 参数1:接收类型字符串
  // 参数2:异步方法执行的函数.
  yield takeEvery(INCREMENT_ASYNC, addCount_async_fn);
}
```

页面调用

```js
   <button onClick={addCount_async}>+ 5 </button>
```

### redux-saga传参

https://github.com/dL-hx/react-redux-guide

feat/2.1.0分支



页面调用

```js
 <button onClick={()=>addCount_async_1(20)}>+ 5 </button>
```

.\store\sagas\counter.saga.js

```js
export const addCount_async_1 = (payload)=> ({type: INCREMENT_ASYNC, payload })
```

.\store\sagas\counter.saga.js

```js
...

function* addCount_async_1_fn(action){
   yield delay(2000)

    // 从形参中, 获取页面层组件,   传递来的参数
//    yield put(addCount(10))
     // 再次触发action, 修改state状态
   yield put(addCount(action.payload))
}



// saga文件默认要求: 导出一个generater函数
export default function* counterSaga() {
  // 接收action
  // 参数1:接收类型字符串
  yield takeEvery(INCREMENT_ASYNC, addCount_async_1_fn);
}
```

### redux-saga拆分合并

https://github.com/dL-hx/react-redux-guide

feat/2.2.0分支

> saga组件拆分

.\store\sagas\counter.saga.js

```js
import { takeEvery, put, delay } from "redux-saga/effects"; // 引入两个异步方法
import { addCount } from "../actions/counter.actions";
import { show } from "../actions/modal.actions";
import { INCREMENT_ASYNC } from "../const/counter.const";
import { SHOW_MODAL_ASYNC } from "../const/modal.const";
// takeEvery 接收action
// put 触发action

function* addCount_async_1_fn(action) {

  // 1. 暂停延迟2s
  yield delay(2000);
  // 2. put 触发action
  //    yield put(addCount(10))
  yield put(addCount(action.payload));
}

function* show_async_fn(action) {
  // 1. 暂停延迟2s
  yield delay(2000);

  yield put(show());
}

// saga文件默认要求: 导出一个generater函数
export default function* counterSaga() {
  // 接收action
  // 参数1:接收类型字符串
  yield takeEvery(INCREMENT_ASYNC, addCount_async_1_fn);

  yield takeEvery(SHOW_MODAL_ASYNC, show_async_fn);
}

```



// 因为如果不拆分, 这个saga文件就会变得很臃肿, 所以需要拆分

.\store\sagas\counter.saga.js

``` js
import { takeEvery, put, delay } from "redux-saga/effects"; // 引入两个异步方法
import { addCount } from "../actions/counter.actions";
import { INCREMENT_ASYNC } from "../const/counter.const";
// takeEvery 接收action
// put 触发action

function* addCount_async_1_fn(action) {
  // 执行异步操作
  // 注意: 在generater函数中,   延迟不能使用setTimeout

  // 1. 暂停延迟2s
  yield delay(2000);
  // 2. put 触发action
  //    yield put(addCount(10))
  yield put(addCount(action.payload));
}


// saga文件默认要求: 导出一个generater函数
export default function* counterSaga() {
  // 接收action
  // 参数1:接收类型字符串
  yield takeEvery(INCREMENT_ASYNC, addCount_async_1_fn);

}
```



.\store\sagas\modal.saga.js

```js
import { takeEvery, put, delay } from "redux-saga/effects"; // 引入两个异步方法
import { show } from "../actions/modal.actions";
import { SHOW_MODAL_ASYNC } from "../const/modal.const";
// takeEvery 接收action
// put 触发action

function* show_async_fn(action) {
  // 1. 暂停延迟2s
  yield delay(2000);

  yield put(show());
}

// saga文件默认要求: 导出一个generater函数
export default function* modalSaga() {
  // 接收action
  // 参数1:接收类型字符串

  yield takeEvery(SHOW_MODAL_ASYNC, show_async_fn);
}
```

.\store\sagas\root.saga.js

> 组合saga文件

```js
import { all } from "redux-saga/effects"; // 引入all方法

import counterSaga from "./counter.saga";
import modalSaga from "./modal.saga";

// saga文件默认要求: 导出一个generater函数
// 通过all方法导出saga文件
export default function* rootSaga() {
  yield all([counterSaga(), modalSaga()]);
}
```

在修改store/index.js文件

进行注册

```js
import { createStore, applyMiddleware } from "redux";
// import reducer from './reducers/counter.reducer'
// 改为合并后的reducers
import RootReducer from "./reducers/root.reducer";


import createSagaMiddleware from 'redux-saga'

// import counterSaga from './sagas/counter.saga';

import rootSaga from './sagas/root.saga';


// 创建sagaMiddleware,创建中间件
const sagaMiddleware = createSagaMiddleware()

// 注册redux-saga
export const store = createStore(RootReducer, applyMiddleware(sagaMiddleware));

// 启动counterSaga, 这样才会加入redux工作流中
// sagaMiddleware.run(counterSaga)
sagaMiddleware.run(rootSaga)
```

## redux-actions

https://github.com/dL-hx/react-redux-guide

feat/2.3.0分支

redux-actions解决的问题

> 相关文章:
>
> https://zhuanlan.zhihu.com/p/273569290

### 4.3 redux-actions

#### 4.3.1 redux-actions 解决的问题

redux流程中大量的样板代码读写很痛苦, 

,如action, reducer, const,等

使用redux-actions 可以简化Action和Reducer的处理.



#### 4.3.2 redux-actions 下载

``` shell
$	npm install redux-actions --save
```



+ 1. 用于简化action代码
+ 2. 用于简化reducer代码



#### 4.3.3 创建 Action

> 使用了redux-actions 这个函数 actions 就不需要自己去定义了
>
> 1. (之前) 手动定义action_create函数
>
>    ``` js
>    export const addCount = (payload)=> ({type:INCREMENT, payload })
>    ```
>
> 2. (现在) 通过 'redux-actions' 自动生成该函数, 
>
>    使用时候,不用定义type 常量,  redux-action的中间件

``` js
import { createAction } from 'redux-actions';

const increment_action = createAction('increment');
const decrement_action = createAction('decrement');
```



#### 4.3.4 创建 Reducer

> redux-actions 简化reducer

简化前

counter.reducer.js

```js
import { INCREMENT, DECREMENT } from "../const/counter.const";

const initialState = {
  count: 0,
};

function reducer(state = initialState, actions) {
  switch (actions.type) {
    case INCREMENT: // 数值 + 1 ,返回一个新对象
      return {
        ...state,
        // count: state.count + 1,
        count: state.count + actions.payload,
      };

    case DECREMENT:
      return {
        ...state,
        // count: state.count - 1,
        count: state.count - actions.payload,
      };

    default:
      return state;
  }
}

export default reducer;

```

简化后

``` js
import {handleActions as createReducer } from 'redux-actions';

import { addCount_Action, minusCount_Action } from '../actions/counter.actions';

const initialState = { count: 0 }

const counterReducer = createReducer({
  [addCount_Action]:(state, actions)=>({
    ...state,
    // count: state.count + 1,
    count: state.count + actions.payload,
  }),


  [minusCount_Action]:(state, actions)=>({
    ...state,
    // count: state.count - 1,
    count: state.count - actions.payload,
  })

}, initialState)

export default counterReducer;
```



.\store\actions\counter.actions.js

> 将简化常量文件的定义, 因为后面将通过addCount_Action,这个方法去定义了
>
> createAction: 自动添加了payload方法

```js
import { createAction } from 'redux-actions';

// import { INCREMENT ,DECREMENT , INCREMENT_ASYNC } from "../const/counter.const";

export const addCount_Action = createAction('increment');
// export const addCount_Action = createAction(INCREMENT);

// export const minusCount_Action = createAction(DECREMENT);
export const minusCount_Action = createAction('decrement');
```

调用

点击按钮时候,  传递到reducer中自动处理,  从而减少了代码量

```js
      <button onClick={()=>addCount_Action(20)}>+ 20</button>
	  <button onClick={()=>minusCount_Action(5)}>- 5</button>
```



createAction 给我们创建了变量 action 这样就避免了我们在其他文件到处使用字符串 action。

handleActions 给我们生成了 reducer 丰富了reducer 中处理功能，这就是我在大前端训练营所接触的冰山一角。



## 五. redux shopping案例

https://github.com/dL-hx/shopping

### 5.1 项目初始化

shoppingCart 项目前端文件

shoppingCartService 项目服务端文件

![image-20220101013820695](README.assets/image-20220101013820695.png)



```js
import React from 'react'
import CartTable from './CartTable';
import ProductList from './ProductList';


function App() {
  return (
    <div>
       <ProductList />
       <CartTable />
    </div>
  );
}

export default App;
```

### 5.2 搭建redux工作流

> 搭建完成的工作流查看如下:
>
> https://github.com/dL-hx/shopping/releases/tag/v1.0
>
> ```
> redux工作流创建
> ```



git tag 使用技巧

> https://wenku.baidu.com/view/63cf605502f69e3143323968011ca300a6c3f6bc.html
>
> 1、添加tag
>
> > git tag v0.2.0 -m "use sdl [render](https://so.csdn.net/so/search?q=render&spm=1001.2101.3001.7020) audio."
>
> 2、提交tag
>
> > git push --tags



#### 5.2.1 依赖安装

``` shell
$	npm install redux react-redux redux-saga redux-actions --save

```

#### 5.2.2 项目文件目录

> 参考如下进行搭建         feat/1.6.0分支

> https://github.com/dL-hx/react-redux-guide

```
+ ------store
	+ ------actions
	+ ------reducers
		+ product.reducer.js
		+ ------root.reducer.js // 根目录的reducer
	+ ------sagas
	
	+ ------index.js

```



app.js

> 引入Provider

``` js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './components/App';
import { Provider } from 'react-redux'
import {store} from './store' // 引入Provider
import './index.css';

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/470f1c2ab2a14fb4a2f04b3e0824ec56.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5bCP5p2O56eR5oqA,size_20,color_FFFFFF,t_70,g_se,x_16)
至此基本搭建完成

### 5.3 action文件编写

#### 5.3.1 实现商品列表数据获取

> ```
> redux-saga搭建获取产品数据
> ```
>
> 查看如下:
>
> https://github.com/dL-hx/shopping/tree/v1.1
>
> ```
> redux-saga搭建获取产品数据
> ```





> 查看  4.2 redux-saga, 异步操作,放入redux-store中
>
> 查看  4.3 redux-actions 中间件 减少了模板代码的编写
>
> 思考为什么要使用redux-saga?
>
> https://blog.csdn.net/weixin_34293059/article/details/93169225

redux-saga优点：

- 异步解耦：异步操作被被转移到单独saga.js中，不再是掺杂在action.js或component.js中；
- action摆脱thunk function: dispatch的参数依然是⼀个纯粹的 action (FSA)，⽽不是充满 “⿊魔法” thunk function；
- 异常处理：受益于 generator function 的saga实现，代码异常/请求失败都可以直接通过try/catch语法直接捕获处理；
- 功能强⼤：redux-saga提供了⼤量的Saga辅助函数和Effect创建器供开发者使⽤，开发者⽆须封装或者简单封装即可使⽤；
- 灵活：redux-saga可以将多个Saga可以串⾏/并⾏组合起来，形成⼀个⾮常实⽤的异步flow；
- 易测试，提供了各种case的测试⽅案，包括mock task，分⽀覆盖等等。

redux-saga缺陷：

- 额外的学习成本：redux-saga不仅在使⽤难以理解的generator function，⽽且有数⼗个API，学习成本远超reduxthunk，最重要的是你的额外学习成本是只服务于这个库的
- 体积庞⼤：体积略⼤，代码近2000⾏，min版25KB左右；
- 功能过剩：实际上并发控制等功能很难⽤到，但是我们依然需要引⼊这些代码；
- ts⽀持不友好：yield⽆法返回TS类型。

	
		+ ------store
		+ ------actions
		+ ------reducers
			+ product.reducer.js
			+ ------root.reducer.js // 根目录的reducer
		+ ------sagas
			+ product.saga.js    // product.saga
			+ ------root.saga.js // 合并saga
		
		+ ------index.js
	

``` js
product.action.js

	+ loadProducts

	+ saveProducts
```



bindActionCreactors

sagaMiddleware



#### [v1.2](https://github.com/dL-hx/shopping/releases/tag/v1.2)

```
redux-saga展示购物车数据
```



#### [v1.3 ](https://github.com/dL-hx/shopping/releases/tag/v1.3)

```
CRUD
```

#### 5.3.2 商品加入购物车中

``` js
// 加入购物车
export const addCartListServer = createAction('addCartListServer');

// 更改商品数量
export const changeCartNumListClick = createAction('changeCartNumListClick');
```



#### 5.3.3 购物车案例CRUD

``` js
// 加入购物车
export const addCartListServer = createAction('addCartListServer');

// 更改商品数量
export const changeCartNumListClick = createAction('changeCartNumListClick');


// 更改购物车中的商品数量
export const addCartItemNumServer = createAction('addCartItemNumServer');

// 改变货物数量(修改本地数据)
export const changeCartNumListLocal = createAction('changeCartNumListLocal');


// 删除购物车商品

export const delCartItemServer = createAction('delCartItem');

// 改变删除后的CartList (修改本地数据)
export const delCartItemLocal = createAction('delCartItemLocal');
```



