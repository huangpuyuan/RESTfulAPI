# RESTful API
>Restful 一种软件架构风格，设计风格而不是标准，只是提供了一组设计原则和约束条件。它主要用于客户端和服务器交互类的软件。基于这个风格设计的软件可以更简洁，更有层次，更易于实现缓存等机制。  
本质是一种软件架构风格 核心是面向资源

* 解决的问题
	* 降低开发的复杂性
	* 提高系统的可伸缩性
* 设计概念和准则
	* 网络上的所有事物都可以被抽象为资源
	* 每一个资源都有唯一的资源标识，对资源的操作不会改变这些标识
	* 所有的操作都是无状态的


#### HTTP协议- URL
>RFC文档 

* URL `schema://host[:port]/path[?query-string][#anchor]`
	* scheme 指定低层使用的协议(http,https,ftp)
	* host 服务器的IP地址或者域名
	* port 服务器端口 默认80
	* path 访问路径
	* query-string 发送给http服务器的数据
	* anchor 锚	
* 请求(request) `请求行、消息报头、请求正文`
	* 请求行 格式 `Method Request-URI HTTP-Version CRLF`  
	例如：`GET/HTTP/1.1 CRLF`
	* 请求方法
		* GET 请求Request-URI所标识的资源
		* POST 在Request-URI所标识的资源后附加新的数据
		* HEAD 请求获取Request-URI所标识的资源的响应消息报头
		* PUT 请求服务器储存一个资源...
		* DELETE 请求服务器删除Request-URI所标识的资源
		* OPTIONS 请求查询服务器的性能，或者查询与资源相关的选项和需求
* 响应(response) `状态行、消息报头、响应正文`
	* 状态行 `HTTP-Version Status-Code Reason-Phrase CRLF`   
	例如 HTTP/1.1 200 OK
	* 常用状态码
		* 200 OK
		* 400 Bad Request 客户端语法错误
		* 401 Unauthorized 收到请求，但是拒绝服务
		* 404 Not Found 资源不存在
		* 500 服务器发生不可预期错误
		* 503 服务器当前不能处理客户端服务

##### RESTful架构与其他 架构区别
* SOAP WebService
* 效率和易用性
* 安全性

### 如何设计RESTful API
> 六大要点 

1. 资源路径(URL)
	* 每个网址代表一种资源，所以网址中不能含有动词，只有名词，一般为负数 
	例如 `https://api.example.com/v1/zoos`
		 `https://api.example.com/v1/animals` 
1. HTTP动词
	* CURD 操作GET/POST/PUT/PATCH/DELETE ...
	* 例子：
		* `POST/zoos` 新建一个动物园
	    * `GET/zoos/ID` 获取一个动物园的信息
		* `PUT/zoos/ID` 更新摸个指定动物园的ID
		* `DELETE/zoos/ID` 删除某个动物园
1. 过滤信息
	* 提供参数进行过滤:
	* 例子：
		* `?offset=10` 指定返回记录的开始位置
		* `?page=2&per_page=100` 指定第几页，以及每页记录数
		* `?sortby=name&order=asc`指定返回结果排序，以及排序顺序
		* `?animal_type_id=1` 指定筛选条件
1. 状态码
	
	>服务器向用户返回的状态码和提示信息，使用标准的HTTP状态码	
	* 200 OK 服务器成功返回用户请求的数据，该操作是幂等的
	* 201 CREATED 新建或修改数据成功
	* 204 NO CONTENT 删除数据成功
	* 400 BAD REQUEST 用户发出的请求有错误
	* 401 Unauthorized 表示用户没有认证，无法进行当前的操作
	* 403 Forbidden 表示用户访问是被禁止的(用户已经提供了认证，但被禁止。比如，权限不足)
	* 422 Unprocessable Entity 当创建一个对象时，发生一个验证错误
	* 500 INTERNAL SERVER ERROR 服务器内部错误 无法判断用户发送请求是否成功

1. 错误处理
	
	>如果状态码大于400，就应该向用户返回错误信息，一般来说将error作为健名
	
	```json
	{
		"error":"错误参数"
	}
	```


1. 返回结果
	* GET/collections: 返回资源对象的列表（数组）
	* GET/collections/identity: 返回单个资源对象
	* POST/collections: 返回新生的资源对象
	






