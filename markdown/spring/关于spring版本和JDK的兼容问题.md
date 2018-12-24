当使用JDK1.8和spring3.2架包时会爆出以下错误：

![
![error](http://upload-images.jianshu.io/upload_images/66256-6b8edbaaf2a0b7d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
](http://upload-images.jianshu.io/upload_images/66256-c07961eb383e2274.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![spring 3.2](http://upload-images.jianshu.io/upload_images/66256-46c7c7227ffca085.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果将JDK改为1.7或者1.6则不会出现此类问题

如果要想使用JDK1.8，只要将spring的架包升级到4.3就可以使用，并且也解决了上述可能会出现的服务器乱码问题


![spring 4.3](http://upload-images.jianshu.io/upload_images/66256-7ec6c896ec9c8c19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
