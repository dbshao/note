<small>
###Socket通信：
TCP/IP协力底层通性实现原理
又名 套接字
实现服务端与客户端的交互的通信机智
CS架构：
C：Client客户端
S：Server服务器
需要下载安装客户端，通过用户登录链接服务端，从而实现多客户端之间的相互交互过程。如：qq，微星，旺旺……
弊端：客户端太多，客户端的维护与升级太过繁琐
利：交互性特别好

BS结构：
B：Browse
S：Server
应用型的网站
利：只有一个服务端，服务端的维护升级只要一次即可，浏览器端便直接到的页面更新
弊：页面交互性、浏览器兼容性不完美

通过Socket来实现室内聊天室案例
V1：一对一，一个客户端连上一个服务端
V2：一堆多，一个服务端连着多个客户端
V3：多对多，一个服务端，连着多个客户端
a、服务端接受客户端的信息
b、多个客户端之间相互通信（群聊）

V4：功能定制
a、一对一聊天（私聊）
