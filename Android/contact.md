
##通讯录 
```java
ContactService contactService =  ClientManager.getDefault().getContactService()
```


###同步调用返回通讯录列表
```java
List<Contact> contactList = contactService.getList();
```

###根据用户id返回通讯录信息

 -  传入参数：（好友ID)
   
```java
Contact contact = contactService.findItemByID(long userID);
```

###添加联系人

 -  传入参数：（好友ID，备注，验证信息，回调)
   
```java
contactService.add(long userID, String remark, String info, ResultCallBack callBack);
```

###获取联系人验证方式

 -  传入参数：（好友ID，回调)
   
```java
contactService.getVerifyType(long userID, ResultCallBack<ContactVerifyType, Void, Void> callBack);
```

###删除联系人

 -  传入参数：（好友ID，回调)
   
```java
contactService.remove(long userID, ResultCallBack callBack) ;
```

###更新联系人信息（星标&V标&备注）

 -  传入参数：（contact，回调)
   
```java
contactService.updateInfo(Contact info, ResultCallBack callBack) ;
```
###设置聊天背景

 -  传入参数：（用户id，聊天背景路径，回调)
   
```java
contactService.setBackground( long userID,  String imgPath,  ResultCallBack callBack) ;
```

###设置聊天背景

 -  传入参数：（用户id，聊天背景路径，回调)
   
```java
contactService.setBackground( long userID,  String imgPath,  ResultCallBack callBack) ;
```


###获取联系人在线状态

 -  传入参数：（users 联系人集合 如果为空则查所有联系人状态，回调)
   
```java
contactService.getOnline(List<Long> users, ResultCallBack<List<OnlineState>, Void, Void> callBack) ;
```


###获取联系人信息 ( 同步接口 )

 -  传入参数：（用户id)
   
```java
contactService.getInfo(long userID);
```


###获取联系人/陌生人信息（异步接口）

 -  传入参数：（用户id，回调)
   
```java
contactService.getInfo( long userID, ResultCallBack<Contact, Void, Void> callBack) ;
```


###判断联系人与自己是否是好友关系 ( 同步接口 )

 -  传入参数：（用户id)
   
```java
  boolean  isBuddy=contactService.isBuddy(long userID);
```


###获取黑名单

 -  传入参数：（回调 返回黑名单列表)
   
```java
  contactService.getBlackList(ResultCallBack<List<Long>, Void, Void> callBack) ;
```



###添加黑名单

 -  传入参数：（要加入的黑名单对象ID集合 ，回调 返回添加是否成功)
   
```java
  contactService.addBlackList(List<Long> ids, ResultCallBack callBack) ;
```


###删除黑名单

 -  传入参数：（要删除的黑名单对象ID集合，为空则删除所有黑名单用户 ，回调 返回是否移除成功)
   
```java
  contactService.removeBlackList(List<Long> ids, ResultCallBack callBack) ;
```


###根据条件查询拓展字段信息

 -  传入参数：（要查询的字段，为空时代表查询所有字段，为空则删除所有黑名单用户 ，回调 查询信息)
   
```java
  contactService.queryExtendedField(String dicKey, ResultCallBack<List<EnterpriseDictionary>, Void, Void> callBack) ;
```

###上传通讯录

 -  传入参数：（上传对象集合 ，回调 推荐联系人)
   
```java
  contactService.postContact(List<PhoneBookContact> contacts, ResultCallBack<List<RecommendContact>, Void, Void> callBack);
```


###在线状态更新 监听

```java
  contactService.observeOnlineListener(OnlineStateListener listener);
```








