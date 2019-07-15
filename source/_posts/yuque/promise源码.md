
---

title: promise源码

date: 2019-06-19 14:08:43 +0800

tags: []

---
了解Promise诞生的历史背景<br />学会使用Promise解决异步回调带来的问题<br />掌握Promise的进阶用法

<a name="FP3OW"></a>
## 异步操作的常见语法

```javascript
document.getElementById('start').addEventListener('click',start,false);

function start(){
	//响应事件，进行响应的操作
}

$('#start').on('click',start);
```
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562312377535-f004f625-53a7-4024-8ac6-6446f106488b.png#align=left&display=inline&height=312&name=image.png&originHeight=780&originWidth=1252&size=275324&status=done&width=500)<br />有了Node.js之后<br />对异步的依赖进一步加剧了......<br />无阻塞高并发


<a name="Ev1Pu"></a>
## Promise详解

```javascript
new Promise(
  //执行器 executor
	function(resolve,reject){
    // 一段耗时很长的异步操作
    resolve();// 数据处理完成
    reject();// 数据处理出错
  }
).then(function A(){
  //成功，下一步
},function B(){
  //失败，做相应处理
})
```

<a name="hJJRz"></a>
### Promise实例一经创建，执行器立即执行
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562313871871-30b961ef-e0b0-4e40-8e33-4988c77091e5.png#align=left&display=inline&height=630&name=image.png&originHeight=630&originWidth=1760&size=307820&status=done&width=1760)

<a name="62qXy"></a>
#### 简单实例

```javascript
console.log("here we go");
    new Promise(resolve => {
        setTimeout(() => {
            resolve("hello");
        }, 2000);
    }).then(value => {
        console.log(`${value} world`);
    });
```

<a name="qgezV"></a>
#### 两步执行的范例

```javascript
console.log("here we go");
    new Promise(resolve => {
        setTimeout(() => {
            resolve("hello");
        }, 2000);
    })
        .then(value => {
            console.log(value);
            return new Promise(resolve => {
                setTimeout(() => {
                    resolve("nihao");
                }, 1000);
            });
        })
        .then(value => {
            console.log(`${value} world`);
        });
here we go
hello
nihao world
```

<a name="0fbzZ"></a>
#### 对已完成的Promise执行then

```javascript
console.log("start");

let promise = new Promise(resolve => {
    setTimeout(() => {
        console.log("the promise fulfilled");
        resolve("hello,world");
    }, 1000);
});

setTimeout(() => {
    promise.then(value => {
        console.log("value:", value);
    });
}, 0);

start
the promise fulfilled
value: hello,world
```
不管promise前面的状态是否完成，都会按它的队列去执行

<a name="Wgo4P"></a>
#### then里不返回Promise

```javascript
console.log("start");

let promise = new Promise(resolve => {
    setTimeout(() => {
        console.log("the promise fulfilled");
        resolve("hello,world");
    }, 2000);
})
    .then(value => {
        console.log(value);
        console.log("everyone");
        (function() {
            console.log("比包");
            return new Promise(resolve => {
                setTimeout(() => {
                    console.log("Mr Lanrence");
                    resolve("Merry Xmas");
                }, 0);
            });
        })();
        return false;
    })
    .then(value => {
        console.log(value + " world");
    });
start
the promise fulfilled
hello,world
everyone
比包
false world
Mr Lanrence
```

<a name="aJ6my"></a>
#### 引出.then()

- .then()接受两个函数作为参数，分别代表fulfilled和rejected
- .then()返回一个新的Promise实例，所以它可以链式调用
- 当前面的Promise状态改变时，.then()根据其最终状态，选择特定的状态响应函数执行
- 状态响应函数可以返回新的Promise，或其他值
- 如果返回新的Promise,那么下一级.then()会在新Promise状态改变后执行
- 如果返回其它任何值，则会立刻执行下一级.then()
<a name="ISdkS"></a>
#### .then()里有.then()的情况

- 因为.then()返回的还是Promise实例。
- 会等里面的.then()执行完，再执行外面的。
- 对于我们来说，此时最好将其展开，会更好读。
```javascript
console.log("start");

let promise = new Promise(resolve => {
    console.log("step1");
    setTimeout(() => {
        resolve("100");
    }, 1000);
})
    .then(value => {
        return new Promise(resolve => {
            console.log("Step 1-1");
            setTimeout(() => {
                resolve(110);
            }, 1000);
        })
            .then(value => {
                console.log("Step 1-2");
                return value;
            })
            .then(value => {
                console.log("Step 1-3");
                return value;
            });
    })
    .then(value => {
        console.log(value);
        console.log("Step 2");
    });
start
step1
Step 1-1
Step 1-2
Step 1-3
110
Step 2


一样的效果可以这样改
console.log("start");

let promise = new Promise(resolve => {
    console.log("step1");
    setTimeout(() => {
        resolve("100");
    }, 1000);
})
    .then(value => {
        return new Promise(resolve => {
            console.log("Step 1-1");
            setTimeout(() => {
                resolve(110);
            }, 1000);
        });
    })
    .then(value => {
        console.log("Step 1-2");
        return value;
    })
    .then(value => {
        console.log("Step 1-3");
        return value;
    })
    .then(value => {
        console.log(value);
        console.log("Step 2");
    });

start
step1
Step 1-1
Step 1-2
Step 1-3
110
Step 2
```
<a name="RR6Hm"></a>
### 问题：下面的四种Promise的区别是什么
<a name="250pW"></a>
#### 问题一
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562552319805-63ec61b8-40bb-469b-a3ec-c58d0ab384b7.png#align=left&display=inline&height=874&name=image.png&originHeight=874&originWidth=1848&size=351895&status=done&width=1848)
<a name="voK4H"></a>
#### 问题二
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562552362678-e96a47eb-10d3-49ac-9e28-335c1b7c2831.png#align=left&display=inline&height=830&name=image.png&originHeight=830&originWidth=1830&size=325575&status=done&width=1830)
<a name="VNd5d"></a>
#### 问题三（比较有欺骗性）doSomethingElse()也是一个promise
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562552412695-cf19837d-4fc4-45e6-b1db-8fe1f4dd30d9.png#align=left&display=inline&height=740&name=image.png&originHeight=740&originWidth=1884&size=321619&status=done&width=1884)
<a name="YJH0i"></a>
#### 问题四
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562552470609-22e0bf85-d94f-48ff-88f2-bf556144d445.png#align=left&display=inline&height=694&name=image.png&originHeight=694&originWidth=1848&size=328357&status=done&width=1848)
<a name="kyXgk"></a>
### 错误处理

```javascript
console.log("start");
new Promise(resolve => {
    setTimeout(() => {
        throw new Error("bye");
    }, 2000);
})
    .then(value => {
        console.log(value + " world");
    })
    .then(error => {
        console.log("Error: ", error, error.message);
    });

```
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562553541709-10635239-ff16-40db-a5b1-30ea290252f4.png#align=left&display=inline&height=111&name=image.png&originHeight=111&originWidth=233&size=8587&status=done&width=233)

<a name="9Jt2a"></a>
#### 错误处理的两种做法：

- reject('错误信息').then(null,message=>{})

```javascript
console.log("start");
new Promise((resolve, reject) => {
    setTimeout(() => {
        reject("bye bye");
    }, 2000);
}).then(
    value => {
        console.log(value + " world");
    },
    value => {
        console.log("Error: ", value);
    }
);

一样的

console.log("start");
new Promise((resolve, reject) => {
    setTimeout(() => {
        // reject("bye bye");
        throw new Error("bye bye");
    }, 2000);
}).then(
    value => {
        console.log(value + " world");
    },
    value => {
        console.log("Error: ", value);
    }
);
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562554180575-fec7226b-23df-41a7-8494-ee4ec2d2699d.png#align=left&display=inline&height=255&name=image.png&originHeight=255&originWidth=812&size=49678&status=done&width=812)
- throw new Error('错误信息').catch(message=>{})
```javascript
console.log("start");
new Promise((resolve, reject) => {
    setTimeout(() => {
        throw new Error("bye");
    }, 2000);
})
    .then(value => {
        console.log(value + " world");
    })
    .then(error => {
        console.log("Error: ", error, error.message);
    });
```


- 推荐使用第二种，更加清晰好读，并且可以捕获前面的错误
- 强烈建议在所有队列最后都加上.catch(),以避免漏掉错误处理造成意想不到的问题

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562555590174-9fa29dd5-076e-49fd-bad3-54021a77d640.png#align=left&display=inline&height=145&name=image.png&originHeight=336&originWidth=696&size=164162&status=done&width=300)

<a name="R7jMa"></a>
### Promise.all

- 当所有子Promise都完成，该Promise完成，返回值是全部值的数组
- 有任何一个失败，该Promise失败，返回值是第一个失败的子Promise的结果
<a name="ksLPd"></a>
### 与.map连用、实现队列
![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562567609153-e5446117-c197-4993-8792-2b6f4c39fb93.png#align=left&display=inline&height=129&name=image.png&originHeight=328&originWidth=1270&size=309024&status=done&width=500)



