##插件扩展
```java
ExtService extService = ClientManager.getDefault().getExtService()
```
###企业组织 
####设置企业成员信息更新监听
```java
extService.observeUpdateListener(EntUpdateStatusListener listener);
```
####获取组织信息
* @param orgID    组织Id
* @param callBack 组织信息;
```java
extService.getOrgInfo(long orgID, ResultCallBack<OrganizationInfo, Void, Void> callBack);
```
####获取组织集合和企业用户信息
* @param orgId    组织ID  传 0 表示获取根组织
* @param callBack 组织集合, 企业用户信息;
```java
extService.getVisibleOrgUsers(long orgId, ResultCallBack<byte[], List<OrganizationInfo>, List<EnterpriseUserInfo>> callBack);
```
####根据条件查询企业用户列表
* @param enterpriseUserQueryInfo 查询信息
* @param callBack  total 总数, totalPage 总页数, 用户信息集合;
```java
extService.queryEnterpriseUserList(EnterpriseUserQueryInfo enterpriseUserQueryInfo, ResultCallBack<Long, Long, Map<String, List<EnterpriseUserInfo>>> callBack);
```
####获取企业所有用户信息
* @param orgIds   需要获取的用户集合
* @param callBack 传入接收结果回调 _1 错误号;_2 返回企业用户信息;
```java
extService.queryEntUserAll(List<Long> orgIds, ResultCallBack<List<EnterpriseUserInfo>, Void, Void> callBack);
```
####通过userId获取企业用户信息
* @param userId   userID
* @param callBack 企业用户信息;
```java
extService.queryEntUserOneById(long userId, ResultCallBack<List<EnterpriseUserInfo>, Void, Void> callBack);
```
####通过userName获取企业用户信息
* @param userName 用户名
* @param callBack 企业用户信息;
```java
extService.queryEntUserOneByName(String userName, ResultCallBack<List<EnterpriseUserInfo>, Void, Void> callBack);
```
###记事本
####添加记事本
* @param noteInfo 记事本信息
```java
extService.addNote(NoteInfo noteInfo, ResultCallBack callBack);
```
####获取记事本
* @param beginID    起始消息ID offsetFlag = 0 msgBeginID = 0时，代表从最大的消息Id进行查找
* @param offset     查询的数量
* @param offsetFlag 偏移标志；0.消息Id由大到小偏移 1.消息Id由小到大偏移 offsetFlag.
* @param callBack   记事本集合
```java
extService.getNote(long beginID, int offset, byte offsetFlag, ResultCallBack<List<NoteInfo>, Void, Void> callBack);
```
####删除记事本
* @param noteId   需删除noteID
```java
extService.deleteNote(List<Long> noteId, ResultCallBack callBack);
```
####修改记事本
* @param noteInfo 新的note信息
```java
extService.editNote(NoteInfo noteInfo, ResultCallBack callBack);
```
####置顶记事本
* @param noteId   要置顶的note id
* @param top      是否置顶
```java
extService.topNote(long noteId, boolean top, ResultCallBack callBack);
```
####搜索记事本
* @param key      搜索关键字
* @param callBack 搜索的记事本集合
```java
extService.searchNote(String key, ResultCallBack<List<NoteInfo>, Void, Void> callBack);
```
####归档记事本
* @param noteId    要归档的note id
* @param isArchive 是否归档
```java
extService.archiveNote(long noteId, byte isArchive, ResultCallBack callBack);
```
###房间
####创建房间
* @param roomName 房间名
* @param ids      成员集合
* @param flag     是否置顶
* @param url      头像url
* @param callBack 房间ID
```java
extService.createRoom(String roomName, List<Long> ids,byte flag, String url, ResultCallBack<Integer, Void, Void> callBack)
```
####删除房间
* @param roomID   房间ID
```java
extService.deleteRoom(long roomID, ResultCallBack callBack)
```
####修改房间图标
* @param roomId   要修改的roomID
* @param icoURL   头像的URL
```java
extService.changRoomIcon(long roomId, String icoURL, ResultCallBack callBack);
```
####修改房间名称
* @param roomID   要修改的roomID
* @param newName  新名称
```java
extService.changRoomName(long roomID, String newName, ResultCallBack callBack)
```
####房间置顶
* @param roomID   房间ID
* @param top      是否置顶

```java
extService.topRoom(long roomID, boolean top, ResultCallBack callBack)
```
####获取所有房间信息
* @param callBack 房间信息集合
```java
extService.getAllRoom(ResultCallBack<List<Room>, Void, Void> callBack)
```
####获取房间信息
* @param roomID   房间ID
* @param callBack 获取的房间信息;

```java
extService.getRoom(long roomID, ResultCallBack<List<Room>, Void, Void> callBack)
```

####房间增加人员
* @param roomId   房间ID
* @param list     加入的成员

```java
extService.addRoomMember(long roomId, List<Long> list, ResultCallBack callBack)
```

####房间删除人员
* @param roomId   房间ID
* @param list     删除的成员
```java
extService.delRoomMember(long roomId, List<Long> list, ResultCallBack callBack)
```
###获取消息
####获取与目标的聊天消息数目
* @param targetId targetId
* @param callBack 消息数目;
```java
extService.getMsgCountByTargetID(long targetId, ResultCallBack<Integer, Void, Void> callBack)
```
####获取@自己最多的topN群
* @param topN     获取前topN会话的群组
* @param callBack targetID集合,消息数目;
```java
extService.getMsgTopNAtGroup(int topN, ResultCallBack<List<Long>, List<Integer>, Void> callBack)
```
####获取前topN群组的消息
* @param topN     获取前topN群组的消息
* @param callBack targetID集合,消息数目;
```java
extService.getMsgTopNGroup(int topN, ResultCallBack<List<Long>, List<Integer>, Void> callBack)
```
####获取前topN会话的消息
* @param topN     获取前topN会话的消息
* @param callBack targetID集合, 消息数目;
```java
extService.getMsgTopNSession(int topN, ResultCallBack<List<Long>, List<Integer>, Void> callBack)
```
##任务
####发送任务消息
* @param msg      传入组织id
* @param callBack msgID, sendTime;
```java
extService.sendTaskMsg(ChatMsg msg, ResultCallBack<Long, Long, Void> callBack)
```
###获取任务回复消息
     * @param taskID   要获取的的任务id
     * @param callBack 回复消息;
```java
extService.getReceiveMsg(long taskID, ResultCallBack<List<ChatMsg>, Void, Void> callBack)
```
####获取接收的任务
* @param callBack 任务集;
```java
extService.getReceiveTask(ResultCallBack<List<Task>, Void, Void> callBack)
```
####恢复任务
* @param taskId   需要恢复的TaskID
```java
extService.recoveryTask(long taskId, ResultCallBack callBack)
```
####获取历史任务
* @param callBack 任务集;
```java
extService.getHistoryTask(ResultCallBack<List<Task>, Void, Void> callBack)
```
####置顶任务消息
* @param msgId    传入TaskId
* @param isTop    是否置顶
```java
extService.topTask(long msgId, byte isTop, ResultCallBack callBack)
```
####完成任务
* @param taskID   需要完成的任务 id
```java
extService.finishTask(long taskID, ResultCallBack callBack) 
```
####获取指派的任务
* @param callBack 任务集;
```java
extService.getApTask(ResultCallBack<List<Task>, Void, Void> callBack)
```
####获取任务上下文
* @param taskId   指定的TaskID
* @param callBack 任务上下文;
```java
extService.getBodyTask(long taskId, ResultCallBack<String, Void, Void> callBack)
```

