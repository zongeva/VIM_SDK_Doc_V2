
##账户管理
###好友
设置重要好友

```objectivec
- (void)addStar:(void (^) (NSError *error))completion;
```
取消重要好友

```objectivec
- (void)removeStar:(void (^) (NSError *error))completion;
```
添加备注

```objectivec
- (void)resetRemark:(void (^) (NSError *error))completion;
```
修改聊天背景

```objectivec
- (void)modifyChatImage:(void (^) (NSError *error))completion;
```
网络检索，返回包含用户，群组，机器人数组的字典

```objectivec
- (void)contactsWithKey:(NSString*)key
 
                 onArea:(search_area)area
 
                forType:(search_type)type
 
             completion:(void (^) (NSError *error,NSDictionary *info))completion;
```
添加好友

```objectivec
- (void)addContact:(LDUserModel *)contact
 
       verifyInfo:(NSArray<NSString*> *)info
 
           remark:(NSString *)remark
 
       completion:(void (^) (NSError *error))completion;
```       
解除好友关系

```objectivec
- (void)removeContact:(LDContactModel*)contact
 
           delEither:(BOOL)deleteEither
 
          completion:(void (^) (NSError *error))completion;
```         
###群组
####群操作权限

| 权限  | 临时群  |
|:------:|:--------:|  
|邀请成员|任何人|  
|可以被搜索|可以|
|踢出成员|群主/管理员|
|解散群|群主|
|退群|普通群成员/管理员|
|更改群名称|群主/管理员|
|更改群公告|群主/管理员|
|更改群介绍|群主/管理员|
|转让|群主|   

####群组model提供的接口
获取群信息

```objectivec
- (void)syncGroupInfo:(groupInfo)info;
```
修改群资料

```objectivec
- (void)updateGroupInfo:(void (^)(NSError *error))completion;
```
修改群头像

```objectivec
- (void)modifyGroupIcon:(void (^) (NSError *error))completion;
```
修改群聊背景图片

```objectivec
- (void)modifyChatImage:(void (^) (NSError *error))completion;
```
设置加入群的验证方式

```objectivec
- (void)setGroupVerify:(void (^) (NSError *error))completion;
```
转让群

```objectivec
- (void)transferGroup:(LDGroupMemberModel *)contact
			   completion:(void (^)(NSError*error))completion;
```			   
设置群V标

```objectivec
- (void)setGroupVsign:(void (^) (NSError *error))completion;
```
设置群消息通知方式

```objectivec
- (void)changeNotificationType:(notification_type)type completion:(void (^) (NSError *error))completion;
```
设置群消息通知内容

```objectivec
- (void)changeNotificationContent:(notification_content)content completion:(void (^) (NSError *error))completion;
```
创建群聊

```objectivec
- (void)createGroupWithInviteMembers:(NSArray <LDUserModel *>*)contactList
                              completion:(void (^)(NSError *error, NSDictionary *info))completion;
```                             
申请加入群

```objectivec
- (void)joinGroup:(LDGroupModel *)group
           VerifyInfo:(NSString *)info
           completion:(void (^)(NSError *error))completion; 
```           
解散群

```objectivec
- (void)dismissGroup:(LDGroupModel *)group
              completion:(void (^)(NSError *error))completion;  
```                       			   
退出群

```objectivec
- (void)quitGroup:(LDGroupModel *)group
           completion:(void (^)(NSError *error))completion;
```           
####个人信息
用于登录用户修改头像

```objectivec
- (void)modifyMyselfHeader:(void (^)(NSError *error, LDMyselfModel *myself))block;
```
同于登录用户修改个人信息

```objectivec
- (void)modifyMyselfBasicInfo:(void (^)(NSError *error, LDMyselfModel *myself))block;
```
个人设置项值获取，对应的设置项值

```objectivec
- (NSNumber*)myselfConfigure:(configInfo)configure;
```
个人设置相关信息修改

```objectivec
- (void)modifyMyselfConfigure:(NSDictionary *)configureInfo callBack:(void (^) (NSError *error))completion;
```

个人设置项值获取，开启状态

```objectivec
- (BOOL)myselfSetting:(settingInfo)info;
```
个人信息修改

```objectivec
- (void)modifyMyselfSetting:(settingInfo)settingInfo completion:(void (^) (NSError *error))completion;
```
全局免打扰状态

```objectivec
- (BOOL)noDisturbMode;
```
改变全局免打扰模式

```objectivec
- (void)changeNodisturbModel:(void (^) (NSError *error))completion;
```
获取验证码

```objectivec
- (void)getCode:(NSString *)phoneNum callBack:(void (^)(NSError *error))completion;
```
绑定手机

```objectivec
- (void)bindPhone:(NSString *)phone callBack:(void (^)(NSError *error))completion;
```
绑定邮箱

```objectivec
- (void)bindEmail:(NSString *)email callBack:(void (^)(NSError *error))completion;
```
##扩展功能
###黑名单
添加好友到黑名单

```objectivec
- (void)addContactsToBlackList:(NSMutableArray<LDUserModel *> *)contactList
 
                    completion:(void (^) (NSError *error))completion;
 ```                   
移除黑名单里的好友

```objectivec
- (void)removeContactsFromBlackList:(NSMutableArray<LDUserModel *> *)contactList
 
                         completion:(void (^) (NSError *error))completion;
```                         
 清空黑名单
 
```objectivec
- (void)clear:(void (^) (NSError *error))completion;
```
获取黑名单id列表

```objectivec
- (void)requestBlackList:(void (^) (NSError *error,NSArray<NSNumber*>* members))completion;
```
###隐藏好友
添加隐藏的好友或群组

```objectivec
- (void)addHiddenID:(NSArray<NSNumber *>*)items
 
        completion:(void (^) (NSError *error))completion;
```        
 删除隐藏的好友或群组
 
```objectivec
- (void)removeHiddenID:(NSArray<NSNumber *>*)items
 
           completion:(void (^) (NSError *error))completion;
```
 获取被隐藏的好友
 
```objectivec
- (void)queryHiddenIDs:(void (^) (NSError *error,NSArray *items))completion;
```
修改隐藏好友密码

```objectivec
- (void)resetHiddenPassword:(void (^) (NSError *error))completion;
```
###记事本

```objectivec
/*!
 
*@method    queryNoteByBeginID
 
*@descript  添加隐藏的好友或群组 起始消息ID offsetFlag = 0 msgBeginID = 0时，代表从最大的消息Id进行查找
 
*@param     beginID 起始消息ID offset 查询的数量 offsetFlag 0.消息Id由大到小偏移 1.消息Id由小到大偏移 offsetFlag
 
*@result    completion回调代码块
 
*/
 
- (void)queryNoteByBeginID:(long long)beginID
 
                    offset:(int)offset
 
                      flag:(int)flag
 
                completion:(void (^) (NSError *error))completion;
 
```   
添加一个笔记

```objectivec
- (void)addNote:(LDNoteModel *)note
 
     completion:(void (^) (NSError *error))completion;
```
删除笔记
 
```objectivec
- (void)deleteNotes:(NSArray<NSNumber *>*)IDs
 
         completion:(void (^) (NSError *error))completion;
```         
 编辑笔记

```objectivec 
- (void)editNote:(LDNoteModel *)note
 
      completion:(void (^) (NSError *error))completion;
```      
 创建note对象

```objectivec 
+(instancetype)buildWithTitle:(NSString*)title
 
                          content:(NSString*)content
 
                          keyword:(NSString *)keyword
 
                             type:(NoteType)type
 
                       sourceType:(NoteSource)sourceType;
```                         
###任务
获取发送的任务消息列表

```objectivec
- (void)querySendMessages:(void (^) (NSError *error))completion;
```
获取接受的任务消息列表

```objectivec
- (void)queryReceiveMessages:(void (^) (NSError *error))completion;
```
获取历史任务消息列表

```objectivec
- (void)queryHistoryMessages:(void (^) (NSError *error))completion;
```	
任务发送接口

```objectivec
- (void)sendMessageTo:(int64_t)target onStatus:(MessageSendStatus)status;
```	
查询任务上下文

```objectivec
- (void)queryMessageBody:(void (^) (NSError *error))completion;
```
任务消息置顶

```objectivec
- (void)moveMessageTop:(void (^) (NSError *error))completion;
```
恢复任务消息

```objectivec
- (void)recoveryTask:(void (^) (NSError *error))completion;
```
完成任务消息

```objectivec
- (void)completeTask:(void (^) (NSError *error))completion;
```
###房间
创建房间

```objectivec
- (void)createRoom:(NSString*)roomName withChats:(NSArray*)chats completion:(void (^) (NSError *error,LDRoomListModel *roomList))completion;
```
删除房间

```objectivec
- (void)removeRoom:(LDRoomModel*)room completion:(void (^) (NSError *error,LDRoomListModel *roomList))completion;
```
修改房间名称

```objectivec
- (void)updateRoomName:(NSString*)roomName completion:(void (^) (NSError *error))completion;
```
###多服务器
通过缓存路径初始化子账号

```objectivec
- (instancetype)initWithCachePath:(NSString*)path;
```
全局登录接口

```objectivec
/*!
 
* @method    loginWithAccount-子账号手动登录,用于添加子账号
 
* @descript  全局登录接口
 
* @param     account    登录帐号
 
* @param     password   登录密码
 
* @param     loginType  登录类型
 
* @param     region 国家或者地区编码
 
* @param     domain 服务器标识或者服务器地址
 
* @param     completion 登录结果(error为空表示成功,失败有具体失败原因说明)
 
* @result    空
 
*/
 
- (void)loginWithAccount:(NSString*)account
 
                password:(NSString*)pwd
 
               loginType:(login_type)loginType
 
                  region:(NSString*)regionCode
 
                  domain:(NSString *)domain
 
              completion:(void (^) (NSError *error))completion;
 
 
 /*!
 
* @method    loginWithLoginAuth-子账号自动登录
 
* @descript  全局登录接口
 
* @param     loginAuth  主账号关联的子账号信息
 
* @result    空
 
*/
 
- (void)loginWithLoginAuth:(LDAuthModel*)loginAuth
 
                completion:(void (^) (NSError *error))completion;
 
``` 
同步消息

```objectivec
- (void)loadOfflineMessage;
```
未读消息数

```objectivec
- (NSInteger)numberOfUnreadMessage;
```
获取子账号列表

```objectivec
- (NSArray*)multiServerInfo;
```
绑定子账号

```objectivec
- (bool)bindMultiServer:(NSArray<LDMultiServerModel *>*)servers;
```
切换主账号

```objectivec
- (bool)switchMultiServer:(LDMultiServerModel*)server;
```

                                     

	
   
