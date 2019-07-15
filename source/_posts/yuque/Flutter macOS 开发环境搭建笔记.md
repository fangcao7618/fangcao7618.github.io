
---

title: Flutter macOS 开发环境搭建笔记

date: 2019-07-09 10:06:19 +0800

tags: []

---
本文主要记录在 macOS 系统上搭建 Flutter 开发环境的过程，以及遇到的问题和解决办法，供大家参考。

<a name="FD1Z2"></a>
## 1. 系统环境
Flutter 同时支持在 Windows、macOS、Linux 等主流操作系统上进行开发，如下图所示：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016980-00212f36-eb7c-4e06-9f06-083bc7f012e8.png#align=left&display=inline&height=686&originHeight=686&originWidth=1516&size=0&status=done&width=1516)](https://file.kangzubin.com/blog/static/20181118/1.png)<br />本文的环境搭建主要参考了官方的 [Get started](https://flutter.io/docs/get-started/install) 教程，同时你也可以在 [Flutter 中文网](https://flutterchina.club/get-started/install/) 或者 [Flutter 中文开发者论坛](http://doc.flutter-dev.cn/get-started/install/) 查阅相关中文翻译文档。<br />我们这里进行实践的操作系统信息为：
> macOS Mojave 10.14 (64-bit)

<a name="fXxEm"></a>
## [](https://kangzubin.com/flutter-dev-env/#2-%E5%AE%89%E8%A3%85-Flutter-%E5%92%8C-Dart-SDK)2. 安装 Flutter 和 Dart SDK
<a name="4yXil"></a>
### [](https://kangzubin.com/flutter-dev-env/#2-1-%E7%BD%91%E7%BB%9C%E7%8E%AF%E5%A2%83)2.1 网络环境
在安装之前，先插个题外话，由于众所周知的原因，Google 提供的服务在中国大陆一直都是无法访问或者速度很慢，所以在下载一些资源时，我们通常需要翻墙或者选择一个与官方同步的可信的镜像站点作为替代。不过，Flutter 官方也很贴心地专门为中国用户写了一个教程，如何更快的下载资源、搭建环境以及执行 flutter 相关命令：

- [Using Flutter in China](https://flutter.io/community/china)
<a name="d2yDg"></a>
### [](https://kangzubin.com/flutter-dev-env/#2-2-%E8%8E%B7%E5%8F%96-Flutter)2.2 获取 Flutter
根据 [Flutter SDK Archive](https://flutter.io/docs/development/tools/sdk/archive?tab=macos) 页面的介绍，我们可以选择安装三种不同版本的 Flutter，分别如下：

- Dev channel：开发版本<br />
- Beta channel：测试版本<br />
- Master channel：最新版本，直接从 [GitHub repo](https://github.com/flutter/flutter) 中克隆获取最新的 SDK。<br />

由于 Flutter 目前还没正式发布 Release 版本，所以我们建议选择相对比较稳定 Beta 版 SDK。在本文撰写的时候，最新的为 v0.10.2-beta，下载地址如下：

- [https://storage.googleapis.com/flutter_infra/releases/beta/macos/flutter_macos_v0.10.2-beta.zip](https://storage.googleapis.com/flutter_infra/releases/beta/macos/flutter_macos_v0.10.2-beta.zip)

但由于这个 URL 在国内下载特别慢（400+ MB），根据 [Using Flutter in China](https://flutter.io/community/china) 介绍，我们可以改成如下国内镜像地址进行下载，替换前缀为 [https://storage.flutter-io.cn](https://storage.flutter-io.cn/) 即可：

- [https://storage.flutter-io.cn/flutter_infra/releases/beta/macos/flutter_macos_v0.10.2-beta.zip](https://storage.flutter-io.cn/flutter_infra/releases/beta/macos/flutter_macos_v0.10.2-beta.zip)
<a name="APuq6"></a>
### [](https://kangzubin.com/flutter-dev-env/#2-3-%E5%AE%89%E8%A3%85-Flutter)2.3 安装 Flutter
我们把上述下载的 flutter_macos_v0.10.2-beta.zip 拷贝到 $HOME/Flutter/ 目录下（可自行选择任意其他目录），然后进行解压：

| 12 | $ cd ~/Flutter$ unzip ./flutter_macos_v0.10.2-beta.zip |
| :--- | :--- |

此时，flutter 命令就在解压后的 flutter/bin 目录下。比如在我们这里，其完整路径为：$HOME/Flutter/flutter/bin/flutter。<br />接下来，我们需要把 flutter 命令所在目录添加到系统的 PATH 变量中，方便后续在任何终端直接使用，而不用切换到特定目录。<br />我们可直接在命令行中执行 export PATH=$PATH:$HOME/Flutter/flutter/bin，不过该命令只能在当前的终端窗口暂时设置 PATH 变量，关闭终端后就失效了。<br />因此，要想永久地将 Flutter 添加到 PATH 中，需要在 $HOME 用户目录下的 .bashrc、.bash_profile 或者 .vimrc 等文件中（不同系统终端环境可能会不太一样）添加如上命令。由于我的 macOS 的终端环境使用的是 ZSH，所以我需要在 $HOME/.zshrc 文件中进行添加。<br />此外，对于国内用户在使用 flutter 命令时，同样地，我们需要切换镜像源以加快速度，节省时间。根据[文档](https://github.com/flutter/flutter/wiki/Using-Flutter-in-China)，需要为此设置两个环境变量：PUB_HOSTED_URL 和 FLUTTER_STORAGE_BASE_URL，然后再运行 Flutter 命令行工具。<br />这里推荐 Flutter 官方中文社区的镜像如下，当然我们可以[选择其他的源](https://flutter-io.cn/)。

| 12 | export PUB_HOSTED_URL=https://pub.flutter-io.cnexport FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn |
| :--- | :--- |

综上，这里我们需要在 $HOME/.zshrc 文件中添加如下几行命令：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016654-12c68af2-709b-41e7-abbd-5d2ef6703d7a.png#align=left&display=inline&height=384&originHeight=384&originWidth=1296&size=0&status=done&width=1296)](https://file.kangzubin.com/blog/static/20181118/2.png)
<a name="2-4-Dart-SDK"></a>
### [](https://kangzubin.com/flutter-dev-env/#2-4-Dart-SDK)2.4 Dart SDK
我们知道，Flutter 使用 Dart 语言进行开发应用程序，为了方便起见，我们下载的 Flutter SDK 已经同时包含了 Dart SDK，放在下面目录中：

- flutter/bin/cache/dart-sdk
<a name="tpcuo"></a>
## [](https://kangzubin.com/flutter-dev-env/#3-%E5%B9%B3%E5%8F%B0%E8%AE%BE%E7%BD%AE-%E7%BC%96%E8%AF%91%E7%8E%AF%E5%A2%83)3. 平台设置/编译环境
在添加完 flutter 命令到 PATH 后，我们可以打开终端，在命令行中执行 flutter doctor，进行检查相关工具或者配置是否完整，我们第一次运行时，可能会得到如下图信息：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016676-9254aeef-633c-4122-bf9a-446bb8e6ed8d.png#align=left&display=inline&height=609&originHeight=609&originWidth=1200&size=0&status=done&width=1200)](https://file.kangzubin.com/blog/static/20181118/3.png)<br />我们看到一堆问题，接下来，我们只要根据上述结果和建议，一步步进行完善配置就好了。<br />此外，macOS 支持为 iOS 和 Android 开发 Flutter 应用程序，所以我们同时也需要先完成这两个平台的相关编译环境配置，以便能够构建并运行第一个 Flutter Demo。
<a name="HsEna"></a>
### [](https://kangzubin.com/flutter-dev-env/#3-1-iOS-%E9%85%8D%E7%BD%AE)3.1 iOS 配置

- 安装 Xcode 9.0+ 或更新版本；<br />
- 设置 iOS 模拟器；<br />
- 安装 [Homebrew](https://brew.sh/)、[Cocoapod](https://cocoapods.org/)、[Carthage](https://github.com/Carthage/Carthage) 等 iOS 开发必要工具；<br />
- 安装 iOS 真机调试工具：<br />
| 12345 | $ brew update$ brew install --HEAD usbmuxd$ brew link usbmuxd$ brew install --HEAD libimobiledevice$ brew install ideviceinstaller ios-deploy |
| :--- | :--- |

PS：如果你安装上述工具出行错误，请参考这个 [issues](https://github.com/flutter/flutter/issues/22595)，先卸载 usbmuxd 和 libimobiledevice 后重新安装，加上 --HEAD。
<a name="I4fXA"></a>
### [](https://kangzubin.com/flutter-dev-env/#3-2-Android-%E9%85%8D%E7%BD%AE)3.2 Android 配置

- 下载安装 Android Studio，然后启动根据“安装向导”进行相关初始化配置；<br />
- 设置你的 Android 设备<br />
- 设置 Android 模拟器<br />
> 更详细的教程请参考官方 [Platform setup](https://flutter.io/docs/get-started/install/macos#platform-setup)，或者上述相关中文翻译文档。

<a name="8Kxsq"></a>
## [](https://kangzubin.com/flutter-dev-env/#4-%E9%85%8D%E7%BD%AE-IDE)4. 配置 IDE
接下来我们需要配置一下 Flutter 的集成开发环境（IDE），以方便我们进行开发和调试。<br />我们可以使用任何文本编辑器与命令行工具来构建 Flutter 应用程序。但这里推荐在 Android Studio、IntelliJ 或 VS Code 等优秀的编辑器上添加 Flutter 开发插件，即可获得代码自动补全，语法高亮，Widget 编辑助手，运行和调试的支持等一系列实用的功能。
<a name="y59UK"></a>
### [](https://kangzubin.com/flutter-dev-env/#4-1-%E5%91%BD%E4%BB%A4%E8%A1%8C)4.1 命令行

- 创建工程

Create a new Flutter project in the specified directory.

| 1 | flutter create <output directory> |
| :--- | :--- |

- 连接设备

List all connected devices.

| 1 | flutter devices |
| :--- | :--- |

- 运行工程

Run your Flutter application on an attached device or in an emulator.

| 1 | flutter run [options] |
| :--- | :--- |

<a name="4-2-Visual-Studio-Code"></a>
### [](https://kangzubin.com/flutter-dev-env/#4-2-Visual-Studio-Code)4.2 Visual Studio Code
VS Code 是一个轻量级编辑器，支持 Flutter 运行和调试。

- 安装 VS Code

我们可以在[这里下载](https://code.visualstudio.com/download)并安装最新版本的 VS Code，本文安装的版本为 1.29.0

- 安装 Flutter 和 Dart 插件

启动 VS Code，在菜单栏中选择 View（查看）-> Command Palette…（命令面板…），输入 ‘install’，然后选择 Extensions: Install Extension 安装扩展，接着在搜索框输入 ‘flutter’， 在搜索结果列表中选择 ‘Flutter’，点击 Install（安装），同时会自动安装 ‘Dart’ 依赖，最后重启 VS Code 即可生效。

- 验证配置

打开 View（查看）-> Command Palette…（命令面板…），输入 ‘doctor’，然后选择 Flutter: Run Flutter Doctor，进行检查：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638017324-03180a34-344a-44b1-ad0d-12bf4e48015a.png#align=left&display=inline&height=130&originHeight=130&originWidth=1210&size=0&status=done&width=1210)](https://file.kangzubin.com/blog/static/20181118/4.png)<br />查看 OUTPUT 窗口中的输出是否有问题，并按建议解决即可。<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016996-00236b63-5126-4703-9647-c38b6d1207ea.png#align=left&display=inline&height=672&originHeight=672&originWidth=1426&size=0&status=done&width=1426)](https://file.kangzubin.com/blog/static/20181118/5.png)<br />至此，VS Code 的 Flutter 开发环境搭建好了。
<a name="4-3-Android-Studio"></a>
### [](https://kangzubin.com/flutter-dev-env/#4-3-Android-Studio)4.3 Android Studio
Android Studio 为 Flutter 提供了更加完整的 IDE 体验，毕竟它们都是 Google 的“亲儿子”。

- 安装 Android Studio

我们可以在[这里下载](https://developer.android.com/studio/install?hl=zh-cn)并安装最新版本的 Android Studio（推荐 3.0+ 或更高版本），本文安装的版本为 3.2.1，此外 Android Studio 依赖 Java 环境，我们这里安装的 JDK 版本如下：
> Java 8 Update 191 (1.8.0_191-b12)

当然，我们也可以选择使用 [IntelliJ IDEA](https://www.jetbrains.com/idea/download/)。

- 安装 Flutter 和 Dart 插件

启动 Android Studio，打开插件设置（在 macOS 上为 Preferences -> Plugins），然后选择 Browse repositories… 按钮，<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016772-4e65e02f-0c61-4b0d-b305-ce612e9e5348.png#align=left&display=inline&height=1042&originHeight=1042&originWidth=1728&size=0&status=done&width=1728)](https://file.kangzubin.com/blog/static/20181118/6.png)<br />搜索 Flutter 插件，点击 Install（安装）<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016676-dc8fa698-f24d-471a-ad04-9ba7fd9a9313.png#align=left&display=inline&height=562&originHeight=562&originWidth=1532&size=0&status=done&width=1532)](https://file.kangzubin.com/blog/static/20181118/7.png)<br />此时会自动提示安装 Dart 插件，点击 Yes 接受即可。<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016727-23c6235a-141f-4e3b-8506-c5a44d3bf593.png#align=left&display=inline&height=187&originHeight=187&originWidth=500&size=0&status=done&width=500)](https://file.kangzubin.com/blog/static/20181118/8.png)<br />最后，重启 Android Studio，Flutter 开发环境就搭建好了。
<a name="Lsrl1"></a>
### [](https://kangzubin.com/flutter-dev-env/#4-4-%E5%A4%A7%E5%8A%9F%E5%91%8A%E6%88%90)4.4 大功告成
当我们完成上面所有开发环境的配置，并通过 USB 连接上真机设备或者打开 iOS/Android 模拟器，然后再执行 flutter doctor 可得到如下结果，一切 OK 了：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016504-118731e5-42bd-4335-8157-abaa2af43c48.png#align=left&display=inline&height=414&originHeight=414&originWidth=1260&size=0&status=done&width=1260)](https://file.kangzubin.com/blog/static/20181118/9.png)
<a name="5-Hello-World"></a>
## [](https://kangzubin.com/flutter-dev-env/#5-Hello-World)5. Hello World
这部分我们简单介绍一下如何创建一个 Flutter 的 Hello World 工程。上面提到，我们可以使用命令行、VS Code 或者 Android Studio/IntelliJ 等作为开发环境，综合比较，我们推荐 Android Studio。<br />启动 Android Studio，如下图，选择 Start a new Flutter project（或者在菜单栏选择 File -> New Flutter Project）<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638017520-d0c1a495-2c32-4ab3-a04d-dee4add790a2.png#align=left&display=inline&height=928&originHeight=928&originWidth=1364&size=0&status=done&width=1364)](https://file.kangzubin.com/blog/static/20181118/10.png)<br />接下来，我们可以参考官方的 [Test drive](https://flutter.io/docs/get-started/test-drive?tab=androidstudio) 教程以及 Android Studio 的向导，创建工程，然后编译运行，并体验 Flutter 的热重载（Hot Reload），详见上述教程，我们这里不再赘述。<br />这里需要注意的是，当我们在 Android Studio 创建新的 Flutter 工程，或者打开一个已有的 Flutter 工程时，可能会提示没有配置 Flutter 或者 Dart SDK 环境，如下图：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016651-a50e4cae-743e-4e45-ac01-09b200cf5219.png#align=left&display=inline&height=166&originHeight=166&originWidth=1170&size=0&status=done&width=1170)](https://file.kangzubin.com/blog/static/20181118/11.png)<br />此时，我们需要打开 Android Studio 的偏好设置（Preferences），手动配置相关路径。<br />首先选择 Preferences -> Languages & Frameworks -> Flutter，填写 Flutter SDK path，如下图所示，我们这里填写的路径为 $HOME/Flutter/flutter（取决于你 Flutter 的安装路径）：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016793-77447872-9660-4001-848f-42dad0344da3.png#align=left&display=inline&height=1016&originHeight=1016&originWidth=1748&size=0&status=done&width=1748)](https://file.kangzubin.com/blog/static/20181118/12.png)<br />同样地，在左侧选中 Dart，然后填写 Dart SDK path，如下图，我们这里填写的路径为 $HOME/Flutter/flutter/bin/cache/dart-sdk（取决于你 Flutter 的安装路径）：<br />[![](https://cdn.nlark.com/yuque/0/2019/png/263301/1562638016772-638590cf-8a62-4bff-9163-2839ec860902.png#align=left&display=inline&height=1016&originHeight=1016&originWidth=1728&size=0&status=done&width=1728)](https://file.kangzubin.com/blog/static/20181118/13.png)
<a name="QVfn5"></a>
## [](https://kangzubin.com/flutter-dev-env/#6-Flutter-%E7%9B%B8%E5%85%B3%E8%B5%84%E6%BA%90)6. Flutter 相关资源

- Flutter 官网：[https://flutter.io/](https://flutter.io/)
- Flutter GitHub 项目：[https://github.com/flutter/flutter](https://github.com/flutter/flutter)
- Flutter 社区中文资源（官方）：[https://flutter-io.cn/](https://flutter-io.cn/)
- Flutter 中文网：[https://flutterchina.club/](https://flutterchina.club/)
- Flutter 中文开发者论坛：[http://flutter-dev.cn/](http://flutter-dev.cn/)
- Flutter 中文文档：[http://doc.flutter-dev.cn/](http://doc.flutter-dev.cn/)
- Flutter 中文 CodeLabs：[https://codelabs.flutter-io.cn/](https://codelabs.flutter-io.cn/)
- Flutter 示例项目：[https://itsallwidgets.com/](https://itsallwidgets.com/)
- [https://github.com/Solido/awesome-flutter](https://github.com/Solido/awesome-flutter)
- [https://github.com/awesome-tips/flutter-resources](https://github.com/awesome-tips/flutter-resources)

转自：[https://kangzubin.com/flutter-dev-env/](https://kangzubin.com/flutter-dev-env/)

