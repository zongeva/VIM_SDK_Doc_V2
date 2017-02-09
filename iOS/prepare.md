##开发准备

###1.首先从信源豆豆官网下载 IOS SDK(支持iOS7.0以上系统版本)然后手动添加到你的项目中。

###2.添加依赖库

* AudioToolbox.framework--音频文件解析工具包
* AVFoundation.framework--视频流处理工具包
* libstdc++.tbd--用于支持c++标准库链接
* libz.tbd--支持压缩的动态链接库
* 注:在 XCode7 以上版本中后缀为 tbd,XCode6 及以下均为 dylib。

###3.工程引入头文件<SDKClient/SDKClient.h>,建议引入到工程pch文件中。

* 注:由于SDK库是静态库文件,需要在Build Settings->Other Linker Flags添加-ObjC
* 注:如果您的工程需要使用 C++ ,在 Build Setting -> Apple LLVM 7.0 - Language - C++ -> C++ Standard Library 里，设置值为 libstdc++ (GNU C++ standard library)。

###4.SDK库应用证书引入
在官网[(http://www.linkdood.cn/server-linkdood/reg)](http://www.linkdood.cn/server-linkdood/reg)上申请证书,
将审核通过的证书下载好并加入工程,程序启动时通过SDK接口registerApp注册应用证书。


```

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    //1.注册应用证书
    NSString *path = [[LDClient sharedInstance] registerApp:[[NSBundle mainBundle] pathForResource:@"linkdood" ofType:@"crt"] onCachePath:@"Linkdood"];
    if (path == nil) {
        //证书无效或者失效
        return false;
    }
    //path为SDK用户自定义的缓存文件根目录
    //[[NSBundle mainBundle] pathForResource:@"linkdood" ofType:@"crt"] 为证书的路径
    return YES;
}
```


