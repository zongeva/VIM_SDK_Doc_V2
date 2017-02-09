##最近联系人/消息
```java
ChatService chatService = ClientManager.getDefault().getChatService();
```
###注册消息接收监听
* @param targetID 用来接收当前targetID的聊天消息
* @param listener
```java
chatService.observeReceiveListener(long targetID, ReceiveMsgListener listener)   
```  
###设置消息进度监听
* @param listener
```java
chatService.observeProgressListener(ProgressListener listener)   
```  
###设置聊天背景更改监听
* @param listener
```java
chatService.observeBackgroundListener(BackgroundChangeListener listener)
```  
###获取会话列表
```java
List<Chat> list=chatService.getList()
```  
###移除会话
* @param targetID 会话对应的ID，群或者人 (0为删除全部联系人)
```java
chatService.remove(long targetID, ResultCallBack callBack)
```  
###发送消息
* @param msg  消息 （E extends ChatMsg）
```java
chatService.sendMsg(final E msg, ResultCallBack callBack) 
```  
###转发消息
* @param targetID
* @param msg （E extends ChatMsg）
```java
chatService.transferMsg(long targetID, E msg, ResultCallBack callBack)
```  
###发送隐藏消息(不存储)
* @param msg （E extends ChatMsg）
```java
chatService.sendHiddenMsg(final E msg, final ResultCallBack callBack)
```  
###下载文件
* @param chatMsg
* @param callBack 本地路径 发送者ID
* @param stateCallBack （额外的请求信息，进度信息，描述信息）
* @return 每个文件对应的唯一localID
```java
chatService.downloadFile(final ChatMsg chatMsg, ResultCallBack<String, Long, Void> callBack,
                             final ResultCallBack<Integer, Integer, String> stateCallBack)
```  
###下载图片
* @param msgImg
* @param originImage   是否为缩略图
* @param callBack 本地路径 发送者ID
* @param stateCallBack  （额外的请求信息，进度信息，描述信息）
* @return
```java
chatService.downloadImage(final MsgImg msgImg, boolean originImage, ResultCallBack<String, Long, Void> callBack,
                              final ResultCallBack<Integer, Integer, String> stateCallBack)  
```  
###删除所有消息
```java
chatService.deleteAllMsg(boolean clearChatList, ResultCallBack callBack)
```  
###通过msgID删除消息
* @param targetID 会话对应的ID，群或者人
* @param msgIDs   要删除的消息ID集合 msgIDs为空，清空对应targetID的所有消息
```java
chatService.deleteMsgByID(long targetID, List<Long> msgIDs, ResultCallBack callBack)
```  
###删除时间段消息
* @param targetID  会话对应的ID，群或者人 targetID为0，则针对所有用户
* @param beginTime 起始时间
* @param endTime   结束时间
```java
chatService.deleteMsgByTime(long targetID, long beginTime, long endTime, ResultCallBack callBack) 
```  
###设置消息已读
* @param targetID 会话对应的ID，群或者人
* @param msgID    消息ID
```java
chatService.setMsgRead(long targetID, long msgID)
```  
###设置消息未读
* @param targetID 会话对应ID
```java
chatService.setMsgUnread(long targetID, ResultCallBack callBack) 
```  
###获取消息
* @param targetID 会话对应的ID，群或者人
* @param msgID    查询消息的起始ID，将从该消息的下一条消息开始查询
* @param count    查询消息总数
* @param flag     上一页还是下一页 向上偏移 0；向下偏移 1
* @param callBack 会话ID，消息集合
```java
chatService.getMessages(long targetID, long msgID, int count, int flag, ResultCallBack<Long, List<ChatMsg>, Void> callBack)
```  
###最近联系人置顶
* @param targetID 置顶的目标ID
* @param isTop    是否置顶
```java
chatService.top(long targetID, boolean isTop, ResultCallBack callBack)
```  
###获取图片消息
* @param targetID 个人或群ID
* @param callBack 消息集合
```java
chatService.getImgMsg(long targetID, ResultCallBack<List<ChatMsg>, Void, Void> callBack)
```  
###获取URL的详细信息
* @param url      网址
* @param callBack 接收结果回调 [网址,标题,图片地址,摘要]
```java
chatService.getUrlInfo(String url, ResultCallBack<String[], Void, Void> callBack)   
```  
###设置私信密码
* @param targetID 目标ID，个人或群
* @param password 密码
```java
chatService.setPrivateKey(long targetID, String password, ResultCallBack callBack)  
```  
###通过消息ID解密消息
* @param msgIds   要解密的消息ID集合
* @param callBack 传入接收结果回调 _1 错误信息 _2 解密消息的targetId _3已解密的消息
* @param targetId 目标ID，个人或群
```java
chatService.decryptMsg(long targetId, List<Long> msgIds, ResultCallBack<Long, List<ChatMsg>, Void> callBack)
```  
###更新消息（ChatMsg 为完整数据+被修改的数据）
* @param targetID 用来接收当前targetID的聊天消息
* @param listener
```java
chatService.updateMsg(List<ChatMsg> msgs, ResultCallBack callBack)  
```  
###通过目标ID查询最近会话信息
* * @return Chat 最近会话信息
```java
chatService.findItemByID(long targetID)  
```  
###通过目标ID查询最近会话位置
* @return 最近会话的位置
```java
chatService.indexByID(long targetID)  
```  
