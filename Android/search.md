##搜索
```java
SearchService searchService = ClientManager.getDefault().getSearchService();
```
###从网络进行查找
* @param key      关键字
* @param callBack 搜索结果
```java
searchService.searchFromNet(String key, ResultCallBack<SearchResult, Void, Void> callBack)
```
###从本地数据库进行查找
* @param key      关键字
* @param callBack 搜索结果
```java
searchService.searchFromNet(String key, ResultCallBack<SearchResult, Void, Void> callBack)
```
###从本地数据库进行查找
```java
searchService.searchFromNet(String key, ResultCallBack<SearchResult, Void, Void> callBack)
```
###全局查找消息
* @param key         查找关键字
* @param msgProperty 查找的附加属性
* @param callBack    消息搜索结果集合
```java
searchService.searchMessage(String key, MsgSearchProperty msgProperty,
                              ResultCallBack<MsgSearchResult, Void, Void> callBack)
```
###查找相应targetID的详细消息
* @param key               查找关键字
* @param msgDetailProperty 查找的附加属性
* @param callBack          消息搜索结果集合
```java
searchService.searchDetailMessage(String key, MsgDetailSearchProperty msgDetailProperty,
                                    ResultCallBack<MsgDetailSearchResult, Void, Void> callBack)
```
