
---

title: 通过 ngrok 实现 ssh 内网穿透

date: 2019-06-11 10:32:02 +0800

tags: []

---
<a name="sBcEB"></a>
### ngrok
用 ssh 访问一台主机，如果和主机在一个局域网中或者主机拥有公网 IP，就可以使用 ssh 命令直接连接主机的 IP 地址，但是大部分公司和家庭内部都是局域网，并不能给局域网内的每一台主机都分配一个公网 IP，这时候就需要进行内网穿透，才能从外部连接到局域网内的主机。<br />ngrok 是一个反向代理工具，可以实现将内网的端口暴露到公网，通过 ngrok，也能将 ssh 使用的端口暴露出去，以此实现 ssh 的内网穿透。
<a name="x1f25"></a>
### 注册并下载 ngrok
访问 [https://ngrok.com/](https://ngrok.com/) 注册 ngrok 账号并下载 ngrok 客户端。
<a name="KHUYu"></a>
### 查看 ngrok 的 token
访问 [https://dashboard.ngrok.com/auth](https://dashboard.ngrok.com/auth) 查看 token并复制。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220387673-d86bc6f3-0819-4920-9150-b84294d3fd47.png#align=left&display=inline&height=130&name=image.png&originHeight=130&originWidth=606&size=48864&status=done&width=606)
<a name="A8baD"></a>
### 在内网机器上启动 ngrok
连接 ngrok 账号
```
ngrok authtoken 5TqUhMnum6ntDE8Z5HkNb_49F9ffzzcV9V7pKLVdDYc
```
启动 ngrok 并打开 22 端口转发
```
ngrok tcp 22 --log=stdout > "$HOME/ngrok.log" --region ap &
```
其中 region 的 ap 代表 ngrok 新加坡节点，访问速度相比美国节点会快一些。访问 [https://ngrok.com/docs#config-options](https://ngrok.com/docs#config-options) 可以查看支持的所有区域。<br />访问 `http://127.0.0.1:4040`。<br />可以看到一个tcp开头的地址，通过访问这个地址，就可以转发到本机的 22 端口上。<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1560220374479-eab9837f-3df4-4d3b-bf53-2f03678abcee.png#align=left&display=inline&height=181&name=image.png&originHeight=181&originWidth=603&size=44348&status=done&width=603)
<a name="fDLJA"></a>
### 通过 ssh 访问内网机器
查看到转发地址后，就可以在外网通过 ssh 命令访问内网机器来。以上图为例，ssh 访问的命令是：
```
ssh -p 10502 username@0.tcp.ap.ngrok.io
```
<a name="R8uO4"></a>
### 需要注意的问题
由于所有流量都要经过 ngrok 服务器，而 ngrok 的服务节点又只有美国、新加坡等地，所以速度上还是比较慢的。另外，如果 ngrok 的服务节点存在安全隐患的话，存在敏感内容的泄漏的可能性。


