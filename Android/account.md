## 账户管理

### 获取AccountService

```java
AccountService accountService = ClientManager.getDefault().getAccountService()
```

### 获取当前登录账户

```java
Account current = accountService.getCurrent()
```
### 获取当前账户ID

```java
long userID = accountService.getUserID();
```
###判断是否为当前账户
```java 
boolean isMyself = accountService.isMyself(long userID);
```

### 获取子账号信息

是否存在子账号

~~~
boolean hasChild = accountService.hasChild();
~~~

获取子账号列表,当前子账号的最大数量为4

~~~
List<Account> childList = accountService.getChild();
~~~

### 监听

网络状态监听

~~~
accountService.observeNetChangeListener(NetChangeListener listener);
~~~

重新登录监听

~~~
accountService.observeReLoginListener(ReLoginListener listener);
~~~

重连监听

~~~
accountService.observeReConnectListener(ReConnectionListener listener);
~~~

子账号新消息监听

~~~
accountService.observeChildNewMsgListener(ChildNewMsgListener listener);
~~~

