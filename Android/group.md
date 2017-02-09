##群 
```java
GroupService grouService = ClientManager.getDefault().getGroupService()
```

###群列表
   
```java
List<TinyGroup> = grouService.getList();
```



###创建群
 -  传入参数：（群等级，群名称，群成员id，回调 群id)
   
```java
  grouService.create(int level, String name, List<Long> members, ResultCallBack<Long, Void, Void> callBack);
```


###添加群
 -  传入参数：（群id，验证信息，回调 是否添加成功)
   
```java
  grouService.add(long groupID, String verifyInfo, ResultCallBack callBack);
```

###解散/退出群
 -  传入参数：（群id，回调 解散/退出是否成功)
   
```java
  grouService.remove(long groupID, ResultCallBack callBack);
```


###转让群
 -  传入参数：（群id，新群主id，回调 转让是否成功)
   
```java
  grouService.transfer(long groupID, long memberID, ResultCallBack callBack);
```

###获取群设置
 -  传入参数：（群id，回调 验证类型: 1.不允许任何人添加, 2.需要验证信息, 3.允许任何人添加.是否  允许群成员邀请好友加入群: 1.允许 2.不允许 )
   
```java
  grouService.getSetting(long groupID, ResultCallBack<Byte, Byte, Void> callBack);
```


###设置群设置
 -  传入参数：（群id，验证类型，是否允许成员邀请用户，回调 设置是否成功)
   
```java
  grouService.setSetting(long groupID, byte verifyType, byte isAllow, ResultCallBack callBack);
```



###获取群详细信息 （同步接口）
 -  传入参数：（群id)
   
```java
  grouService.getDetailInfo(long groupID);
```


###获取群详细信息 （异步）
 -  传入参数：（群id,回调 返回群详细信息)
   
```java
  grouService.getDetailInfo(long groupID, ResultCallBack<Group, Void, Void> callBack) ;
```

###更新群信息（群主/管理员操作）
 -  传入参数：（群id, GroupUpdate对象，回调 是否更新成功)
   
```java
  grouService.updateInfo(long groupID, GroupUpdate updateInfo, ResultCallBack callBack) ;
```

###更新群头像，（群主/管理员操作）
 -  传入参数：（群id, 图像路径，回调 是否更新成功)
   
```java
  grouService.updateAvatar( long groupID, String avatar, final ResultCallBack callBack) ;
```




###管理员设置群聊天背景
 -  传入参数：（群id, 群背景图片路径，回调 是否设置成功)
   
```java
  grouService.setBackgroundByAdmin( long groupID, String imagePath, final ResultCallBack callBack) ;
```



###邀请群成员
 -  传入参数：（群id, 邀请群成员，回调 是否邀请成功)
   
```java
  grouService.inviteMember(long groupID, List<Long> members, ResultCallBack callBack) ;
```

###移除群成员
 -  传入参数：（群id, 移除群成员id，回调 是否移除成功)
   
```java
  grouService.removeMember(long groupID, long memberID, ResultCallBack callBack) ;
```


###设置群成员信息
 -  传入参数：（成员信息 member 必须设置 memberID和groupID, 回调 是否设置成功)
   
```java
  grouService.setMemberInfo(Member member, ResultCallBack callBack)  ;
```

###判断用户是否在群里 (同步接口)
 -  传入参数：（群id ，用户id，注return false代表不是群成员)
   
```java
  grouService.isInGroup(long groupID, long memberID) ;
```



###获取群成员信息 (同步接口)
 -  传入参数：（群id ，群成员id，注return member 群成员信息)
   
```java
  grouService. getMemberInfo(long groupID, long memberID) ;
```



###获取群成员列表
 -  传入参数：（群id ，回调 群成员列表)
   
```java
  grouService. getMemberList(long groupID, ResultCallBack<List<Member>, Void, Void> callBack)  ;
```


###获取群文件列表
 -  传入参数：（群id ，起始id，数量，偏移标志0为向上1为向下，回调 群文件列表)
   
```java
  grouService. getFileList(long groupID, long beginID, int count, byte flag, ResultCallBack<List<FileInfo>, Void, Void> callBack) ;
```


###删除群文件
 -  传入参数：（群文件id集合 ，回调 是否删除成功)
   
```java
  grouService. deleteFile(List<Long> files, ResultCallBack callBack);
```

###获取个人群聊背景图片
 -  传入参数：（群id ，回调 聊天背景图片路径)
   
```java
  grouService.getPersonalGroupImg(long groupID, ResultCallBack<String, Void, Void> callBack);
```

###设置个人群聊背景图片
 -  传入参数：（群id ，聊天背景图片地址，回调 是否设置成功)
   
```java
  grouService.setPersonalGroupImg( long groupID,  String imgUrl,  ResultCallBack callBack);
```


###设置群消息免打扰模式
 -  传入参数：（群id ，mode提醒模式 1：提示并接收消息；2：不提示，接收仅显示数目；3：屏蔽消息，回调 是否设置成功)
   
```java
  grouService.setGroupMsgRemindType(long groupID, byte mode, ResultCallBack callBack) ;
```

###获取群消息免打扰模式
 -  传入参数：（群id ，回调 提醒模式)
   
```java
  grouService.getGroupMsgRemindType(long groupID, ResultCallBack<Byte, Void, Void> callBack);
```


###设置群 v标
 -  传入参数：（群id ，是否为v标群，回调 是否设置成功)
   
```java
  grouService.setGroupVSign(long groupID, boolean vSign, ResultCallBack callBack) ;
```


###设置群消息内容提醒模式
 -  传入参数：（群id ，群通知消息内容模式: 1、通知详情  2、通知源，隐藏内容  3、完全隐藏，回调 是否设置成功)
   
```java
  grouService.setGroupMsgContentMode(long groupID, byte msgMode, ResultCallBack callBack) ;
```

