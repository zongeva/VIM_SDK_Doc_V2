
##会话消息
###发送消息
发送普通文本消息

```objectivec
/*!

* @method    sendMessage

* @descript  发送普通文本消息

* @param     message 消息对象

* @param     status 消息发送状态

* @result    空

*/

- (void)sendMessage:(LDMessageModel*)message

           onStatus:(MessageSendStatus)status;

```
发送文件消息

```objectivec
/*!

* @method    sendMessage

* @descript  发送文件消息

* @param     message 消息对象

* @param     progress 文件上传进度

* @param     status 消息发送状态

* @result    空

*/

- (void)sendMessage:(LDMessageModel *)message

         onProgress:(FileUploadProgress)progress

           onStatus:(MessageSendStatus)status;

```
###接收消息
接收消息的消息列表

```objectivec
/*!

* @method    receivedMessage

* @descript  收到消息时更新对应chat的消息列表

* @param     block

             回调代码块

* @result    空

*/

- (void)receivedMessage:(LDMessageModel*)message;
```
###会话消息操作
返回会话消息列表

```objectivec
- (LDMessageListModel*)chatMessageList;
```
返回所给类型的本地消息列表

```objectivec
- (void)searchMessagesWithType:(MessageType)type completion:(void (^) (NSError* error,LDMessageListModel *messaages))completion;
```
是否置顶会话

```objectivec
- (bool)isTopChat;
```
消息来源

```objectivec
- (MessageOwner)chatOwner;
```
设置消息已读

```objectivec
- (void)makeMessageReaded;
```
获取本地聊天记录，historyMessages-此方法需要初始化新对象

```objectivec
- (void)historyMessages:(void (^)(NSError *error,LDMessageListModel *messageList))completion;
```
搜索对应关键字并返回对应本地消息列表

```objectivec
- (void)searchMessagesWithKeyword:(NSString *)keyword completion:(void (^) (NSError* error,LDMessageListModel *chatList))completion;
```
通过关键字搜索chat对象

```objectivec
- (void)searchChatWithKeyword:(NSString *)keyword
                      completion:(void (^) (NSError* error,NSArray *chats))completion;
```
删除会话记录

```objectivec
/*!

* @method    removeChatRecord

* @descript  删除会话记录

* @param     chatModel

             需要删除的会话

* @param     completion

             删除会话记录回调

* @result    空

*/

- (void)removeChatRecord:(LDChatModel*)chatModel completion:(void (^) (NSError* error))completion;

```
删除历史消息

```objectivec
/*!

* @method    removeHistoryMessageFor

* @descript  删除历史消息

* @param     target

             需要删除历史消息的对象,可以是好友或者群,当target为空是表示删除所有历史消息

* @param     completion

             删除历史消息回调

* @result    空

*/

- (void)removeHistoryMessageFor:(LDItemModel*)target completion:(void (^) (NSError* error))completion;

```
置顶会话

```objectivec
/*!

* @method    makeTopChat

* @descript  置顶会话

* @param     chatModel

             需要置顶的会话

* @param     completion

             置顶会话回调

* @result    空

*/

- (void)makeTopChat:(LDChatModel*)chatModel completion:(void (^) (NSError* error))completion;

```
获取房间列表

```objectivec
- (void)roomList:(void (^) (NSError *error,LDRoomListModel *roomList))completion;
```

##基础消息类型
* SDK  提供一套完善的消息传输管理服务，包括收发消息，存储消息，上传下载附件，管理最近联系人等。

* SDK 原生支持发送文本，图片，文件，名片，语音和地理位置等 6 种类型消息，同时支持用户发送自定义的消息类型。

```objectivec
/*!

* @method    loadMedia

* @descript  加载消息文件

* @param     fileData  文件数据data

* @param     progress  加载文件进度

* @result    空

*/

- (void)loadMedia:(FileDownloadResult)fileData onProgress:(FileDownloadProgress)progress;
```
###文本消息
通过字符串初始化文本消息

```objectivec
- (instancetype)initWithText:(NSString*)text;
```
###图片消息
通过图片文件路径初始化图片消息

```objectivec
- (instancetype)initWithImage:(UIImage*)image;
```
###语音消息
通过语音文件路径初始化语音消息

```objectivec
- (instancetype)initWithAudio:(NSString*)audioPath;
```
###文件消息
初始化文件消息

```objectivec
- (instancetype)initWithFile:(NSString *)secretKey
 
                        sign:(int)fileSign
 
                     fileURL:(NSString *)fileurl;
```                     
###名片消息
初始化名片消息

```objectivec
- (instancetype)initWithItem:(LDItemModel*)item;
```
###位置消息
初始化位置消息

```objectivec
- (instancetype)initWithCoordinate:(CLLocationCoordinate2D)coordinate andAddress:(NSString*)address;
```
###系统提示消息
系统消息列表

```objectivec
- (void)sysMessages:(void (^) (NSError *error,LDListModel *sysMessageList))completion;
```
处理好友请求

```objectivec
- (void)verifyBuddy:(void (^) (NSError *error))completion;
```
处理入群请求

```objectivec
- (void)verifyGroup:(void (^) (NSError *error))completion;
```
设置系统消息已读

```objectivec
- (void)sysMsgReaded:(void (^) (NSError *error))completion;
```
                    