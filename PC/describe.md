
##SDK概述

   **为了让开发者方便快捷的接入Linkdood SDK，我们对SDK进行了封装，以类的形式对外暴露；
	类位于service/include/interface目录下。**


###SDK提供类的介绍
* IMClient：提供初始化SDK和获取各个类的指针
* INotifyService:设置各监听类的实例
* IAuthService:认证类；提供注册登录账户信息等认证相关的接口
* IAuthObserver：认证监听类；接收认证相关的数据推送
* IChatService: 会话类；提供发送接收消息等会话相关的接口
* IChatObserver:会话监听类；接收会话相关的数据推送
* IFileService:文件类；提供上传下载文件图片等相关接口


##接口调用示例
###示例接口名称：getAccountInfo
###示例接口所在类：IAuthService
###示例接口调用：
	1.创建类AuthController,使其继承于类IAuthObserver，并创建成员变量：
	  std::shared_ptr<service::IAuthService> m_service
	2.初始化AuthController：获取IAuthService指针和设置IAuthObserver监听实例
	3.在AuthController中用成员变量m_service调用IAuthService中getAccountInfo接口，
    并实现IAuthObserver中负责监听账户信息变动的接口onAccountInfo
	
	代码：
	void AuthController::Init(void){
		m_service = service::IMClient::getClient()->getAuth();
		//获取IAuthService指针
		service::IMClient::getClient()->->getNotify()->setAuthObserver(this);
		//设置IAuthObserver监听实例
	} //初始化AuthController

	void AuthController::GetAccountInfo(){
		m_service->getAccountInfo();
	}    //调用IAuthService中接口，获取账户信息
			
	void AuthController::onAccountInfoChanged(service::User& info){
	    std::cout<<info.name<<std::endl;
	}    //	通过onAccountInfoChanged接收账户信息info

