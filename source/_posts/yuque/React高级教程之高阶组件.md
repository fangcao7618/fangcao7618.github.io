
---

title: React高级教程之高阶组件

date: 2019-07-02 09:39:10 +0800

tags: []

---
[https://www.imooc.com/learn/1075](https://www.imooc.com/learn/1075)

[https://www.imooc.com/video/18267](https://www.imooc.com/video/18267) 高阶组件
<a name="4VFpG"></a>
# 高阶组件介绍
高阶组件的定义及原理<br />高阶组件在项目中的常见应用<br />通用高阶组件如何封装

<a name="sdLnp"></a>
### 高阶函数基本概念（High Order Component,HOC）

- 高阶组件就是接受一个组件作为参数并返回一个新组件的函数
- 高阶组件是一个函数，并不是组件
<a name="9vQnN"></a>
#### 函数可以作为参数被传递
```javascript
setTimeOut(()=>{console.log(1)},1000)
```
<a name="pJNis"></a>
#### 函数可以作为返回值输出
```javascript
function foo(x){
	return function(){
  	return x;
  }
}
```

高阶组件不是一个组件

<a name="ObeFE"></a>
# 高阶组件应用
<a name="5b1eD"></a>
## 代理方式的高阶组件
返回的新组件类直接继承自React.Component类，新组件扮演的角色传入参数组件的一个代理，在新组件的render函数中，将被包裹的组件渲染出来，除了高阶组件自己要做的工作，其余功能全部转手给了被包裹的组件<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562289743635-2446343c-2a9d-495e-bff1-d3cfb6aef9d9.png#align=left&display=inline&height=222&name=image.png&originHeight=222&originWidth=1262&size=192389&status=done&width=1262)

```javascript
A.jsx
/*
 *代理方式的高阶组件
 */
import React, { Component } from "react";

export default title => WrappedComponent =>
    class A extends Component {
        constructor(props) {
            super(props);
            this.state = {
                inputvalue: ""
            };
        }
        onInputChange = e => {
            this.setState({
                inputvalue: e.target.value
            });
        };
        refc(instance) {
            //instance是WrappedComponent的实例
            console.log(instance);
            // instance.getName && console.log(instance.getName());
        }
        render() {
            const { age, ...otherProps } = this.props;
            const newProps = {
                inputvalue: this.state.inputvalue,
                onInput: this.onInputChange
            };
            return (
                <div className="a-container">
                    <div className="header">
                        <div>{title}</div>
                        <div>×</div>
                    </div>
                    <div className="content">
                        我是高阶组件A
                        <WrappedComponent
                            sex={"男"}
                            {...otherProps}
                            ref={this.refc.bind(this)}
                            {...newProps}
                        />
                    </div>
                </div>
            );
        }
    };


B.jsx
import React, { Component } from "react";
import A from "./A";
// import D from "./D";

// @D
class B extends Component {
    constructor(props) {
        super(props);
        this.state = {
            value: ""
        };
    }
    changeInput(e, parame) {
        console.log(e.target.value, parame);
        this.setState({
            value: e.target.value
        });
    }
    getName() {
        return "我是B组件";
    }
    render() {
        return (
            <div>
                我是组件B
                <br />
                <input type="text" {...this.props} />
                <br />
                <input
                    type="text"
                    value={this.state.value}
                    onChange={e => {
                        this.changeInput(e, "wfc");
                    }}
                />
                <br />
                我的名字叫:{this.props.name}
                <br />
                我的年龄是:{this.props.age}
                <br />
                我的性别是：{this.props.sex}
                <img src={require("../images/B.jpg")} alt="" />
            </div>
        );
    }
}
export default A("提示")(B);
// export default B;

C.jsx
import React, { Component } from "react";
import A from "./A";

@A("警告")
class C extends Component {
    getName() {
        return "我是C组件";
    }
    render() {
        return (
            <div>
                <input type="text" {...this.props} />
                <img src={require("../images/C.jpg")} alt="" />
            </div>
        );
    }
}

export default C;


App.js
import React from "react";
import B from "./components/B";
import C from "./components/C";
import "./App.css";

function App() {
    return (
        <div className="App">
            <B name={"张三"} age={18} />
            <C />
        </div>
    );
}

export default App;

```


<a name="Gk3CH"></a>
## 继承方式的高阶组件
采用继承关联作为参数的组件和返回的组件，假如传入的组件参数是WrappedComponent,那么返回的组件就直接继承自WrappedComponent<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562289757349-50f2c880-d710-417e-9b5b-21f0df7b3a20.png#align=left&display=inline&height=236&name=image.png&originHeight=236&originWidth=1280&size=190020&status=done&width=1280)
<a name="zHdlK"></a>
### 操纵prop
<a name="2Gh2J"></a>
### 操纵生命周期函数

```javascript
D.jsx
/*
 * 继承方式的高阶函数组件
 */
import React from "react";

const modifyPropsHOC = WrappedComponent =>
    class NewComponent extends WrappedComponent {
        componentWillMount() {
            console.log("我是修改后的生命周期");
        }
        render() {
            const element = super.render();
            const newStyle = {
                color: element.type === "div" ? "red" : "green"
            };
            const newProps = { ...this.props, style: newStyle };
            return React.cloneElement(
                element,
                newProps,
                element.props.children
            );
        }
    };
export default modifyPropsHOC;


E.jsx
import React, { Component } from "react";
import D from "./D";
@D
class E extends Component {
    componentWillMount() {
        console.log("我是原始生命周期");
    }
    render() {
        return <div>我是div</div>;
    }
}
export default E;

F.jsx
import React, { Component } from "react";
import D from "./D";
@D
class F extends Component {
    render() {
        return <p>我是P</p>;
    }
}
export default F;


App.js
import React from "react";
import E from "./components/E";
import F from "./components/F";
import "./App.css";

// const BComponent = A(B);
function App() {
    return (
        <div className="App">
            <E />
            <F />
        </div>
    );
}

export default App;

```
<a name="gx5Af"></a>
## 高阶组件显示名

```javascript
/**
 * @description 继承方式的高阶函数组件
 * @author wfc
 * @date 2019-07-05
 * @param {*} WrappedComponent
 * @returns
 */
import React from "react";

const modifyPropsHOC = WrappedComponent =>
    class NewComponent extends WrappedComponent {
        static displayName = `NewComponent(${getDispalyName(
            WrappedComponent
        )})`;
        componentWillMount() {
            console.log("我是修改后的生命周期");
        }
        render() {
            const element = super.render();
            const newStyle = {
                color: element.type === "div" ? "red" : "green"
            };
            const newProps = { ...this.props, style: newStyle };
            return React.cloneElement(
                element,
                newProps,
                element.props.children
            );
        }
    };

//高阶组件显示名
function getDispalyName(WrappedComponent) {
    console.log(WrappedComponent);
    return WrappedComponent.displayName || WrappedComponent.name || "Component";
}
export default modifyPropsHOC;
```

<a name="jFpgq"></a>
## 高阶组件实战项目搭建
<a name="qIuUB"></a>
### 1.create-react-app tabbar
<a name="Jqley"></a>
### 2.Tabbar静态布局实现
去[https://www.iconfont.cn/](https://www.iconfont.cn/)搜图标 添加图标到项目
```javascript
tabbar/index.js
import React, { Component } from "react";
import "./index.css";

const tarbarArr = [
    {
        img: "icon-home",
        text: "首页"
    },
    {
        img: "icon-fenlei_",
        text: "分类"
    },
    {
        img: "icon-gouwuche",
        text: "购物车"
    },
    {
        img: "icon-yonghu",
        text: "用户"
    }
];
export default class index extends Component {
    render() {
        return (
            <div className="tabbar">
                <div className="tabbar-content">
                    {tarbarArr.map((v, i) => (
                        <div key={i} className="tarbar-item">
                            <div className={`iconfont ${v.img}`} />
                            <div className="">{v.text}</div>
                        </div>
                    ))}
                </div>
            </div>
        );
    }
}

```

<a name="ZbzJV"></a>
### 3.Tabbar绑定点击事件
```javascript
tabbar/index.js
import React, { Component } from "react";
import "./index.css";

const tarbarArr = [
    {
        img: "icon-home",
        text: "首页"
    },
    {
        img: "icon-fenlei_",
        text: "分类"
    },
    {
        img: "icon-gouwuche",
        text: "购物车"
    },
    {
        img: "icon-yonghu",
        text: "用户"
    }
];
export default class index extends Component {
    constructor(props) {
        super(props);
        this.state = {
            index: 0
        };
    }
    itemChange = i => {
        this.setState({
            index: i
        });
    };
    render() {
        return (
            <div className="tabbar">
                <div className="tabbar-content">
                    {tarbarArr.map((v, i) => (
                        <div
                            key={i}
                            className={`tarbar-item${
                                this.state.index === i ? " active" : ""
                            }`}
                            onClick={() => {
                                this.itemChange(i);
                            }}
                        >
                            <div className={`iconfont ${v.img}`} />
                            <div className="">{v.text}</div>
                        </div>
                    ))}
                </div>
            </div>
        );
    }
}

```
<a name="imkhn"></a>
### 4.Tabbar添加路由
[react-router](https://reacttraining.com/react-router/web/guides/quick-start)
```javascript
router.js
import React from "react";
import { BrowserRouter, Route, Switch } from "react-router-dom";

// const Home = () => <div>home</div>;
import Home from './pages/home';
import Category from "./pages/category";
import Car from "./pages/car";
import User from "./pages/user";

export default () => (
    <BrowserRouter>
        <Switch>
            <Route path="/home" component={Home} />
            <Route path="/category" component={Category} />
            <Route path="/car" component={Car} />
            <Route path="/user" component={User} />
        </Switch>
    </BrowserRouter>
);

```

<a name="mnxiH"></a>
### 5.Tabbar添加路由切换
```javascript
tabbar/index.js

import React, { Component } from "react";
import { Link } from "react-router-dom";
import "./index.css";

const tarbarArr = [
    {
        img: "icon-home",
        text: "首页",
        link: "/home"
    },
    {
        img: "icon-fenlei_",
        text: "分类",
        link: "/category"
    },
    {
        img: "icon-gouwuche",
        text: "购物车",
        link: "/car"
    },
    {
        img: "icon-yonghu",
        text: "用户",
        link: "/user"
    }
];
export default class index extends Component {
    constructor(props) {
        super(props);
        this.state = {
            index: 0
        };
    }
    itemChange = i => {
        this.setState({
            index: i
        });
    };
    render() {
        return (
            <div className="tabbar">
                <div className="tabbar-content">
                    {tarbarArr.map((v, i) => (
                        <Link
                            to={v.link}
                            key={i}
                            className={`tarbar-item${
                                this.state.index === i ? " active" : ""
                            }`}
                            onClick={() => {
                                this.itemChange(i);
                            }}
                        >
                            <div className={`iconfont ${v.img}`} />
                            <div className="">{v.text}</div>
                        </Link>
                    ))}
                </div>
            </div>
        );
    }
}

```
<a name="hFFgA"></a>
### 6.其它页面

```javascript
pages/home.js

import React, { Component } from "react";
import Tabbar from "../components/tabbar";

export default class home extends Component {
    render() {
        return (
            <div>
                <img
                    className="bg"
                    src={require("../static/images/home.jpg")}
                    alt=""
                />
                <Tabbar />
            </div>
        );
    }
}

car.js category.js user.js 以此类推

tabbar/index.js
import React, { Component } from "react";
import { Link } from "react-router-dom";
import "./index.css";

const tarbarArr = [
    {
        img: "icon-home",
        text: "首页",
        link: "/home"
    },
    {
        img: "icon-fenlei_",
        text: "分类",
        link: "/category"
    },
    {
        img: "icon-gouwuche",
        text: "购物车",
        link: "/car"
    },
    {
        img: "icon-yonghu",
        text: "用户",
        link: "/user"
    }
];
export default class index extends Component {
    constructor(props) {
        super(props);
        this.state = {
            index: 0
        };
    }
    itemChange = i => {
        this.setState({
            index: i
        });
    };
    render() {
        const url = window.location.href;
        return (
            <div className="tabbar">
                <div className="tabbar-content">
                    {tarbarArr.map((v, i) => (
                        <Link
                            to={v.link}
                            key={i}
                            className={`tarbar-item${
                                url.indexOf(v.link) > -1 ? " active" : ""
                                // this.state.index === i ? " active" : ""
                            }`}
                            onClick={() => {
                                this.itemChange(i);
                            }}
                        >
                            <div className={`iconfont ${v.img}`} />
                            <div className="">{v.text}</div>
                        </Link>
                    ))}
                </div>
            </div>
        );
    }
}

```
因为每个页面都加了tabbar，判断条件必须编程url，不然不准。
<a name="JXeCF"></a>
### 7.使用高阶组件改写Tabbar
编写高阶组件<br />1.实现一个普通组件<br />2.将普通组件使用函数包裹
```javascript
tabbar/index.js
import React, { Component } from "react";
import { Link } from "react-router-dom";
import "./index.css";

const tarbarArr = [
    {
        img: "icon-home",
        text: "首页",
        link: "/home"
    },
    {
        img: "icon-fenlei_",
        text: "分类",
        link: "/category"
    },
    {
        img: "icon-gouwuche",
        text: "购物车",
        link: "/car"
    },
    {
        img: "icon-yonghu",
        text: "用户",
        link: "/user"
    }
];
const Tabbar = WrappedComponent =>
    class Tabbar extends Component {
        constructor(props) {
            super(props);
            this.state = {
                index: 0
            };
        }
        itemChange = i => {
            this.setState({
                index: i
            });
        };
        render() {
            const url = window.location.href;
            return (
                <React.Fragment className="tabbar-container">
                    <div className="tabbar-children">
                        <WrappedComponent />
                    </div>
                    <div className="tabbar">
                        <div className="tabbar-content">
                            {tarbarArr.map((v, i) => (
                                <Link
                                    to={v.link}
                                    key={i}
                                    className={`tarbar-item${
                                        url.indexOf(v.link) > -1
                                            ? " active"
                                            : ""
                                    }`}
                                    onClick={() => {
                                        this.itemChange(i);
                                    }}
                                >
                                    <div className={`iconfont ${v.img}`} />
                                    <div className="">{v.text}</div>
                                </Link>
                            ))}
                        </div>
                    </div>
                </React.Fragment>
            );
        }
    };
export default Tabbar;

// pages/home.js
import React, { Component } from "react";
import Tabbar from "../components/tabbar";

class Home extends Component {
    render() {
        return (
            <div>
                <img
                    className="bg"
                    src={require("../static/images/home.jpg")}
                    alt=""
                />
            </div>
        );
    }
}
export default Tabbar(Home);
car.js category.js user.js一次类推
```

<a name="A339Q"></a>
## 总结回顾
高阶组件概述<br />高阶组件实现<br />高阶组件应用<br />高阶组件使用出现的问题<br />高阶组件实战<br />回顾与总结

