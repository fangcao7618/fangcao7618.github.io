
---

title: JsBridge

date: 2019-06-12 18:18:53 +0800

tags: []

---
整个流程就是Native和Js两端各准备一个bridge，Native的bridge提供modules，js的bridge注册Native提供的modules。这就是bridge存在的意义--提供一个桥梁，让两边通信。

简单来说，只需要两步，第一简历桥连接，第二注册方法：

```javascript
function setupWebViewJavascriptBridge(callback) {
    if (window.WebViewJavascriptBridge) {
        return callback(WebViewJavascriptBridge);
    }
    if (window.WVJBCallbacks) {
        return window.WVJBCallbacks.push(callback);
    }
    window.WVJBCallbacks = [callback];
    var WVJBIframe = document.createElement('iframe');
    WVJBIframe.style.display = 'none';
    WVJBIframe.src = 'wvjbscheme://__BRIDGE_LOADED__';
    document.documentElement.appendChild(WVJBIframe);
    setTimeout(function () {
        document.documentElement.removeChild(WVJBIframe)
    }, 100)
}
function connectWebViewJavascriptBridge(callback) {
    if (window.WebViewJavascriptBridge) {
        callback(WebViewJavascriptBridge)
    } else {
        document.addEventListener(
        'WebViewJavascriptBridgeReady'
        , function () {
            callback(WebViewJavascriptBridge)
        }, false);
    }
}

```
兼容安卓ios

```javascript
if (navigator.userAgent.match(/(iPhone|iPod|iPad);?/i)) { //ios
    setupWebViewJavascriptBridge(function (bridge) {
        bridge.callHandler(funcName, data,callback );
    });
} else if (navigator.userAgent.match(/android/i)) {
    connectWebViewJavascriptBridge(function(bridge) {
        if(window.WebViewJavascriptBridge){
            window.WebViewJavascriptBridge.callHandler(
               funcName
               , data,
               callback
            );
        }else{
            bridge.callHandler(funcName, data, callback);
        }
   });
} else {

}
```
Android 初次加载是需要初始化

```javascript
bridge.init(function(message, responseCallback) {responseCallback(data)});
```

h5调用native<br />iOS在setupWebViewJavascriptBridge里注册<br />android在connectWebViewJavascriptBridge里注册

```javascript
bridge.callHandler(funcName, data, callback);
```
native调用js

```javascript
bridge.registerHandler(funcName, function(responseData, responseCallback) {
});
```

<a name="tAWE1"></a>
### 概念

1、H5，即是html5，超文本标记语言，用于描述网页内容结构的语言，网页编程中由它有负责描述页面数据和信息<br />2、JS，即是JavaScript，广泛用于web应用开发中的脚本语言，负责响应用户的操作，为网页添加动态功能<br />3、native APP，即传统的原生APP开发模式，Android基于Java语言，底层调用Google的 API；iOS基于Objective-C或者Swift语言，底层调用App官方提供的API<br />4、Hybrid App，即原生和web的混合开发模式，由原生提供统一的API给js调用，实现跨平台的效果

<a name="zfJgE"></a>
### 交互方式

- 第一种为H5与native的基本通讯方式

说是基本通讯方式是因为由native自身的组件进行通讯的，这里需要区分为android和iOS，两端的组件实现有差异

![vv.jpg](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560390930770-e52bed1b-90bc-4ab7-b615-a39859f1cea1.jpeg#align=left&display=inline&height=312&name=vv.jpg&originHeight=312&originWidth=1126&size=78347&status=done&width=1126)


基本通讯方式汇总

1. iOS通过官方提供的库文件JaveScriptCore来实现交互，可以脱离webview直接运行js
1. android是通过addJavascriptInterface开放统一的api给js调用，实现交互，但具有安全性问题，版本4.2之前addJavascriptInterface接口引起安全漏洞，可被反编译获取Native注册的js对象，在页面通过反射Java的内置静态类，获取一些敏感的信息和破坏。
- 第二种H5与native交互方式为JSBridge原理

JSBridge是H5代码与native代码之间的一个通讯桥梁，是广为流行的交互理念。目前的统一实现流程是：H5触发url scheme-->native捕获url scheme-->原生分析并执行-->原生调用H5，如下图：<br />![gg.jpg](https://cdn.nlark.com/yuque/0/2019/jpeg/263301/1560391235884-88aaf64b-ceb6-4d4d-969d-9414e63fd272.jpeg#align=left&display=inline&height=437&name=gg.jpg&originHeight=437&originWidth=874&size=46259&status=done&width=874)

URL scheme，是一个URL最初始的位置，即://之前的那段字符，如[baidu.com](https://link.zhihu.com/?target=http%3A//www.baidu.com)的scheme为http；根据我们上面对URL scheme的使用，我们可以理解，H5通过某种方式如iframe触发scheme，然后Native用某种方法捕获对应的url触发事件，根据定义好的协议，分析当前触发了哪种方法，然后根据定义来执行。比如短信，就是sms：，比如微信，就是weixin<br />
所以JSBridge交互本质就是通过webview的代理拦截url scheme，然后注入相应的JS，从而实现交互，目前我们公司使用的是第三方开源库WebViewJavascriptBridge，下面我们来讲讲这个通讯桥梁。

<a name="bDwzz"></a>
### 实现流程

1. 首先在H5代码注入js代码块

```javascript
function setupFH5JsBridge(callback) {
    var ua = navigator.userAgent.toLowerCase(),
        isiOS = ua.match(/(iphone|ipod|ipad);?/i),
        isAndroid = ua.match("android");
    if (isAndroid) {
        if (window.FH5JsBridge) {
            window.FH5JsBridge.initBridge(callback);
        } else {
            document.addEventListener(
                "FH5JsBridgeReady",
                function() {
                    window.FH5JsBridge.initBridge(callback);
                },
                false
            );
        }
        window.WebViewJavascriptBridge = window.FH5JsBridge;
    } else if (isiOS) {
        if (window.WebViewJavascriptBridge) {
            return callback(WebViewJavascriptBridge);
        }
        if (window.WVJBCallbacks) {
            return window.WVJBCallbacks.push(callback);
        }
        window.WVJBCallbacks = [callback];
        var WVJBIframe = document.createElement("iframe");
        WVJBIframe.style.display = "none";
        WVJBIframe.src = "wvjbscheme://__BRIDGE_LOADED__";
        document.documentElement.appendChild(WVJBIframe);
        setTimeout(function() {
            document.documentElement.removeChild(WVJBIframe);
        }, 0);
    }
}
setupFH5JsBridge(function(bridge) {});

```
or<br />我们项目里是这样：
```javascript
function nativeApp() {
    var App = {
            callbacks: {}
        },
        slice = Array.prototype.slice;
    /**
     * 常量定义
     */
    var ua = navigator.userAgent.toUpperCase();
    // 当前环境是否为Android平台
    App.IS_ANDROID = ua.indexOf("ANDROID") != -1;
    // 当前环境是否为IOS平台
    App.IS_IOS = ua.indexOf("IPHONE OS") != -1;
    // 当前环境是否为WP平台
    App.IS_WP = ua.indexOf("WINDOWS") != -1 && ua.indexOf("PHONE") != -1;

    App.IS_YZT = /One Account (IOS|Android)/gi.test(ua);

    App.callbacks.__leftAction__ = function() {
        var haveLeftAction = typeof App.callbacks.leftAction === "function",
            args = slice.call(arguments);
        if (haveLeftAction) {
            setTimeout(function() {
                App.callbacks.leftAction.apply(App.callbacks, args);
            }, 0);
            if (App.IS_ANDROID) {
                App.call(["called"]);
            } else if (App.IS_IOS) {
                return true;
            }
        }
    };

    //=======================Native 相关================================

    var callindex = 0,
        isFunc = function(name) {
            return typeof name === "function";
        },
        isObj = function(name) {
            return typeof name === "object";
        };
    /**
     * 调用一个Native方法
     * @param {String} name 方法名称
     */
    App.call = function(name) {
        // 获取传递给Native方法的参数
        var args = slice.call(arguments, 1);
        var successCallback = "",
            errorCallback = "",
            item = null,
            returnArg;
        var methodName = name[name.length - 1];
        if (App.IS_YZT) {
            if (App.IS_ANDROID) {
                if (window.HostApp) {
                    var newArguments = [];
                    for (var i = 0; i < args.length; i++) {
                        if (isFunc(args[i])) {
                            var callbackName =
                                methodName + "Callback" + callindex;
                            window[callbackName] = args[i];
                            newArguments.push(callbackName);
                            callindex++;
                        } else if (isObj(args[i])) {
                            newArguments.push(JSON.stringify(args[i]));
                        } else {
                            newArguments.push(args[i]);
                        }
                    }

                    // 之所以要重新调用，是因为Android 初始化HostApp可能晚于JS调用。
                    try {
                        HostApp[methodName].apply(window.HostApp, newArguments);
                    } catch (e) {
                        // TODO 这里应该走Mock functions
                        var params = slice.call(arguments, 0);
                        setTimeout(function() {
                            App["call"].apply(window.App, params);
                        }, 300);
                    }
                } else {
                    var params = slice.call(arguments, 0);
                    setTimeout(function() {
                        App["call"].apply(window.App, params);
                    }, 1000);
                }
            } else if (App.IS_IOS) {
                var tempArgument = [];
                for (var i = 0; i < args.length; i++) {
                    if (isFunc(args[i])) {
                        var callbackName = methodName + "Callback" + callindex;
                        window[callbackName] = args[i];
                        tempArgument.push(callbackName);
                        callindex++;
                    } else {
                        args[i] && tempArgument.push(args[i]);
                    }
                }
                callindex++;
                var iframe = document.createElement("iframe");
                var _src =
                    "callnative://" +
                    methodName +
                    "/" +
                    (tempArgument && tempArgument.length
                        ? encodeURIComponent(JSON.stringify(tempArgument)) +
                          "/" +
                          callindex
                        : "");
                console.log(_src);
                iframe.src = _src;
                iframe.style.display = "none";
                document.body.appendChild(iframe);
                iframe.parentNode.removeChild(iframe);
                iframe = null;
            } else {
                // WP 用户不支持。 Mock functions, 模拟H5 容器
                console.warn("Tips: No available environment WP");
                // Mock functions, 模拟H5 容器
                for (var i = 0; i < args.length; i++) {
                    if (isFunc(args[i])) {
                        args[i]({});
                        return;
                    }
                }
            }
        } else {
            console.warn("Tips: No available environment, NO YZT");
            // Mock functions, 模拟H5 容器
            for (var i = 0; i < args.length; i++) {
                if (isFunc(args[i])) {
                    args[i]({});
                    return;
                }
            }
        }
    };
}
window.AppAPI = nativeApp();
AppAPI.call(["onGetShareData"], data);
AppAPI.call(
    ["checkLoginStatus"],
    function(data) {
        callback && callback(SUCCESS, formatJSON(data));
    },
    function(err) {
        //do nothing
        callback && callback(ERROR, err);
    },
    {}
);

```


2. JS端使用方式

native端需要进行注册对应的方法，H5才可以调用


Android注册方式如下:
```javascript
FH5JsBridge.registerHandler(bridgeWebView, handlerName, bridgeHandler);
```

iOS端注册方式如下

```javascript
/*** @param registerHandler 要注册的事件名称
@param handel 回调block函数 当后台触发这个事件的时候会执行block里面的代码 ***/ 
[_bridge
registerHandler:@"loginFunc" handler:^(id data, PAFFWVJBResponseCallback
responseCallback) { 
// data 后台传过来的参数,例如用户名、密码等 
NSLog(@"testObjcCallback called:
%@", data); 
//具体的登录事件的实现,这里的login代表实现登录功能的一个OC函数。 
[self login]; 
// responseCallback 给后台的回复 
responseCallback(res);
}];
```

H5调用方式如下

```javascript
FH5JsBridge.callHandler(methodName, 方法名options,对象 callback) 
调用 Native API其中callback 统一接受一个参数json对象
```

H5常见的调用方法

- 打开native 页面，从H5页面跳转到某个原生页面
```javascript
void openAppPage(data,callback) --data 为{pageName:''}
```

- 获取会话token，H5登录区内的操作需获取原生的登录态
```javascript
void getSSOTicket(data,callback)
```

- 刷新会话，在一定的时间内刷新会话
```javascript
void refreshSession(data,callback)
```

- 打开原生App的安全键盘
```javascript
void openSafeKeyboard(data,callback)
```

- 打开分享，微信QQ等分享
```javascript
void share(data,callback)
```

- 设置临时存储数据，H5需要存储native的数据作为临时数据，退出APP后，临时数据清空
```javascript
void setData(data, callback)
data 格式为{key:"key", value: string }
```

- 获取临时存储数据，获取临时存储的数据进行使用
```javascript
void getData(data, callback)
data 格式为{key:"key"}
```

- 删除临时存储数据
```javascript
void removeData(data, callback)
data格式为{key:"key"}
```


![1767225-bb4069ede233b274.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560340159134-466bbab7-ce2a-4401-9bdc-a1ddd2c59810.png#align=left&display=inline&height=880&name=1767225-bb4069ede233b274.png&originHeight=880&originWidth=1239&size=105844&status=done&width=1239)<br />
加载过程<br />![1767225-0f6275ca58b94775.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560340174592-956831d0-3c65-4fdf-be85-0387a95fdb51.png#align=left&display=inline&height=880&name=1767225-0f6275ca58b94775.png&originHeight=880&originWidth=1281&size=147776&status=done&width=1281)<br />
加载和互相调用

