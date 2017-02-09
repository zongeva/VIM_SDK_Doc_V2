## 认证

### 获取AuthService

#### 主账号或者仅有一个账号的情况

```java
SDKClient defaultClient = ClientManager.getDefault();
AuthService authService = defaultClient.getAuthService();
```
#### 存在子账号时

首先获取子账号的SDKClient

~~~
SDKClient child = ClientManager.indexByID(account.getID());
~~~

或者获取所有的子账号的SDKClient

~~~
List<SDKClient> allChildClient = ClientManager.getAllChildClient();
~~~

#### 用户类型

AuthService中定义了如下6中用户类型：

| 用户类型 |  取值  |
| :--: | :--: |
| 手机号  |  1   |
|  邮箱  |  3   |
| 豆豆ID |  4   |
| 身份证  |  5   |
| 豆豆账号 |  6   |
| 自定义  |  7   |

当账号为手机号时，需要拼接国家码，例如：0086133********。

### 注册

注册账号分为两步，获取验证码，设置密码（同时传入验证码）。

#### 获取验证码：

传入参数：（用户类型，企业域，账号，ResultCallBack<Integer, Void, Void>）

callBack成功返回 验证码

``` java
authService.getRegCode(byte userType, String server, String account, ResultCallBack<Integer, Void, Void> callBack);
```
#### 设置密码：

传入参数：（验证码，姓名，密码，ResultCallBack）
callBack返回成功表示注册成功，注册完成
```java 
authService.signUp(String regCode, String user, String pwd, final ResultCallBack callBack);
```
### 登录

#### 获取预登录服务器状态

传入参数：（企业域）
直接返回 附加数据json串,如果不为空则表示该企业域可用或者无效

可将校验过的服务器地址存储在本地，离线登录时可以使用本地存储的信息进行校验。

```java 
String result = authService.getPreLogin(String server);
```
#### 手动登录

传入参数：（用户类型，账号，密码，企业域或者IP地址，ResultcallBack<Long, Void, Void>）
callBack返回code=117或者1102需要登录验证码验证
```java 
authService.login(byte userType, String user, String pwd, String server, ResultCallBack<Long, Void, Void> callBack);
```
#### 获取/验证登录验证码

传入参数：（账号，验证码，ResultCallBack<String, Void, Void>）

验证码如果为空字符串则获取下一张验证码图像，否则进行校验。

callback返回验证码图片在本地的存储路径。

```java 
authService.verifyImgCode(String account, String code, ResultCallBack<String, Void, Void> callBack);
```

#### 添加子账号

添加子账号时，需要手动创建一个SDKClient对象来执行登录操作

~~~
SDKClient templeClient = ClientManager.createClient();
AuthService authService = defaultClient.getAuthService();
~~~

### 自动登录

执行自动登录分为两步：判断自否可以自动登录，执行自动登录。

在登录前判断是否可以自动登录,默认所有账号都可以自动登录；

```java 
boolean autoLogin = auth.isAutoLogin();
```
自动登录

传入的参数：（用户ID，企业域，ResultCallBack<Long, Void, Void>）

callback返回成功的第一个参数为 用户ID。

```java 
authService.autoLogin(long userID, String server, ResultCallBack<Long, Void, Void> callBack);
```
### 离线登录

传入的参数：（用户ID，密码，ResultCallBack）

~~~
authService.offlineLogin(long userID, String pwd, ResultCallBack callBack);
~~~

### 取消登录

传入的参数：（当前登录时操作的ID，ResultCallBack）

登录操作ID可在手动登录或者自动登录时获取。

~~~
abortLogin(long operateID, ResultCallBack callBack)
~~~

### 登出

```java 
authService.logout(ResultCallBack callBack);
```
### 获取最近一次登录信息

~~~
LoginInfo lastLoginInfo = authService.getLastLoginInfo();
~~~

### 忘记密码

 忘记密码分为两步，获取验证码， 设置新密码(同时传入验证码)。

#### 获取验证码：

传入参数：（用户类型，企业域，账号，ResultCallBack<Integer, Void, Void>）

账号如果为手机号，需要拼接国家码。

callBack结果返回 1表示错误结果，返回2表示超时。

```java 
authService.getResetPasswordCode(byte userType, String server, String account, ResultCallBack<Integer, Void, Void> callBack);
```
#### 设置密码：

传入参数：（验证码，新密码，ResultCallBack）
callBack返回成功进入下一步
```java 
authService.resetPasswd(String regCode, String pwd, ResultCallBack callBack);
```
### 获取密码规则

```java 
/**
*	接收结果回调 密码规则:
*   高8位代表最小长度
*   低8位，按照最低位开始，依次代表:(1代表必须，0 表示可选)
*   1. 是否必须有数字
*   2. 是否必须有小写字母
*   3. 是否必须有大写字母
*   4. 是否必须有英文字母
*   5. 是否必须有字符(特殊字符)
*   6. 是否允许注册(1允许，0不允许)
*/
authService.getPasswordRule(ResultCallBack<Integer, Void, Void> callBack);
```
### 修改密码（用户在线/登录成功状态下使用）

传入参数：（当前密码，新密码，ResultCallBack）

```java 
authService.changePassword(String oldPw, String newPw, ResultCallBack callBack);
```
### 获取安全中心页面

传入参数:（ 服务器名称，ResultCallBack<String, Void, Void>）

callback返回成功可获取到url。

```java 
authService.getSecUrl(String server, ResultCallBack<String, Void, Void> callBack);
```
### 获取ClientKey

~~~
authService.getClientKey(ResultCallBack<String, Void, Void> callBack);
~~~

### 绑定手机号或者邮箱

#### 绑定手机号：

分为两步，获取注册ID，执行绑定。

获取注册ID

传入的参数：（手机号，语言类型，ResultCallBack<Integer, Long, Void>）

callback返回成功，可获取到 有效时长（单位为秒），注册ID

~~~
authService.getBindPhoneCode(String phone, String language, ResultCallBack<Integer, Long, Void> callBack);
~~~

执行绑定

传入的参数：（手机号，验证码，注册ID，ResultCallBack）

~~~
authService.bindPhone(String phone, String code, long registryID, ResultCallBack callBack);
~~~

#### 绑定邮箱

传入的参数: （邮箱地址，ResultCallBack）

callback返回成功表示已发送确认邮件至指定邮箱。

~~~
authService.bindMail(String mail, ResultCallBack callBack);
~~~

### 监听

数据库更新监听

~~~
authService.observeDBUpdateListener(DBUpdateListener listener);
~~~

版本升级推送

~~~
authService.observeUpgradeListener(UpgradeListener listener);
~~~

