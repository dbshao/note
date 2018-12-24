Asp.net中需要一些对象来维护程序的相关信息，这些对象就是这篇文章要讲的这些内置对象，而这些内置对象又课分为两类，一类是Request，Response和server对象，主要用来连接服务器和客户端浏览器之间的联系，而Cooikes，Session和application对象则主要用于网站的状态管理。

####一、Request
当用户在客户端使用浏览器向应用程序发出请求时,客户端就会发送一个http请求,而这个请求包含了所查询的字符串参数或表单参数,等信息.在asp[.NET](http://lib.csdn.net/base/dotnet)中就把这些客户端的的请求封装成Request对象。

在使用过程中我们比较常用的是获得用户提交的变量以此来查询.

其中常用的是使用QueryString来得到Get请求发送的数据,而使用Post提交的则由Form来收集.

![request的方法和属性](http://upload-images.jianshu.io/upload_images/66256-2cabd93114d0c170.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####二、Response
与Request相反,response是服务器响应请求后,向客户端发送的数据的封装而成的.

 
其经常使用到的方法有：Write（发送信息给客户端）
                                        Redirect（将客户端重新定位到新的URL）
                                        End （结束该页的执行）

![response的方法和属性](http://upload-images.jianshu.io/upload_images/66256-a0b1740ec10b83d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

####三 .Server
Server对象是用提供了对服务器对象上的方法和属性进行的访问.
常用的属性和方法

![server的对象和属性](http://upload-images.jianshu.io/upload_images/66256-02b78632aa3f2495.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


####四、Cookies
cookies是一种能够让网站服务器把少量数据保存到客户端的硬盘或者内存中。它可以记录用户的ID，密码浏览过的网页，停留时间等信息，当用户再次来到这个网站的时候，可以通过读取Cookies得到用户的相关信息。
Cookies保存的信息片段以“键值”对的形式保存。一个键值对就是一条命名的数据。



![cookies属性和方法](http://upload-images.jianshu.io/upload_images/66256-4e0374786e63d3c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



