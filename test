# 物联网平台开发设计文档v1.0

---
### 1. 网站开发设计 


 1. 按照axure开发页面ui布局；
 2. 整理相应素材整合至页面；
 3. markdown编写开发手册整合至网站

------

### 2.平台概要开发设计 #


 1. 按照axure设计开发页面ui布局和样式；
 2. 后端提供相应数据接口；

 
 #### (1). 用户概要信息接口:
>`GET /dashboard/statistics`
 入参:无
 出参:
 管理员返回：
`{"userNumber":90,
"appNumber":90,
"deviceNumber"::90}`
 普通用户返回：
`{"appNumber":90,"deviceNumber":90}`


 #### (2). 应用列表接口：
>`GET /dashboard/apps`
 入参: page 分页参数对象
 出参:
`  {"appName":"appName",
     "protocol":"protocol",
     "createTime":"2018-10-23 11:11:11",
     "deviceNumber":3,
     "secretNumber":5}
`


------------------------------

### 3. 设备调试tcp协议开发设计
 1. tcp调试页面通过websocket连接平台tcp调试服务，接收和发送与设备通讯的消息内容；
 2. 平台提供tcp调试服务，对接页面的ws连接；
 3. 调试页面发送消息至设备，调试服务检测该设备是否在线，在线直接发送，不在线返回页面 相应提示；
 4. 设备发出的B类消息，在转发activeMq之后，通过检测是否存在该设备调试页面ws存在，若存在通过ws连接推送给调试页面

    
> `ws://111.47.243.211:8090/emc-ws/{deviceId}`
    服务推送数据到客户端
`  {"event":"deviceMsg",
     "deviceId":"tcp_device_001",
     "timestamp":"1347343217",
     "data":"
		{'payload':'device send message to apply','deviceId':'tcp_device_001','appId':'app_Tcp'}
	 "}
`
 
---

### 4. 设备调试udp协议开发设计



 1. udp调试页面通过websocket连接平台udp调试服务，接收和发送与设备通讯的消息内容
 2. 平台提供udp调试服务，对接页面的ws连接
 3. 调试页面发送消息至设备，调试服务检测该设备是否在线，在线直接发送，不在线返回页面 相应提示
 4. 设备发出的B类消息，在转发activeMq之后，通过检测是否存在该设备调试页面ws存在，若存在通过ws连接推送给调试页面
   

   > `ws://111.47.243.211:8090/emc-ws/{deviceId}`
    服务推送数据到客户端
`  {"event":"deviceMsg",
     "deviceId":"tcp_device_001",
     "timestamp":"1347343217",
     "data":"
		{'payload':'device send message to apply','deviceId':'tcp_device_001','appId':'app_Tcp'}
	 "}
`
   
---


### 5. 设备详情展示页面开发设计



 1. 设备管理画面增加“详情”按钮，显示该设备连接不同协议的必要字段信息;
 2. 后端提供相应接口；
 3. 设备详情显示字段如下：
 
>  * mqtt:clientId、设备密钥、mqtt中间件地址，设备订阅地址，
>  * tcp:ip、端口、设备密钥
>  * udp:ip、端口、设备密钥
>  * 显示设备在线状态（mqtt,tcp）、最后一次通讯时间(udp,coap)
>  * 点击“消息记录”跳转该设备消息记录 

	### 接口设计
	`GET  /device/details
	
	入参： Serializable id 设备id
	出参：
	- mqtt :{"clientId":"124243234234",
			"password":"kjdjfjsfkusjdkfhdsfd",
			"mqtt连接地址":"tcp://111.47.243.211:1884",
			"订阅单发topic":"appid/deviceId/update",
			"订阅群发topic":"appid",
			"发布topic":"appid/deviceId/get",
			"onLine":true|false
			}
			
	- tcp :{"ip":"111.47.243.211",
			"port":"8765",
			"lastMessageTime":"2018-10-30 11:11:11"
			}
	- coap :{"获取token资源":"coap://111.47.243.211:5683/accessToken",
			"发送消息资源":"coap://111.47.243.211:5683/message",
			"lastMessageTime":"2018-10-30 11:11:11"
			}
	
  
 ---


### 6. 设备监控页面开发设计(**暂定**)


 1. 初始化查询展示所有设备的当前时刻状态(`在线/离线`);
 2. 动态更新能实时监控状态变化的设备(主要是mqtt,tcp)
 
 ### tcp设备动态上下线:上线online,下线offline
>`ws://111.47.243.211:8090/emc-ws/device_online_offline`
  服务推送数据到客户端 
`  {"event":"online/offline",//online上线，offline下线
     "deviceId":"tcp_device_001",
     "timestamp":"1347343217",
     "data":"device online"}
`
 
