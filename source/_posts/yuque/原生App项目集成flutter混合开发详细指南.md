
---

title: 原生App项目集成flutter混合开发详细指南

date: 2019-07-12 13:58:49 +0800

tags: []

---
<a name="Pe5ZB"></a>
### 方案选择
目前主流的混合开发方案有两种集成方式：<br />**源码集成：** 也就是谷歌官方提供的方案[[github.com/flutter/flu…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fflutter%2Fflutter%2Fwiki%2FAdd-Flutter-to-existing-apps)]<br />**产物集成：** Flutter项目单独开发，开发完成后发布成aar包或者iOS的framework形式，原生项目依赖flutter输出的制品即可。具体可以参考闲鱼的文章<br />![](https://cdn.nlark.com/yuque/0/2019/webp/263301/1562910991738-2d68621f-466e-4bfe-912f-c15de452cc2c.webp#align=left&display=inline&height=534&originHeight=534&originWidth=1280&size=0&status=done&width=1280)<br />两种方式各有优劣，其实产物集成更好一些，不过即使是进行产物集成，也需要弄懂源码集成的方式，因为当有很多和原生交互的功能进行开发的时候，源码集成的方式可以直接调试会方便很多。<br />根据目前我们的情况：<br />1.参与人员都要进行flutter开发、<br />2.持续发布和构建我可以修改控制<br />我们现在这个项目选择了**源码集成**的方式。
<a name="YUyoJ"></a>
### 为原生项目集成flutter
整个的集成方案是参考谷歌方法：[[github.com/flutter/flu…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fflutter%2Fflutter%2Fwiki%2FAdd-Flutter-to-existing-apps)]，但是有一些不一样，我是创建了一个flutter项目后，在原生的项目中使用`git submodule`的形式进行管理的。
<a name="nj9vl"></a>
#### 1.创建flutter module project
我们假定已经有了原生的项目`Native-iOS`和`Native-Android`；现在我们需要创建我们的flutter项目。

1. 把我们的flutter的channel切换到master(master分支下是flutter的preview版本)<br />`flutter channel master`
1. 创建flutter模块的项目<br />`flutter create -t module {moduleName}`<br />我这里创建一个flutter的模块项目叫`flutter_module`
```
➜ flutter create -t module flutter_module
Creating project flutter_module...
  flutter_module/test/widget_test.dart (created)
  ...
  ...
  flutter_module/.idea/workspace.xml (created)
Running "flutter packages get" in flutter_module...                 7.2s
Wrote 12 files.
All done!
Your module code is in flutter_module/lib/main.dart.
复制代码
```

1. 创建成功后我们可以看一下目录结构
```
➜  flutter_module git:(master) ✗ tree -L 2 -a
.
├── .android
│   ├── Flutter
│   ├── app
│   ├── ...
├── .gitignore
├── .ios
│   ├── Config
│   ├── Flutter
│   ├── ...
│   └── Runner.xcworkspace
├── lib
│   └── main.dart
├── pubspec.lock
├── pubspec.yaml
└── test
    └── widget_test.dart
复制代码
```

1. 在flutter的模块项目中包含有一个隐藏的`.android`和`.ios`目录这个目录下是可运行的Android和iOS项目，我们的flutter代码还是在`lib`下编写，注意在`.android`和`.ios`目录下都有一个Flutter目录，这个是我们flutter的库项目了。也就是Android用来生成aar，iOS用来生产framework的库。如果我们用`flutter create xxx` 生成的纯flutter项目是没有这个Flutter目录的。
1. 把该项目使用git管理起来，稍后我们要在native项目中以子模块的形式添加进去。
```
➜  cd flutter_module
➜  git init
Initialized empty Git repository in /Users/zhiqiangdeng/Documents/ProjectSource/FlutterProject/flutter_module/.git/
➜  flutter_module git:(master) ✗
复制代码
```
~~初始化git仓库后我们先编辑一下项目下的`.gitignore`文件，当前这个文件是把项目下的--`.ios`和`.android`忽略掉的。这个两个项目我们需要跟踪一下，大家可以去github上找一下iOS和Android的gitignore模版文件，然后添加到这个两个目录中，然后把顶层目录的文件作出如下修改，删除`.android和.ios`添加`.ios/Flutter/Generated.xcconfig`~~<br />~~.gitignore文件:~~
```
-.android/
-.ios/
+.ios/Flutter/Generated.xcconfig
复制代码
```
**上面的内容做一些更正，不需要编辑.gitignore文件使用自动生成的即可。`.android`和`.ios`目录在每次执行`flutter packages get`命令会自动生成（团队其他成员拉取代码后没有.android和.ios执行一下flutter packages get即可）**

4. 提交你的flutter模块项目到你的git服务器(我提交到github上了[[github.com/zakiso/flut…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fzakiso%2Fflutter-module-demo.git)]大家可以参考)
```
git remote add origin {你的flutter module的仓库地址}
git push origin master
复制代码
```
<a name="zG9h6"></a>
### 2.给iOS项目集成flutter
1.进入我们原生的iOS项目根目录中，为它添加一个git submodule，把我们的flutter项目拉取下来.
```
git submodule add {你的flutter module的仓库地址}
git submodule update
复制代码
```
2.在项目的`Podfile`文件中添加下面的代码，在每次执行pod install会运行podhelper.rb
```
platform :ios, '8.0'
use_frameworks!
target 'MyApp' do
  pod 'AFNetworking', '~> 2.6'
  xxxx
end
#添加如下两行代码，路径修改为我们的fluter module的路径
flutter_application_path = './flutter-module-demo'
  eval(File.read(File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')), binding)
复制代码
```
3.打开Xcode关闭bitcode配置`Build Settings->Build Options->Enable Bitcode`<br />4.添加编译脚本，打开Xcode在 Build Phases中添加`New Run Script Phase`在里面填入如下脚本
```
"$FLUTTER_ROOT/packages/flutter_tools/bin/xcode_backend.sh" build
"$FLUTTER_ROOT/packages/flutter_tools/bin/xcode_backend.sh" embed
复制代码
```
![](https://cdn.nlark.com/yuque/0/2019/webp/263301/1562910991695-d2fdffdd-9334-40a5-a902-9fbd558ccdc3.webp#align=left&display=inline&height=391&originHeight=391&originWidth=686&size=0&status=done&width=686)<br />5.项目的配置完成现在需要生成一些配置文件<br />a. 进入原生项目的flutter模块目录中执行`flutter packages get`命令<br />b. 回到原生项目根目录执行`pod install`
```
➜  cd flutter-module-demo
➜  flutter-module-demo git:(master) flutter packages get
Running "flutter packages get" in flutter-module-demo...            0.4s
➜  flutter-module-demo git:(master) cd ..
➜  FlutterNativeiOS git:(master) ✗ pod install
Analyzing dependencies
Fetching podspec for `Flutter` from `./flutter-module-demo/.ios/Flutter/engine`
Fetching podspec for `FlutterPluginRegistrant` from `./flutter-module-demo/.ios/Flutter/FlutterPluginRegistrant`
Downloading dependencies
Using AFNetworking (2.6.3)
Installing Flutter (1.0.0)
Installing FlutterPluginRegistrant (0.0.1)
Generating Pods project
Integrating client project
Sending stats
Pod installation complete! There are 3 dependencies from the Podfile and 3 total pods installed.
复制代码
```
到此为止我们的原生项目就已经集成好了flutter项目了。<br />5.在原生项目中使用flutter，下面以swift项目为例<br />修改AppDelegate.swift:注意AppDelegate是集成自FlutterAppDelegate
```
import UIKit
import Flutter
import FlutterPluginRegistrant // Only if you have Flutter Plugins.
@UIApplicationMain
class AppDelegate: FlutterAppDelegate {
  var flutterEngine : FlutterEngine?;
  // Only if you have Flutter plugins.
  override func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    self.flutterEngine = FlutterEngine(name: "io.flutter", project: nil);
    self.flutterEngine?.run(withEntrypoint: nil);
    GeneratedPluginRegistrant.register(with: self.flutterEngine);
    return super.application(application, didFinishLaunchingWithOptions: launchOptions);
  }
}
复制代码
```
修改Controller代码
```
import UIKit
import Flutter
class ViewController: UIViewController {
  override func viewDidLoad() {
    super.viewDidLoad()
    let button = UIButton(type:UIButtonType.custom)
	...
    self.view.addSubview(button)
  }
  @objc func handleButtonAction() {
    let flutterEngine = (UIApplication.shared.delegate as? AppDelegate)?.flutterEngine;
    let flutterViewController = FlutterViewController(engine: flutterEngine, nibName: nil, bundle: nil)!;
    self.present(flutterViewController, animated: true, completion: nil)
  }
复制代码
```

6. RUN….
<a name="YIPfW"></a>
### 3.iOS项目集成过程梳理
整个的集成过程其实总得来说是如下三个步骤：<br />1.将flutter项目放入原生项目的文件夹下<br />2.在podfile中添加`podhelper.rb`配置<br />3.在Xcode的build phases添加`"$FLUTTER_ROOT/packages/flutter_tools/bin/xcode_backend.sh"`iOS编译脚本。<br />其中podhelper.rb文件位于我们flutter模块项目的`.ios/Flutter/podhelper.rb`下，大家查看它的源码可以发现，它有下面几个作用：<br />1.把Flutter（flutterEngine）和FlutterPluginRegistrant两个库用pod给原生项目导入进入<br />2.如果flutter项目有用到flutter plugin插件，把插件用pod导入<br />3.导入`Generated.xcconfig`的相关配置信息，在`podhelper.rb`同级别的目录下还有一个`Generated.xcconfig`文件，这个文件在使用`flutter create xx、flutter run xxx、flutter packages get`命令的时候如果该文件不存在则会生成这个文件。这个文件内容如下：
```
// This is a generated file; do not edit or check into version control.
FLUTTER_ROOT=/Users/zhiqiangdeng/.flutter_wrapper/1.2.2-pre.43
FLUTTER_APPLICATION_PATH=/Users/zhiqiangdeng/Documents/ProjectSource/XcodeProject/lianhua-order-iOS/order-check-module-flutter
FLUTTER_TARGET=lib/main.dart
FLUTTER_BUILD_DIR=build
SYMROOT=${SOURCE_ROOT}/../build/ios
FLUTTER_BUILD_NAME=1.0.0
FLUTTER_BUILD_NUMBER=1
复制代码
```
他记录了当前flutter sdk的目录位置，以及版本号，还有项目模块的目录位置。这个文件的内容在执行`pod install`的时候会被写入到xcode build setting中，在执行完pod install之后，可以在原生项目根目录使用`xcodebuild -showBuildSettings|grep flutter` 查看相关的信息。<br />![](https://cdn.nlark.com/yuque/0/2019/webp/263301/1562910991728-2e90df24-17ee-4ae2-8120-572f3d2abdc2.webp#align=left&display=inline&height=162&originHeight=162&originWidth=798&size=0&status=done&width=798)<br />最后一步就是运行程序，运行程序的时候在Build phase添加了`xcode_backend.sh`该脚本会使用到上面pod install给xcode build setting设置的那些环境变量，然后找到项目目录生成AppFramework。
<a name="x9bZz"></a>
### 4.给原生Android项目集成Flutter
Android的文章很多，这里不再详细描述了<br />1.在原生Android项目中添加子模块，将上面创建的flutter module项目拉取到原生安卓项目中
```
git submodule add {你的flutter module的仓库地址}
git submodule update
复制代码
```
<a name="EYKda"></a>
#### 2.在根目录的`settings.gradle`中添加如下配置
```
setBinding(new Binding([gradle: this]))                                 
evaluate(new File(                                                                 
  '{xxxxx你的flutter module目录}/.android/include_flutter.groovy'                    
))      
复制代码
```
<a name="kTTF4"></a>
#### 3.在原生项目的app目录下的build.gradle文件中添加Flutter库的依赖
```
dependencies {
  implementation project(':flutter')
}
复制代码
```
<a name="9OGh9"></a>
#### 4.在原生代码中集成flutter跳转到flutter页面
我使用了一个新的Activity进行跳转。具体可以参看源码
```
Button open = findViewById(R.id.openBtn);
open.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
        Intent intent = new Intent();
        intent.setClass(MainActivity.this, MyFlutterActivity.class);
        startActivity(intent);
    }
});
复制代码
```
```
public class MyFlutterActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_flutter);
        final FlutterView flutterView = Flutter.createView(
                this,
                getLifecycle(),
                "route1"
        );
        final FrameLayout layout = findViewById(R.id.flutter_container);
        layout.addView(flutterView);
        final FlutterView.FirstFrameListener[] listeners = new FlutterView.FirstFrameListener[1];
        listeners[0] = new FlutterView.FirstFrameListener() {
            @Override
            public void onFirstFrame() {
                layout.setVisibility(View.VISIBLE);
            }
        };
        flutterView.addFirstFrameListener(listeners[0]);
    }
}
复制代码
```
<a name="cU1Jt"></a>
### 5.团队中其他同事协同开发

1. 拉取项目源码`git clone xxxxx{项目地址}`
1. 初始化项目中的子模块`git submodule init && git submodule update`
1. 执行`flutter packages get` (有时候可能出现无法运行可以进入.ios和.android中分别执行pod install 和 gradle assembleDebug,或者flutter build ios,flutter build apk等命令构建一次)
1. Run...

**Android从原生跳到Flutter模块的黑屏问题**，在网上看到很多说设置透明主题的但是没有用，后来看到一种先隐藏显示，等待渲染好第一帧后才显示flutter页面的方法。这里要注意一点要在布局中先把flutter的Container布局设置为InVisible状态，不要使用Gone，用gone的话是不显示也不渲染，用InVisible不显示但是会渲染界面占位置，等待渲染完成后再设置为Visible即可。
<a name="IdS8P"></a>
### 6.flutter的版本管理
在我们的开发过程中遇到了一个问题，就是各个开发者使用的flutter sdk版本不一致，导致一些库无法运行，在网上也遇到有相同问题的人，提出了模仿gradle wrapper来做一个flutter_wrapper的思路。于是我根据自己的需要写了一个flutter_wrapper的小工具。它的主要作用是统一开发人员的本地flutter环境。<br />**使用说明**

1. 在你的项目根目录中执行命令下载脚本<br />`curl -O https://raw.githubusercontent.com/zakiso/flutterw/master/flutterw && chmod 755 flutterw`
1. 下载好脚本后在根目录中使用<br />`./flutterw init`<br />该命令会收集你当前系统中的flutter版本，并将相关信息写入`flutter_wrapper.properties`文件中，团队中所有成员都会以该版本号做为该项目的标准版本
1. 将flutterw文件和flutter_wrapper.properties文件添加到git中提交到仓库里
1. 其他成员拉取代码后在项目中使用`flutter`命令的地方使用`./flutterw`代替，如果使用ide请选择home目录下对应版本的sdk包

**flutterw做了什么？**

1. 使用flutterw的时候会获取当前目录下的flutter_wrapper.properties文件中的版本号
1. 去用户的`${HOME}/flutter_wrapper/{版本号}/` 目录下查找是否有该版本sdk
1. 如果没有该版本sdk会下载下来，然后使用该目录下的sdk执行命令

**注意事项**<br />如果flutter版本是preview的版本是直接使用master的最新代码来管理的。大家可以查看源码很简单，根据自己的需要定制。<br />项目demo我已经传到github中：有遇到问题的可以参考项目源码

- 原生Android集成Flutter项目：
  - [github.com/zakiso/flut…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fzakiso%2Fflutter-native-android.git)
- 原生iOS集成Flutter项目：
  - [github.com/zakiso/flut…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fzakiso%2Fflutter-native-ios.git)
- Flutter模块项目：
  - [github.com/zakiso/flut…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fzakiso%2Fflutter-module-demo.git)
- Flutter_Wrapper:
  - [github.com/zakiso/flut…](https://link.juejin.im/?target=https%3A%2F%2Fgithub.com%2Fzakiso%2Fflutterw.git)
<a name="5s3hx"></a>
### 最后：
![](https://cdn.nlark.com/yuque/0/2019/webp/263301/1562910991747-a15693d7-ed99-48c4-9016-7bb7f67cb544.webp#align=left&display=inline&height=447&originHeight=447&originWidth=1280&size=0&status=done&width=1280) 我们整个项目都是使用git进行管理的，虽然每个开发者都需要安装flutter环境，但是对于小团队来说成本并不高，加上flutter_wrapper也保证了版本的一致性。iOS开发者可以在原来的iOS项目中开发flutter的项目，Android开发者可以在原android项目中开发flutter，flutter开发者也可以自己单独开发flutter项目，这种方式其实对于开发者来说也是很方便的。<br />**Everything 用flutter开发的一款App，把记账本日记本，行程，待办等等都装进一个App里**
<a name="KGpXy"></a>
#### [everythings.app/](https://link.juejin.im/?target=https%3A%2F%2Feverythings.app%2F)
![](https://cdn.nlark.com/yuque/0/2019/webp/263301/1562910991739-22406358-1a7e-4a72-8a8c-4455fe12f4d4.webp#align=left&display=inline&height=635&originHeight=635&originWidth=1280&size=0&status=done&width=1280)<br />转自：[https://juejin.im/post/5c6eba82518825626b76f0eb](https://juejin.im/post/5c6eba82518825626b76f0eb)

