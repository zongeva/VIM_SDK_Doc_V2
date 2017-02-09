##文件
```java
FileService fileService = ClientManager.getDefault().getFileService();
```
###注册/取消 p2p监听
* @param listener 

```java
fileService.observeP2pListener(P2pListener listener)
```
###上传头像
* path - 头像本地路径
* callBack - 大图地址json,缩略图地址json

```java
fileService.uploadAvatar(java.lang.String path,ResultCallBack<String,String,Void> callBack);
```
###上传文件
* fileProperty 
* callBack      目标Id _3服务器返回的json
* stateCallBack （额外的请求信息，进度信息，描述信息）
* @return 每个文件对应的唯一localID

```java
fileService.uploadFile(final UploadFileProperty fileProperty, ResultCallBack<Long, String, Void> callBack,
                           final ResultCallBack<Integer, Integer, String> stateCallBack)
```
###下载文件
* fileProperty 
* callBack      本地路径 发送者ID
* stateCallBack （额外的请求信息，进度信息，描述信息）
* @return 每个文件对应的唯一localID

```java
fileService.downloadFile(final DownloadFileProperty fileProperty, ResultCallBack<String, Long, Void> callBack,final ResultCallBack<Integer, Integer, String> stateCallBack)
```
                
###下载外部文件
* localPath     文件本地保存路径
* url           远程路径完整的URL路径
* isFullUrl     是否是全路径 
* callBack      目标Id _3服务器返回的json
* stateCallBack （额外的请求信息，进度信息，描述信息）
* @return 每个文件对应的唯一localID

```java
downloadExternalFile(String localPath, String url, boolean isFullUrl, ResultCallBack callBack,
                                     ResultCallBack<Integer, Integer, String> stateCallBack)
```
                

###上传照片
* @param targetID   人或群的id
* @param thumbPath  缩略图
* @param srcPath    原图
* @param encryptKey 解密密码
* @param callBack   目标ID,原图JSON,缩略图JSON

```java
fileService.uploadImage(long targetID, long localID, String thumbPath, String srcPath, String encryptKey,
                            ResultCallBack<Long, String, String> callBack,
                            ResultCallBack<Integer, Integer, String> stateCallBack)
```
                

###下载图片
* @param targetID 人或群的id
* @param url      图片url
* @param callBack 图片名,对方ID
* @param stateCallBack （额外的请求信息，进度信息，描述信息）
```java
fileService.downloadImage(long targetID, String url, ResultCallBack<String, Long, Void> callBack, ResultCallBack<Integer, Integer, String> stateCallBack) 
```
                

###解密文件，默认解密到cache目录下
* @param encryptKey 秘钥
* @param srcPath 源路径
* @return 解密后的路径

```java
fileService.decryptFile(String encryptKey, String srcPath)
```
                

###解密文件
* @param encryptKey 解密密码
* @param srcPath    原图路径
* @param destPath   解密后图片路径
* @return 成功或失败

```java
fileService.decryptFile(String encryptKey, String srcPath, String destPath)
```
                

###获取文件列表
* @param targetID 查询对象id
* @param fileID   起始文件id
* @param count    数量
* @param flag     偏移标志 0为向上,1为向下
* @param callBack 文件信息集合

```java
fileService.getFileList(long targetID, long fileID, int count, int flag, ResultCallBack<List<FileInfo>, Void, Void> callBack)
```
                

###通过文件消息ID得到文件详细信息
* @param fileMsgIds 文件消息ID集合
* @return 文件消息ID和文件详细信息键值对

```java
fileService.getFilesInfo(List<Long> fileMsgIds)
```
                

###判断是否有文件在传输
* @param localID 文件的local, 0代表判断是否存在任意文件在上传状态
* @return 是否有文件在传输
```java
fileService.isTransmitting(int localID)
```
                
###取消文件上传或下载
* @param localID 文件的localID
* @param type    1.上传 2.下载 3.外部下载
```java
fileService.cancelTransfer(long localID, int type, ResultCallBack callBack)
```
###取消所有文件传输
```java
fileService.cancelAllTransfer(ResultCallBack callBack)
```
###获取局域网可以P2P通讯的用户
```java
* @return p2p用户列表
fileService.getP2pUsers()
```
###取消正在进行的传输或拒绝尚未开始的p2p传输
* 取消正在进行的传输或拒绝尚未开始的p2p传输
```java
fileService.p2pTransferCancel(long taskID)
```

