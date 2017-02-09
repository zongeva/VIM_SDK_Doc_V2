
##认证
###登录
####手动登录
~~~objectivec

/*!

* @method  loginWithAccount-登录

* @descript  全局登录接口

* @param account 登录帐号

* @param passwor 登录密码

* @param loginType  登录类型

* @param region  国家或者地区编码

* @param domain  服务器标识或者服务器地址

* @param completion  登录结果(error为空表示成功,失败有具体失败原因说明)

* @result  空

*/

- (void)loginWithAccount:(NSString*)account

  password:(NSString*)pwd

 loginType:(login_type)loginType

  region:(NSString*)regionCode

  domain:(NSString *)domain

  completion:(void (^) (NSError *error))completion;
~~~

####通过密码验证历史账号登录
~~~objectivec
/*!

* @method  loginWithAccount-登录

* @descript  全局登录接口

* @param password  登录密码

* @param completion  登录结果(error为空表示成功,失败有具体失败原因说明)

* @result  空

*/

- (void)autoLoginWithPassword:(NSString*)password

 	completion:(void (^) (NSError *error))completion;
~~~

####自动登录
利用历史账号登录，登录结果（error为空表示成功，失败有具体失败原因说明）

~~~objectivec
- (void)autoLogin:(void (^) (NSError *error))completion;
~~~
####登出
退出登录,登录接口回调代码块

~~~objectivec
- (void)logoff:(void (^)(NSError *error))completion;

~~~
###应用授权
授权第三方应用key

~~~objectivec
- (void)clientKey:(void (^) (NSError *error,NSString *clientKey))completion;	
~~~
###其他功能或信息获取
获取服务器时间

~~~objectivec
- (void)serverTime:(void (^) (NSError *error,int64_t time))completion;
~~~
通过注册apns推送获取到的设备标识

~~~objectivec
- (void)registerPushToken:(NSString*)pushToken completion:(void (^) (NSError *error))completion;
~~~
账号激活状态（打开或者关闭notify消息,用于多服务器子账号或者主账号程序运行状态切换），设置是否成功

~~~objectivec
- (bool)makeActivationState:(active_state)state;
~~~
###注册、找回密码
注册第一步，获取验证码和注册标识

~~~objectivec
- (void) registery1:(void (^) (bool state,NSDictionary *object))completion;
~~~
注册第二步，设置昵称和密码

~~~objectivec
- (void) registery2:(void (^)(bool, NSDictionary *))completion;
~~~
找回密码第一步，同注册第一步

~~~objectivec
- (void) resetPwd1:(void (^) (bool state,NSDictionary *object))completion;
~~~
找回密码第二部，设置新的密码

~~~objectivec
- (void) resetPwd2:(void (^)(bool, NSDictionary *))completion;
~~~


##全局运行数据
获取SDK版本号

```objectivec
- (NSString*)version;
```
**通过证书注册应用（必须注册应用才能使用SDK）**

```objectivec
/*!

* @method  registerApp

* @descript  证书注册应用

* @param certificatePath 证书地址

* @param cacheFolder 缓存保存地址

* @result  初始化后的缓存地址

*/

- (NSString*)registerApp:(NSString*)certificatePath onCachePath:(NSString*)path;
```


获取指定服务器信息
 
~~~objectivec
- (NSDictionary*)getServeInfo:(NSString*)serveName;
~~~
获取会话记录列表

~~~objectivec
-(LDChatListModel *)chatListModel;
~~~
获取联系人列表

~~~objectivec
-(LDContactListModel *)contactListModel;
~~~	
通过id查找本地联系人，获得联系人

~~~objectivec
- (LDContactModel*)localContact:(int64_t)ID;
~~~
获取机器人列表

~~~objectivec
- (LDRobotListModel *)robotListModel;
~~~ 
通过id获取本地机器人

~~~objectivec
- (LDRobotModel*)localRobot:(int64_t)ID;
~~~
获取群组列表

~~~objectivec
- (LDGroupListModel *)groupListModel;
~~~
通过id获取本地群组

~~~objectivec
- (LDGroupModel*)localGroup:(int64_t)ID;
~~~
获取当前群的群成员集合

~~~objectivec
- (LDGroupMemberListModel*)groupMembers;
~~~
获取组织架构的企业列表

~~~objectivec
- (LDEnterpriseListModel *)enterpriseListModel;
~~~
获取最新系统的提示消息

~~~objectivec
- (LDSysMsgModel*)sysMessage;
~~~
获取登录用户信息

~~~objectivec
- (LDMyselfModel*)mySelfInfo;
~~~
获取登录账号信息

~~~objectivec
- (LDAuthModel*)loginConfig;
~~~
获取组织架构企业列表

~~~objectivec
- (void)queryEnterpriseList;
~~~
获取密码强度信息

~~~objectivec
- (void)queryPasswordInfo;
~~~
密码强度信息

~~~objectivec
- (LDPasswordStipulateModel*)passwordInfo;
~~~
头像图片

~~~objectivec
/*!

* @method  avatar

* @descript  获取头像图片

* @param avatar  头像名

* @param image 缺省图片

* @result  头像图片

*/

- (UIImage*)avatar:(NSString*)avatar withDefault:(NSString*)image;
~~~
解密后的图片

~~~objectivec

/*!

* @method  imageWithKey

* @descript  获取图片

* @param key 文件密钥

* @param imagePath 文件路径

* @param image 缺省图片

* @result  解密后的图片

*/

- (UIImage*)imageWithKey:(NSString*)key fromPath:(NSString*)imagePath withDefault:(NSString*)image;

~~~
加密

~~~objectivec
/*!

* @method  encryptFile

* @descript  加密文件接口

* @param srcPath  源文件路径

* @param targetPath 加密后文件路径

* @param key  加密秘钥

* @result  加密是否成功

*/

- (bool)encryptFile:(NSString*)srcPath toFile:(NSString*)targetPath withKey:(NSString*)key;

~~~
id范围

~~~objectivec
/*!

* @method  idRange

* @descript  id范围(判断id是群、个人、机器人等)

* @param target  判断对象id

* @result  id范围

*/

-(IDRange)idRange:(int64_t)target;
~~~
##推送模块
数据同步状态通知

登录成功后，SDK会立即同步数据(聊天消息、用户资料、用户关系、群资料、离线消息等),并推送给注册监听

监听最近会话列表

~~~objectivec
- (void)chatListMoniter:(ChatListMoniter)moniter;
~~~
监听联系人列表

~~~objectivec
- (void)contactListMoniter:(ContactListMoniter)moniter;
~~~
新消息监听

~~~objectivec
- (void)messageMoniter:(MessageMoniter)moniter forTarget:(int64_t)target;
~~~
个人信息变动监听

~~~objectivec
- (void)myselfInfoMoniter:(MyselfInfoMoniter)moniter;
~~~
群成员信息变动监听

~~~objectivec
- (void)groupMembersMoniter:(GroupMembersMoniter)moniter;
~~~
好友、群、群成员、机器人头像更新并下载到本地后的通知，在需要监听时灵活调用

~~~objectivec
- (void)headerRefreshMoniter:(HeaderRefreshMoniter)moniter;
~~~
上下线提醒或退出或被踢下线

~~~objectivec
- (void)kick:(Kick)moniter;
~~~