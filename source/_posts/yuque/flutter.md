
---

title: flutter

date: 2019-06-12 15:49:52 +0800

tags: []

---
<a name="VbVGI"></a>
## 一门跨全平台移动应用开发（这里主要是以Mac电脑来安装和开发）
- API:[https://flutterchina.club/web-analogs/](https://flutterchina.club/web-analogs/)
- 知乎flutter:[https://zhuanlan.zhihu.com/p/65033883](https://zhuanlan.zhihu.com/p/65033883)

![Group.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562754741414-068311e6-c9d7-4ed1-9f9d-0e1898aa5702.png#align=left&display=inline&height=2566&name=Group.png&originHeight=2566&originWidth=2160&size=1021288&status=done&width=2160)

<a name="YUYVq"></a>
## 安装过程：
1.下载Flutter<br />2.新建目录：/Users/fangcao/Documents/flutter_code<br />3.将flutter安装程序放在flutter_code
```bash
cd ~/flutter_code
unzip ~/Downloads/flutter_macos_v0.5.1-beta.zip
```
将flutter_macos_v0.5.1-beta.zip解压到flutter_code里面<br />4.在～/.bash_profile目录里面加入：export PATH=`pwd`/flutter/bin:$PATH<br />5.如果你的终端用了zshrc,就得：vim ~/.zshrc  最后添加 source ~/.bash_profile

这样全局的环境变量PATH安装成功

注意：google出的东西都需要翻墙下载，不过，这次google给我们提供了一个临时镜像，此镜像为临时镜像，并不能保证一直可用，读者可以参考详情请参考 [Using Flutter in China](https://flutter.dev/community/china) 以获得有关镜像服务器的最新动态。

```bash
export PUB_HOSTED_URL=https://pub.flutter-io.cn //国内用户需要设置
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn //国内用户需要设置
```

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562813192032-3ca134ec-108e-4503-96da-7f5e07e46ff2.png#align=left&display=inline&height=321&name=image.png&originHeight=366&originWidth=570&size=35328&status=done&width=500)

6. 接着运行
```bash
flutter doctor
```
检查安装哪些依赖,该命令检查您的环境并在终端窗口中显示报告<br />缺少的功能或者模块，它会给你提示，按照指示安装即可（一般ios和android软件安装配置完成即可，下面会讲解ios和android软件的安装和配置）。

该flutter工具使用Google Analytics匿名报告功能使用情况统计信息和基本崩溃报告。 这些数据用于帮助改进Flutter工具。Analytics不是一运行或在运行涉及flutter config的任何命令时就发送， 因此您可以在发送任何数据之前退出分析。要禁用报告，请执行flutter config --no-analytics并显示当前设置，然后执行flutter config。 请参阅[Google的隐私政策](https://www.google.com/intl/en/policies/privacy/)。

在vscode里面的终端：发现<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562582529319-93e4cdf5-5b67-49f4-92ad-aff910e595f3.png#align=left&display=inline&height=33&name=image.png&originHeight=33&originWidth=493&size=7697&status=done&width=493)<br />没有flutter,就运行一下source ~/.bash_profile<br />最后检查下echo $PATH 看看 是否已经添加到环境变量中

安装flutter插件<br />安装后，flutter doctor检查一下。

发现要进行如下安装：

```bash
brew update
brew install --HEAD usbmuxd
 brew link usbmuxd
 brew install --HEAD libimobiledevice
 brew install ideviceinstaller ios-deploy cocoapods
 pod setup
```

前端：vscode安装flutter，还要安装Dart sdk<br />安卓：![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562637579931-179f035b-3575-44f6-a70e-f6c1276eea85.png#align=left&display=inline&height=106&name=image.png&originHeight=106&originWidth=394&size=26295&status=done&width=394)<br />IOS:Xcode

详细步骤：[Flutter macOS 开发环境搭建笔记](https://www.yuque.com/fangcao/api/npae52)


<a name="jS0PR"></a>
## 开始HelloWorld
这里以最新的[Dart2](https://dart.dev/samples)为主

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562639010607-2e9aa575-5c1c-43e2-b1a4-e49f73d6995b.png#align=left&display=inline&height=150&name=image.png&originHeight=150&originWidth=300&size=7982&status=done&width=300)


1.[安装dart](http://dart.goodev.org/install/mac):[https://dart.dev/tutorials/web/get-started](https://dart.dev/tutorials/web/get-started)

```bash
brew tap dart-lang/dart
brew install dart --devel
```
如果你需要开发 web 应用，则还需要安装 Dartium 和 Content Shell：

```bash
$ brew tap dart-lang/dart
$ brew install dart --with-content-shell --with-dartium
```

2.看看flutterSDK是不是最新的，如果不是，就升级FlutterSDK

```bash
flutter upgrade
```

3.开启手机应用<br />IOS：
```bash
open -a Simulator
```
[Flutter 配置在 Android Studio](https://www.jianshu.com/p/f7d9bdaa3a9a)<br />[Android Studio添加Flutter开发](https://blog.csdn.net/u010976213/article/details/80241900)

如果发现报错了：<br />1.[flutter错误解决--Error running Gradle 错误](https://blog.csdn.net/mo911108/article/details/88603003)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562660065110-205248b0-9291-4f0e-9137-766f4aa64805.png#align=left&display=inline&height=687&name=image.png&originHeight=687&originWidth=1177&size=129742&status=done&width=1177)

2.flutter\packages\flutter_tools\gradle<br />打开文件进行修改，修改代码如下（其实也是换成阿里的路径就可以了）。<br />这一步有两种情况<br />1，flutter.gradle文件中repositories中是google() 和 jcenter()，<br />repositories{<br />google()<br />gcenter()<br />}<br />把google() 和 jcenter()这两行去掉。改为阿里的链接。<br />maven { url 'https://maven.aliyun.com/repository/google' }<br />maven { url 'https://maven.aliyun.com/repository/jcenter' }<br />maven { url 'http://maven.aliyun.com/nexus/content/groups/public' }

4.创建flutter程序

```bash
flutter create my_app
cd my_app
flutter run
flutter -h
```

5.VScode中常用的快捷键<br />R键：点击后热加载，直接查看预览效果<br />P键：在虚拟机中显示网格，工作中经常使用<br />O键：切换Android和IOS的预览模式<br />Q键：推出调试预览模式

<a name="PhD3u"></a>
## APP开启
[Xcode 9 —进阶的 iOS Simulator](http://www.cocoachina.com/articles/21986)<br />查询设备<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562662667389-5efbd27b-4e73-446d-b0a3-7506a01530a5.png#align=left&display=inline&height=103&name=image.png&originHeight=103&originWidth=637&size=22608&status=done&width=637)

选择运行在哪个模拟器上<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562662710033-689d7ae3-c908-4cd0-8a17-da5cbfa7de84.png#align=left&display=inline&height=32&name=image.png&originHeight=32&originWidth=647&size=7612&status=done&width=647)<br />运行在安卓上<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562662726451-2647fecd-0d51-4165-8c1c-7b3170d0d718.png#align=left&display=inline&height=29&name=image.png&originHeight=29&originWidth=641&size=9200&status=done&width=641)<br />运行在IOS上<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562662757925-72f8ccef-47d5-413e-a88d-93ba3bb5fa77.png#align=left&display=inline&height=18&name=image.png&originHeight=18&originWidth=639&size=6492&status=done&width=639)<br />运行在所有设备上

开始组件讲解<br />[https://www.imooc.com/video/18530](https://www.imooc.com/video/18530)

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Welcome to Flutter',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Hello World'),
        ),
        body: Center(
          child: Text(
            'Hello World,触发事件，在触发n秒后才执行，如果在触发时间的n秒内再次触发事件，那就以新的时间为准，n秒后才执行。总之，需要你在触发事件的n秒内不再触发新事件，我才执行。',
            textAlign: TextAlign.left,
            // maxLines: 2,
            // overflow: TextOverflow.fade,
            style: TextStyle(
                fontSize: 25.0,
                color: Color.fromARGB(120, 255, 0, 0),
                decoration: TextDecoration.underline,
                decorationStyle: TextDecorationStyle.solid),
          ),
        ),
      ),
    );
  }
}

```


<a name="oULxN"></a>
# [Flutter web](https://www.bilibili.com/video/av51954459?from=search&seid=16287043737660496372)
[https://dart.dev/web](https://dart.dev/web)
<a name="P1Ill"></a>
## 如何评价 Flutter for Web？
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

如果觉得webdev serve --auto restart 太麻烦，可以尝试 flutter pub global run webdev serve --auto restart

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562743943934-12349286-005a-4f42-99ae-6a045331a6f3.png#align=left&display=inline&height=490&name=image.png&originHeight=490&originWidth=1900&size=63009&status=done&width=1900)
<a name="MlPkn"></a>
### 5.打包发布
```bash
webdev build
```

flutter项目和flutter web项目的不同

![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562815590844-e73a4ee0-6a4f-4157-af0d-3db6c3558424.png#align=left&display=inline&height=254&name=image.png&originHeight=508&originWidth=1441&size=83258&status=done&width=720.5)<br />![image.png](https://cdn.nlark.com/yuque/0/2019/png/263301/1562815600343-104ddec6-25a6-41b0-9972-bc6961728d79.png#align=left&display=inline&height=206&name=image.png&originHeight=411&originWidth=1377&size=79621&status=done&width=688.5)<br />[s/](https://link.zhihu.com/?target=https%3A//flutter.github.io/samples/)

<a name="G63jn"></a>
# 文件配置说明
<a name="R0hSD"></a>
### [pubspec.yaml](https://book.flutterchina.club/chapter2/flutter_package_mgr.html)包管理
[资源管理](https://book.flutterchina.club/chapter2/flutter_assets_mgr.html)<br />[在Flutter中添加资源和图片](https://flutterchina.club/assets-and-images/)

```yaml

#name很重要，如果修改了name所有的dart的文件的import前引用的本地的文件啊的包名都需要修改
name: flutterdemo #包名
description: A new Flutter application.
 
dependencies:
  flutter:
    sdk: flutter
 
 #添加依赖packages ^表示适配和当前大版本一致的版本，~表示适配和当前小版本一致的版本
  cupertino_icons: ^0.1.2
  english_words: ^3.1.0
 # image_picker: ^0.4.8
 
dev_dependencies:
  flutter_test:
    sdk: flutter
 
  #启用国际化1
  flutter_localizations:
    sdk: flutter
 
#定义常量
 
#数组
server:
    - aaaaaa
    - bbbbbb
	- dddddd
#常量
age: 22         # int
boolitem: true  #定义一个boolean值
name: 'hello'   #定义一个string
 
 
flutter:
 
  # The following line ensures that the Material Icons font is
  # included with your application, so that you can use the icons in
  # the material Icons class.
  uses-material-design: true #启用国际化2
  # To add assets to your application, add an assets section, like this:
  #添加资源，不单单是图片，images是个和pubspec.yaml配置文件同级的目录，如果不同级，需要添加..
  assets:
        - images/park.jpg
        - images/lake.jpg
        - images/touxiang.jpg
  #  - images/a_dot_burr.jpeg
  #  - images/a_dot_ham.jpeg
   #字体设置
   fonts:
     - family: Schyler
       fonts:
       - asset: fonts/Schyler-Regular.ttf
        - asset: fonts/Schyler-Italic.ttf
           style: italic
     - family: Trajan Pro
       fonts:
      - asset: fonts/TrajanPro.ttf
      - asset: fonts/TrajanPro_Bold.ttf
        weight: 700

```
<a name="ywxn3"></a>
### name:包名
<a name="1d2oQ"></a>
### 引入图片资源
```yaml
#不同尺寸图片资源写法：
…/my_icon.png
…/2.0x/my_icon.png
…/3.0x/my_icon.png
```

<a name="h5A8w"></a>
### 读取文本
```dart
import 'package:flutter/services.dart' show rootBundle;
Future<String> loadAsset() async {
//读取文件是的路径，就是assets下配置的 
return await rootBundle.loadString('assets/config.json');
}
```

<a name="k9O5K"></a>
### 使用图片
```dart
//图片路径的配置
new AssetImage('graphics/background.png'),
```

<a name="mIhtk"></a>
### 加载依赖包中图片
```dart
//配置name的作用，需要读取其他外部package下的资源时
new AssetImage('icons/heart.png', package: 'my_icons')
```

<a name="EUeHG"></a>
### 支持字体的设置，可以使用自定义字体
```dart
style: new TextStyle( fontFamily: 'Schyler', fontSize: 24.0, ),
```

<a name="dOg8W"></a>
### 基本控件
flutter提供了一套完备的基本控件，最常用的有如下几个：

- Text ：Text提供了一个用来显示文本的一次性控件（即无状态）。
- Row, Column：这两个控件用来显示水平或垂直方向上的多个组件，并且是可伸缩的。
- Stack：可以将多个组件以一定的顺序排列，可以使用`Positioned`控件来指定组件在Stack中的顺序。
- Container: 是一个可视化的矩形控件，它可以使用`BoxDecoration`来进行外观装饰，装饰内容可以是背景，边框和阴影等。Container也有外边距，内边距等属性，也可以约束自身的大小，另外值得一提的是Container还可以利用矩阵在三维控件内做转换。

下面结合一些基本的控件来自定义我们的组件并构建应用：<br />


<a name="u0vmi"></a>
# [开发Packages和插件](https://flutterchina.club/developing-packages/)

- [Package 介绍](https://flutterchina.club/developing-packages/#package-%E4%BB%8B%E7%BB%8D)
  - [Package 类型](https://flutterchina.club/developing-packages/#types)
- [Developing Dart packages](https://flutterchina.club/developing-packages/#dart)
  - [Step 1: 开发Dart包](https://flutterchina.club/developing-packages/#step-1-%E5%BC%80%E5%8F%91dart%E5%8C%85)
  - [Step 2: 实现package](https://flutterchina.club/developing-packages/#step-2-%E5%AE%9E%E7%8E%B0package)
- [开发插件包](https://flutterchina.club/developing-packages/#plugin)
  - [Step 1: 创建 package](https://flutterchina.club/developing-packages/#step-1-%E5%88%9B%E5%BB%BA-package)
  - [Step 2: 实现包 package](https://flutterchina.club/developing-packages/#edit-plugin-package)
    - [Step 2a: 定义包API（.dart）](https://flutterchina.club/developing-packages/#step-2a-%E5%AE%9A%E4%B9%89%E5%8C%85apidart)
    - [Step 2b: 添加Android平台代码（.java / .kt）](https://flutterchina.club/developing-packages/#step-2b-%E6%B7%BB%E5%8A%A0android%E5%B9%B3%E5%8F%B0%E4%BB%A3%E7%A0%81java--kt)
    - [Step 2c: 添加iOS平台代码 (.h+.m/.swift)](https://flutterchina.club/developing-packages/#step-2c-%E6%B7%BB%E5%8A%A0ios%E5%B9%B3%E5%8F%B0%E4%BB%A3%E7%A0%81-hmswift)
    - [Step 2d: 连接API和平台代码](https://flutterchina.club/developing-packages/#step-2d-%E8%BF%9E%E6%8E%A5api%E5%92%8C%E5%B9%B3%E5%8F%B0%E4%BB%A3%E7%A0%81)
- [添加文档](https://flutterchina.club/developing-packages/#%E6%B7%BB%E5%8A%A0%E6%96%87%E6%A1%A3)
  - [API documentation](https://flutterchina.club/developing-packages/#api-documentation)
- [发布 packages](https://flutterchina.club/developing-packages/#publish)
- [处理包的相互依赖](https://flutterchina.club/developing-packages/#dependencies)
  - [Android](https://flutterchina.club/developing-packages/#android)
  - [iOS](https://flutterchina.club/developing-packages/#ios)
  - [解决冲突](https://flutterchina.club/developing-packages/#%E8%A7%A3%E5%86%B3%E5%86%B2%E7%AA%81)

<a name="yHhPh"></a>
# [Flutter应用](https://book.flutterchina.club/chapter2/first_flutter_app.html)代码讲解
```

<a name="EpZQi"></a>
# 原生App项目集成flutter混合开发详细指南




参考：<br />[Flutter视频学习](https://www.imooc.com/video/18527)<br />[Flutter实战](https://book.flutterchina.club/chapter1/dart.html)<br />[Flutter中文网](https://flutterchina.club/)<br />[Dart官网](https://dart.dev/) 以前的名字叫https://www.dartlang.org<br />[Dart](http://dart.goodev.org/) [http://dart.goodev.org/](http://dart.goodev.org/)<br />[Dartpad](https://dartpad.dartlang.org/)<br />[跨平台的应用程序](https://www.yuque.com/fangcao/api/zq2og4)

