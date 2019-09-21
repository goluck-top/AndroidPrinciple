## Android打包相关原理

从Android Studio 点击'run'到生成apk之间的过程。今天我们讲解下这个过程中，用到的构建工具和构建的过程。

### apk解压后的目录如下：
* AndroidManifest.xml    程序全局配置文件
* classes.dex            Dalvik字节码
* resources.arsc         资源索引表, 解压缩resources.ap_就能看到
* res\                   该目录存放资源文件(图片，文本，xml布局)
* assets\                该目录可以存放一些配置文件
* src\                   java源码文件
* libs\                  存放应用程序所依赖的库
* gen\                   编译器根据资源文件生成的java文件
* bin\                   由编译器生成的apk文件和各种依赖的资源
* META-INF\              该目录下存放的是签名信息


### 下面是构建步骤：

* AAPT（Android Asset Packaging Tool）工具，Android资源打包工具。会打包资源文件（res文件夹下的文件），并生成R.java和resources.arsc文件。
* AIDL工具会将所有的.aidl文件编译成.java文件。
* JAVAC工具将R.java、AIDL接口生成的java文件、应用代码java文件编译成.class文件。
* dx脚本将很多.class文件转换打包成一个.dex文件。
* apkbuilder脚本将资源文件和.dex文件生成未签名的.apk文件。
* jarsigner对apk进行签名。

这些构建中使用的工具或者脚本，在SDK的build-tools或者tools下可以找到

### Google官方提供的构建流程图

对应着上面的构建步骤和apk解压目录看应该很清晰了

![](https://img-blog.csdn.net/20180625083138660?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2NhaWJhb3ppeGlhb2JhaQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)