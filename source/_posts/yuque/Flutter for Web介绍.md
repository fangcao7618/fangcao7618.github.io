
---

title: Flutter for Web介绍

date: 2019-07-09 18:07:25 +0800

tags: []

---
<a name="fUC4C"></a>
# 如何评价 Flutter for Web？
针对 Web 的 Flutter 框架的技术预览版：[https://flutter.dev/web](https://link.zhihu.com/?target=https%3A//flutter.dev/web)<br />Github 仓库：[https://](https://link.zhihu.com/?target=https%3A//github.com/flutter/flutter_web)[https://github.com/flutter/flutter_web](https://github.com/flutter/flutter_web)[ter_web](https://link.zhihu.com/?target=https%3A//github.com/flutter/flutter_web)<br />示例程序：[https://](https://link.zhihu.com/?target=https%3A//flutter.github.io/samples/)[https://flutter.github.io/samples/](https://flutter.github.io/samples/)

<a name="6xiRI"></a>
## Flutter for Web架构图

[https://dart.dev/tutorials/web/get-started](https://dart.dev/tutorials/web/get-started)

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562722204560-958c18bc-8fbd-4682-9914-911c11fccdcd.png#align=left&display=inline&height=368&name=image.png&originHeight=368&originWidth=720&size=133104&status=done&width=720)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562722231288-5375dd0f-31f8-443c-af26-1b3fd5ab265e.png#align=left&display=inline&height=144&name=image.png&originHeight=144&originWidth=1354&size=81299&status=done&width=1354)


<a name="BLP3n"></a>
### 1.安装 Dart

```bash
$ pub global activate webdev
$ pub global activate stagehand
```

<a name="npv3F"></a>
### 2.安装 [webdev](https://dart.dev/tools/webdev) 和 [stagehand:](https://pub.dev/packages/stagehand)
[Stagehand](https://github.com/dart-lang/stagehand)- A Dart project generator
```bash
 $ pub global activate webdev
 $ pub global activate stagehand
```

<a name="IZOwC"></a>
### 3.创建一个wep app

```bash
mkdir quickstart
cd quickstart
stagehand web-simple
pub get 获取包
```

<a name="wlk83"></a>
### 4.运行app

```bash
webdev serve
webdev serve --auto restart 加入了热重新加载
```

如果觉得webdev serve --auto restart 太麻烦，可以尝试 flutter pub global run webdev serve --auto restart

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562743943934-12349286-005a-4f42-99ae-6a045331a6f3.png#align=left&display=inline&height=490&name=image.png&originHeight=490&originWidth=1900&size=63009&status=done&width=1900)
<a name="MlPkn"></a>
### 5.打包发布
```bash
webdev build
```

flutter项目和flutter web项目的不同

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562815590844-e73a4ee0-6a4f-4157-af0d-3db6c3558424.png#align=left&display=inline&height=254&name=image.png&originHeight=508&originWidth=1441&size=83258&status=done&width=720.5)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562815600343-104ddec6-25a6-41b0-9972-bc6961728d79.png#align=left&display=inline&height=206&name=image.png&originHeight=411&originWidth=1377&size=79621&status=done&width=688.5)<br />[s/](https://link.zhihu.com/?target=https%3A//flutter.github.io/samples/)


