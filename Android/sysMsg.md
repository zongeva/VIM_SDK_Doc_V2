## 系统消息 
```java
SysMsgService sysMsgService = ClientManager.getDefault().getSysMsgService();
```
### 获取系统消息列表

传入参数：（时间，偏移量，ResultCallBack<ArrayList<SystemMsg>>)
回调中返回系统消息列表

```java
sysMsgService.getList(long time, int offSet, ResultCallBack<ArrayList<SystemMsg>> callBack);
```
### 请求处理

operType的取值： 0同意，1拒绝

#### 响应加好友的请求

传入的参数：（请求者的用户ID，请求消息的msgID，对此请求的操作，好友备注，附带的拒绝信息，ResultCallBack）

```
sysMsgService.respToAddBuddy(long userId, long msgID, int operType, String remark, String refuseReason, ResultCallBack callBack);
```

#### 响应进群的请求

传入的参数：（要进入的群ID，请求消息的msgID，对此请求的操作，附带的拒绝信息，RequestCallBack）

operType的取值：如果是回应被邀请进群消息，只有同意和拒绝选项

```
sysMsgService.respToEnterGroup(long groupId, long msgID, int operType, String refuseReason, RequestCallBack callBack);
```

### 设置消息为已读

```
sysMsgService.setMsgRead(List<SystemMsg> sysMsgs);
```

### 获取系统消息

传入的参数：（传入响应消息类型，传入数量，传入消息id，传入偏移标志，RequestCallBack<List<SystemMsg>, Void, Void>）

传入响应消息类型： 0 全部 1 加好友请求 2 加好友响应 3 加群请求 4 加群
传入偏移标志： 0 向上偏移 1 向下偏移

```
sysMsgService,getSysMessages(int type, int count, long msgID, int flag, RequestCallBack<List<SystemMsg>, Void, Void> callBack);
```

### 通过类型删除系统消息

type的取值： 1 好友请求验证框已读|2 好友请求返回框已读| 3 设置群验证请求消息已读|4 设置群验证响应消息已读

```
sysMsgService.deleteMessageByType(int type, List<Long> msgIDs, RequestCallBack callBack);
```

### 删除全部系统消息

```
sysMsgService.deleteAllMessage(RequestCallBack callBack);
```

### 监听

注册/取消接收系统消息监听

```
sysMsgService.observeReceiveListener(ReceiveSysMsgListener listener);
```