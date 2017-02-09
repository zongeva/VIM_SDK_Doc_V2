##基础消息功能
###IMClient
#####初始化SDK（init）
	/************************************************************************
	* @brief init（接口位于IMClient）
	* @description: 初始化SDK
	* @param[in] datapath 传入数据路径
	* @param[in] certpath 传入证书路径
	************************************************************************/
	virtual bool init(const std::string& dataPath, 
	const std::string& certPath) = 0;
	//初始化SDK需在初始化各类之前进行

	示例：
	void foo(void){
	char szPath[256] = { 0 };
	char szUtf8[256] = { 0 };
	::GetModuleFileName(NULL, szPath, 256);
	::PathRemoveFileSpec(szPath);
	std::string certPath(szPath);
	certPath += "\\linkdood.crt";
	service::IMClient::getClient()->init(szPath, certPath);
	//初始化SDK
	}

#####获取各个类的指针
	virtual std::shared_ptr<IAuthService> getAuth(void) = 0;
	//获取IAuthService指针
	virtual std::shared_ptr<INotifyService> getNotify(void) = 0;
	//获取INotifyService指针
	virtual std::shared_ptr<IFileService> getFile(void) = 0;
	//获取IFileService指针
	virtual std::shared_ptr<IChatService> getChat(void) = 0;
	//获取IChatService指针
	示例：
	void foo（）{
		std::shared_ptr<service::IAuthService> authservice；
		authservice=service::IMClient::getClient()->getAuth();
	}

---
###INotifyService
#####设置各监听类实例
	/************************************************************************
	* @brief setAuthObserver
	* @description: 设置认证类监听对象
	* @param[in] observer 传入监听对象实例
	************************************************************************/
	virtual void setAuthObserver(AuthObserverPtr observer) = 0;

	/************************************************************************
	* @brief setChatObserver
	* @description: 设置会话监听对象
	* @param[in] observer 传入监听对象实例
	************************************************************************/
	virtual void setChatObserver(ChatObserverPtr observer) = 0;

---
###IAuthController

#####登陆（login）
    /************************************************************************
	* @brief login
	* @description: 登录
	* @param[in] user 传入用户名 如果是手机账户格式为“0086158********”
	* @param[in] pwd 传入密码
	* @param[in] server 传入服务器地址，域名或IP均可
	* @param[inout] await 传入接收调用结果的回调函数
	* @return:	int64 返回当前执行的操作ID，用于取消该次执行
	************************************************************************/
	virtual int64 login(const std::string& user, const std::string& pwd, 
	const std::string& server, std::function<void(ErrorInfo& err,
	 int64 userid/*用户ID*/)> await)=0;


#####获取用户信息（getAccountInfo）
    /************************************************************************
	* @brief getAccountInfo
	* @description: 获取账户信息
	************************************************************************/
	virtual void getAccountInfo(void) = 0;
	//获取结果通过监听接口onAccountInfoChanged（位于IAuthObserver中）返回


#####修改密码（changePassword）
    /************************************************************************
	* @brief changePassword
	* @description: 修改密码
	* @param[in] oldPw 传入旧密码
	* @param[in] newPw 传入新密码
	* @param[inout] await 传入接收调用结果的回调函数
	************************************************************************/
	virtual void changePassword(const std::string& oldPw, const std::string& 
	newPw, std::function<void(ErrorInfo& info)>await) = 0;

#####退出登陆（logout）
    /************************************************************************
	* @brief logout（接口位于IAuthService）
	* @description: 登出
	************************************************************************/
	virtual void logout(void)=0;

---
###IAuthObserver
#####监听账户信息（onAccountInfoChanged）
	/************************************************************************
	* @brief onAccountInfoChanged
	* @description: 监听用户信息修改
	* @param[in] info 传入结果
	************************************************************************/
	virtual void onAccountInfoChanged(service::User& info) = 0;
	示例：
	class MyClass：public IAuthObserver{
		onAccountInfoChanged(service:: User& info){
			std::cout<<info.name<<std::endl;
		}	
	};

---

###IChatService
#####获取最近会话（getChatList）
    /************************************************************************
	* @brief getChatList
	* @description: 获取会话列表
	************************************************************************/
	virtual void getChatList(void) = 0;
	//获取结果通过监听onListChanged（位于IChatObserver）返回
#####获取历史消息（getMessages）
	/************************************************************************
	* @brief getMessages
	* @description: 获取历史消息
	* @param[in] targetid 传入会话对应的ID，群或者人
	* @param[in] msgid 传入查询消息的起始ID（可以为0），从该消息的下一条消息开始查询
	* @param[in] count 传入查询消息总数
	* @param[in] flag  传入偏移量 向上偏移 0；向下偏移 1
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void getMessages(int64 targetid, int64 msgid, int count,
	 int flag, std::function<void(ErrorInfo&, int64/*会话方ID*/,
    std::vector<MsgPtr>)> await) = 0;
#####发送消息（sendMessage）
    /************************************************************************
	* @brief sendMessage（接口位于IChatService）
	* @description: 发送消息
	* @param[in] msg 传入消息
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void sendMessage(Msg& msg, std::function<void(ErrorInfo&,
	 int64/*发送时间*/,int64/*消息ID*/)> await) = 0;
	//此接口用于发送各类型消息，消息类型由传入的参数Msg决定；发送文件和图片消息前,
	需要先上传文件和图片（接口位于IFileService）

---
###IChatObserver
#####监听新的消息(onMessageNotice)
	/************************************************************************
	* @brief onMessageNotice
	* @description: 监听新消息通知
	* @param[in] msg 传入新的消息
	************************************************************************/
	virtual void onMessageNotice(std::shared_ptr<service::Msg> msg) = 0;
#####监听会话列表变化（onListChanged）
	/************************************************************************
	* @brief onListChanged
	* @description: 监听会话列表更新通知
	* @param[in] flag 传入列表标志
	* 1:0x01　第一个包,　　 需要清理原来的数据
	* 2:0x02  中间的包，　　在原来的数据后面追加
	* 3:0x04  最后的包，　　最近会话发送完毕
	* @param[in] chats 传入会话集合
	************************************************************************/
	virtual void onListChanged(int flag, std::vector<std::shared_ptr
	<service::User> > chats) = 0;
#####监听离线消息（onOfflineMsgChanged）
	/************************************************************************
	* @brief onOfflineMsgChanged
	* @description: 监听离线消息通知
	* @param[in] msgs 传入离线消息集合
	************************************************************************/
	virtual void onOfflineMsgChanged(std::vector<OfflineMsg> msgs) = 0;
	//当监听到的消息为文件或者图片时，若要获取到文件或图片，则需要进行下载（下载接口
	位于IFileService）

	

---
###IFileservice
#####上传图片（uploadImage）
    /************************************************************************
	* @brief uploadImage
	* @description: 上传照片
	* @param[in] thumbimg 传入缩略图
	* @param[in] srcimg 传入原图
	* @param[in] property 传入图片属性
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void uploadImage(std::string thumbimg, std::string srcimg, 
	std::string property, std::function<void(int64 tagetid, 
	std::string orgijson, std::string thumbjson, int code)> await) = 0;


#####上传文件（uploadFile）
    /************************************************************************
	* @brief uploadFile
	* @description: 上传文件
	* @param[in] path 传入文件本地路径
	* @param[in] property 传入文件属性
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void uploadFile(
		std::string path, std::string property, std::function<void(
		int64 tagetid, std::string jasoninfo, int code)> await, std::function
		<void(int32 extra_req, int32 process, std::string info)> pro) = 0;

#####下载图片（downloadImage）

	/************************************************************************
	* @brief uploadImage（接口位于IChatService）
	* @description: 上传照片
	* @param[in] thumbimg 传入缩略图
	* @param[in] srcimg 传入原图
	* @param[in] property 传入图片属性
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void uploadImage(std::string thumbimg, std::string srcimg, 
	std::string property, std::function<void(int64 tagetid,
	std::string orgijson, std::string thumbjson, int code)> await) = 0;

---
#####下载文件（onMessageNotice&&downloadFile）
    /************************************************************************
	* @brief downloadImage（接口位于IChatService）
	* @description: 下载图片
	* @param[in] url 传入图片url
	* @param[in] property 传入图片属性
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual void downloadImage(	std::string url, std::string property, 
	std::function<void(ErrorInfo& info,std::string imgname,
	int64 targetid)> await) = 0;
#####解密文件或图片（）
	/************************************************************************
	* @brief decryptFile
	* @description: 解密文件或图片
	* @param[in] encryptkey 传入解密密码
	* @param[in] srcpath 传入原文件路径
	* @param[in] destpath 传入解密后文件路径
	* @param[in] await  传入接收结果回调
	************************************************************************/
	virtual bool decryptFile(
		std::string encryptkey,std::string srcpath,std::string destpath) = 0;