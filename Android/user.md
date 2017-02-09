## 用户

### 获取UserService

```
UserService userService = ClientManager.getDefault().getUserService();
```

### 获取账户信息

```
Account account = userService.getAccountInfo();
```

### 更新用户信息

传入的参数：（Account对象, ResultCallBack）

建议创建一个新的Account 对象，对需要修改的字段进行赋值，该参数不能不为null。

```
userService.updateAccountInfo(Account account, ResultCallBack callBack);
```

### 更新用户头像

传入的参数：（本地图像路径，ResultCallBack）

```
userService.updateAccountAvatar(String avatar, final ResultCallBack callBack);
```

### 账号设置

#### 设置

传入的参数：（设置值，设置类型，ResultCallBack）

| type | 说明              | 取值范围             |
| ---- | --------------- | ---------------- |
| 1    | 设置是否显示在线信息      | 0显示 1不显示 默认0     |
| 3    | 设置豆豆号查找         | 0允许 1不允许 默认0     |
| 4    | 设置手机号查找         | 0允许 1不允许 默认0     |
| 5    | 设置邮箱号查找         | 0允许 1不允许 默认0     |
| 6    | 设置分享更新          | 0提示更新 1不提示更新 默认0 |
| 7    | 新消息通知是否提醒       | 0提醒 1不提醒 默认0     |
| 12   | 多服务新消息通知是否提醒    | 0不始终提示 1始终提示 默认0 |
| 13   | 多服务设置V标好友始终提醒   | 0不始终提示 1始终提示 默认0 |
| 14   | 多服务设置设置@相关人始终提醒 | 0不始终提示 1始终提示 默认0 |

```
userService.setSetting(byte flag, int type, ResultCallBack callBack);
```

#### 获取

传入的参数：（设置项类型，ResultCallBack<UserSetting, Void, Void>）

设置项类型：type为1，则返回值为value_i64第一位 如果type=0,返回所有字段，每个字段所占的位于type相对应。

```
userService.getSetting(int type, ResultCallBack<UserSetting, Void, Void> callBack);
```

### 隐藏对象

#### 通过密码获取隐藏对象（好友或者群）

传入的参数：（之前设置过的密码，ResultCallBack<List<Long>, Boolean, Void>）

callBack 返回对象ID合集 ,true代表存在此密码，false代表不存在

```
userService.getHiddenTarget(String password, ResultCallBack<List<Long>, Boolean, Void> callBack);
```

#### 设置隐藏对象（好友或者群）

传入的参数：（设置的密码，设置的隐藏好友集合）

```
userService.setHiddenTarget(String password, List<Long> hiddenIDs, ResultCallBack callBack);
```

#### 删除隐藏对象(好友或群)

传入的参数：（密码，要删除的ID集合，ResultCallBack）

```
userService.delHiddenTarget(String password, List<Long> hiddenIDs, ResultCallBack callBack)
```

#### 更改隐藏密码

```
userService.changeHiddenPsw(String oldPwd, String newPwd, ResultCallBack callBack);
```

### 全局勿扰模式

获取

callback回调成功返回 （起始时间,结束时间,是否打开）

```
userService.getGlobalNoDisturbMode(ResultCallBack<Integer, Integer, Boolean> callBack);
```

设置

```
userService.setGlobalNoDisturbMode(int startTime, int endTime, boolean isOpen, ResultCallBack callBack);
```

### 针对目标用户的勿扰模式

勿扰模式的取值：1为接收提醒 2表示不提醒仅显示数字 3:为免打扰, 默认1

获取

callback返回成功 （用户ID,设置的值）

~~~
userService.getUserNoDisturbMode(long targetID, ResultCallBack<Long, Byte, Void> callBack);
~~~

设置

```
userService.setUserNoDisturbMode(long targetId, byte value, ResultCallBack callBack);
```

### 针对目标消息的通知模式

模式取值：1.通知详情 2.通知源，隐藏内容 3.完全隐藏

获取

```
userService.getMsgNotifyMode(long targetId, ResultCallBack<Long, Byte, Void> callBack);
```

设置

```
userService.setMsgNotifyMode(long targetId, byte value, ResultCallBack callBack);
```

### 获取服务器时间

单位毫秒

```
userService.getServerTime(ResultCallBack<Long, Void, Void> callBack);
```

### 本地配置

以键值对方式保存

```
userService.addLocalSetting(List<LocalSetting> items, ResultCallBack callBack);
```

获取本地配置

传入的参数：（获取的配置信息的键集合，ResultCallBack<List<LocalSetting>, Void, Void>）

```
userService.getLocalSetting(List<String> keys, ResultCallBack<List<LocalSetting>, Void, Void> callBack);
```

更新本地配置信息

```
userService.updateLocalSetting(List<LocalSetting> newItems, ResultCallBack callBack);
```

删除本地配置信息

```
userService.deleteLocalSetting(List<String> keys, ResultCallBack callBack);
```

### 个人设置项

个人设置项使用PersonalData表示

其中type的取值如下：

| type              | 取值范围                                |
| ----------------- | ----------------------------------- |
| 1(生日)/2(电话)/3(邮件) | 1：所有人可见 2：仅好友可见 3：仅自己可见，默认1         |
| 4(好友验证方式)         | 1：需要验证信息,2:不允许任何人添加,3:允许任何人添加，默认1   |
| 5(V标)             | 1:表示始终有声音提醒，2：表示始终无声音提醒 3:不始终提醒，默认1 |
| 6(@相关人提醒模式)       | 1:表示始终有声音提醒，2：表示始终无声音提醒 3:不始终提醒，默认1 |
| 7(全局通知消息内容展现模式)   | 1:通知详情，2：通知源，隐藏内容 3:完全隐藏，默认2        |

设置

~~~
userService.setPersonalData(List<PersonalData> items, ResultCallBack callBack);
~~~

获取

```
userService.getPersonalData(List<Integer> types, ResultCallBack<List<PersonalData>, Void, Void> callBack);
```

### 应用市场

通过应用ID获取应用信息

```
userService.getAppInfo(long appId, ResultCallBack<EntAppInfo, Void, Void> callBack);
```

查询应用市场应用信息

```
userService.queryMarketApplication(QueryMarketApplication qData, ResultCallBack<SmallMarketAppPage, Void, Void> callBack);
```

删除/添加应用

type的取值：添加2， 删除 4。

```
userService.addOrDeleteApplication(byte type, long appID, ResultCallBack callBack);
```

获取已安装应用

```
userService.getInstalledApplication(ResultCallBack<List<SmallMarketAppInfo>, Void, Void> callBack);
```

### 表情功能

单个查询表情包

```
userService.queryEmoticonPackageByLabel(String label, ResultCallBack<List<EmoticonPackage>, Void, Void> callBack);
```

单个表情查询

```
userService.queryEmoticon(String md5, ResultCallBack<List<Emoticon>, Void, Void> callBack);
```

根据表情包标识查询所有表情

```
userService.queryEmoticonByPackageMd5(String md5, ResultCallBack<List<Emoticon>, Void, Void> callBack);
```

获取自己的自定义表情

```
userService.queryMyEmoticon(ResultCallBack<List<Emoticon>, Void, Void> callBack);
```

单个查询表情包

```
userService.queryEmoticonPackage(String md5, ResultCallBack<EmoticonPackage, Void, Void> callBack)
```

分页查询表情包

```
userService.getEmoticonPackageList(int pageNum, int pageSize, ResultCallBack<PageQueryEmoticon, Void, Void> callBack);
```

增删自定义表情

```
userService.addOrDeleteCustomEmoticon(boolean isAdd, Emoticon emoticon, ResultCallBack<Integer, String, List<EmoticonResult>[]> callBack);
```

### 本地数据导入导出

```
userService.transLocalData(TransferLocalData req, ResultCallBack callBack);
```

