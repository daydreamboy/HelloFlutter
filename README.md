# HelloFlutter

[TOC]

## 1、环境搭建

### （1）平台支持

| 平台    | 系统版本                                      |
| ------- | --------------------------------------------- |
| iOS     | 8.0+ (Flutter supports iOS 8.0 and later[^2]) |
| Android |                                               |







### （2）源码安装

```shell
$ git clone https://github.com/flutter/flutter.git -b stable --depth 1
```

注意

> 没有安装DartSDK，执行flutter命令，会触发下载DartSDK



### （2）SDK安装

下载zip包，解压到本地，包比较大。推荐使用源码安装。



### （3）配置flutter命令行工具

```shell
export PATH="$PATH:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"
```



选择编辑器

* Android Studio/IntelliJ
* Visual Studio Code
* Emacs

这里选择Visual Studio Code（后面简称VSCode），在VSCode的Extensions中搜索flutter并安装。这个flutter插件提供dart文件的语法支持和以及相关代码补全提示。



## 2、HelloWorld工程（iOS）

### （1）创建工程

使用`flutter create`命令创建工程，实际该工程也是pub包的工程。

```shell
$ flutter create hello_world
...
In order to run your application, type:

  $ cd hello_world
  $ flutter run

Your application code is in hello_world/lib/main.dart.
```

说明

> pub包的包名有一定规则[^1]，必须全部小写字母，而且以字母开头，允许的字符为`[a-z0-9_]`，不能和关键词冲突。



### （2）运行工程

​       cd到工程的根目录，执行`flutter run`。该命令会使用ios/Runner.xcworkspace工程，作为构建app的工程，在用命令行方式编译app以及安装app到iOS模拟器或真机上。

​      执行`flutter run`命令，示例如下

```shell
$ flutter run
Launching lib/main.dart on iPhone 11 in debug mode...
 
Running Xcode build...                                                  
                                                   
 └─Compiling, linking and signing...                         9.5s
Xcode build done.                                           25.7s
Syncing files to device iPhone 11...                               185ms

Flutter run key commands.
r Hot reload. 🔥🔥🔥
R Hot restart.
h Repeat this help message.
d Detach (terminate "flutter run" but leave application running).
c Clear the screen
q Quit (terminate the application on the device).
An Observatory debugger and profiler on iPhone 11 is available at: http://127.0.0.1:64260/GD6qwkWpRLU=/
```



注意

> 执行`flutter run`，之前保持iOS模拟器是运行的。



### （3）编写Dart代码

flutter的编程语言是Dart，类似JavaScript语言。

找到工程下的lib/main.dart文件，换成如下代码

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Welcome to Flutter'),
        ),
        body: Center(
          child: Text('Hello World'),
        ),
      ),
    );
  }
}
```

如果app还在运行，在Terminal中，输入`r`，会触发Flutter热更新，app界面会重新刷新。

以上是一个简单HelloWorld的Flutter工程。



## 3、Flutter添加到现有工程中



（1）Embed with CocoaPods and the Flutter SDK

文件结构

```shell
$ tree . -L 2
.
├── HelloFlutter
│   ├── HelloFlutter
│   ├── HelloFlutter.xcodeproj
│   ├── HelloFlutter.xcworkspace
│   ├── Podfile
│   ├── Podfile.lock
│   └── Pods
└── my_flutter
    ├── README.md
    ├── lib
    ├── my_flutter.iml
    ├── my_flutter_android.iml
    ├── pubspec.lock
    ├── pubspec.yaml
    └── test

8 directories, 7 files
```



Podfile

```ruby
flutter_application_path = '../my_flutter'
load File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')

platform :ios, '9.0'

target 'HelloFlutter' do
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!
  install_all_flutter_pods(flutter_application_path)
end
```





显示Flutter view controller

Show a FlutterViewController with your FlutterEngine

https://flutter.dev/docs/development/add-to-app/ios/add-flutter-screen#show-a-flutterviewcontroller-with-your-flutterengine



调试

```shell
$ flutter attach -d <device id>
```











## 附录

### 1、flutter命令

#### （1）run

| 选项          |                                |
| ------------- | ------------------------------ |
| -d <deviceId> | 指定运行在某个已经启动的设备上 |
| -d all        | 运行在所有已经启动的设备上     |









## Reference

[^1]:https://dart.dev/tools/pub/pubspec#name

[^2]:https://flutter.dev/docs/development/add-to-app/ios/project-setup#system-requirements



