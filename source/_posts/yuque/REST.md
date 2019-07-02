
---

title: REST

date: 2019-07-01 17:22:43 +0800

tags: []

---
<a name="5Ayik"></a>
## REST是什么？
- 万维网软件架构风格
- 用来创建网络服务
<a name="AS1xl"></a>
## 为何叫REST

- Representational State Transfer
- Representational:数据的表现形式（JSON、XML......）
- State:当前状态或者数据
- Transfer:数据传输
<a name="zHPgV"></a>
## 通过REST的6个限制详细了解它
<a name="asO2E"></a>
#### 客户-服务器（Client-Server）

- 关注点分离
- 服务端专注数据存储，提升了简单性
- 前端专注用户界面，提升了可移植性
<a name="Hh7Sh"></a>
#### 无状态（Stateless）

- 所有用户会话信息都保存在客户端
- 每次请求必须包括所有信息，不能依赖上下文信息
- 服务端不用保存会话信息，提升了简单性、可靠性、可见性
<a name="LYe0i"></a>
#### 缓存（Cache）

- 所有服务端响应都要被标为可缓存或不可缓存
- 减少前后端交互，提升了性能
<a name="9at8r"></a>
#### 统一接口（Uniform Interface）

- 接口设计尽可能统一通用，提升了简单性、可见性
- 接口与实现解耦，使前后端可以独立开发迭代
<a name="TRTsj"></a>
#### 分层系统（Layered System）

- 每层只知道相邻的一层，后面隐藏的就不知道了
- 客户端不知道是和代理还是真实服务器通信
- 其他层：安全层、负载均衡、缓存层等
<a name="Z3OA0"></a>
#### 按需代码（Code-On-Demand可选）

- 客户端可以下载运行服务端传来的代码（比如JS）
- 通过减少一些功能，简化了客户端

<a name="vvlPZ"></a>
## RESTful API简介
<a name="MFsJu"></a>
### 什么是RESTful API？
符合REST架构风格的API
<a name="4UGjD"></a>
### RESTful API 具体什么样子？
基本的URI，如：https//api.github.com/users<br />标砖HTTP方法，如GET，POST，PUT，PATCH，DELETE<br />传输的数据媒体类型，如：JSON，XML
<a name="WVRRB"></a>
### 现实举例
GET /users#获取user列表<br />GET /users/12#查看某个具体的user<br />POST /users#新建一个user<br />PUT /users/12#更新user12<br />DELETE/users/12 #删除user12

github接口文档：[https://developer.github.com/v3/repos/](https://developer.github.com/v3/repos/)

GitHub API示例








<br />

