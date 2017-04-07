##开发准备
首先从北信源Linkdood官网下载 Android SDK。开发者可以根据实际需求，配置类库。

###类库配置
SDK 包的libs文件夹中，包含了北信源Linkdood SDK的 jar 文件，各 jni 库文件夹以及 SDK 依赖的第三方库，列表如下：

```java
	libs
	├── armeabi
	│   ├── libjniVimServicePresets.so 
	│   ├── liblddplugin.so	
	├── armeabi-v7a
	│   ├── libjniVimServicePresets.so
	│   ├── liblddplugin.so
	└── vimsdk-version.jar
	└── javacpp.jar
```

以上文件列表中，imsdk-version.jar (版本号可能会不同)为Linkdood SDK，子目录中的文件是 SDK 所依赖的各个 CPU 架构的 so 库。

###证书下载
在官网上申请生成证书，将下载好的证书命名为`vimsdk.crt,`保存在你项目 `app/src/main/assets` 下(必须)

### 权限与组件
####在 AndroidManifest.xml 中加入以下配置:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WAKE_LOCK"/>
// ... 你的其他权限
<application>
	<service android:name="com.vrv.imsdk.service.ApNotifyService"/>
	<receiver android:name="com.vrv.imsdk.receiver.ApNotifyReceiver">
		<intent-filter>
		  <action 
			  android:name="com.vrv.imsdk.receiver.ApNotifyReceiver"/>
		  </intent-filter>
	 </receiver>
	<meta-data android:name="com.vrv.imsdk" android:value="0l"/>
</application>
```

### 初始化SDK
####添加 SDK 初始化方法在程序中的Application 中添加
```java
    @Override
    public void onCreate() {
        super.onCreate();
        // ... your codes
	//dirName本地保存数据目录
        boolean init = VIMClient.init(this,dirName);
        if( !init){
	        Log.e("TAG","SDK初始化失败,不能正常使用");
        }
	// ... your codes
    }
```

###请求方法说明
SDK的请求方法都是采用异步方法，对应方法中都有ResultCallback参数 。
     - onSuccess 请求成功，成功后返回的数据有多种形式，具体根据接口判断 。
     - onError 请求失败，errCode具体见 'ResponseCode'

```java
ResultCallBack<T result> callBack = new ResultCallBack() {
     @Override
     public void onSuccess(T result) {
                
     }     @Override
     public void onError(int errCode, String errMsg, ResponseResult data) {
                
     }
};
```

###缓存列表数据更改在每个Service中通过OnChangeListener通知客户端
SDK中的缓存列表数据通过在对应对象中设置监听来更新数据（部分对象中可能还会有别的监听需要设置），以最近联系人为例：

```java
SDKClient.instance.getChatService.setListener(new ServiceModel.OnchangeListener(){
        @Override
        public void notifyDataChange(){
            //Todo 重新获取列表刷新界面
        }
        @Override
        public void notifyItemChange(int position){
            //Todo 更新列表中这个位置的数据
        }
})；
```
