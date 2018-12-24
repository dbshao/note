**一：创建Web项目**
Step-one:创建Web项目 File->new Project

![](http://upload-images.jianshu.io/upload_images/66256-766faa919581174a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/66256-287c0762365cd06f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/66256-592132c401e2e712.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-two:在WEB-INF目录下创建classes和lib目录 new -> Directory

![](http://upload-images.jianshu.io/upload_images/66256-c640c0e49ce6f348.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-three:进入Project Structure窗口 File->Project Structure

.
Step-four:点击 Modules -> 选中项目“JavaWeb” -> 切换到 Paths 选项卡 -> 勾选 “Use module compile output path”，将 “Output path” 和 “Test output path” 都改为之前创建的classes目录

![](http://upload-images.jianshu.io/upload_images/66256-4e4bd98905a7ccc2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-five:点击 Modules->选中项目“JavaWeb”->切换到 Dependencies 选项卡 -> 点击右边的“+”，选择 “JARs or directories”

![](http://upload-images.jianshu.io/upload_images/66256-fb91e1fac129a45d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Java Web项目是需要依赖 上图的JDK与Tomcat包（Servlet模块就在里面）的

![](http://upload-images.jianshu.io/upload_images/66256-38e19c4c12edc8cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/66256-c321b4af45bc92e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/66256-9d9d3139314ac22e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-six:配置打包方式Artifacts：点击 Artifacts选项卡，IDEA会为该项目自动创建一个名为“JavaWeb:war exploded”的打包方式，表示 打包成war包，并且是文件展开性的，输出路径为当前项目下的 out 文件夹，保持默认即可。另外勾选下“Build on make”，表示编译的时候就打包部署，勾选“Show content of elements”，表示显示详细的内容列表

![](http://upload-images.jianshu.io/upload_images/66256-7f2b1e8dda51f270.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

其它参考详解
[IDEA中的Facets和Artifacts的区别](http://www.php-note.com/article/detail/306)
[Java的打包jar、war、ear包的作用与区别](http://www.php-note.com/article/detail/605)
[IDEA 菜单项中Compile、Make和Build的区别](http://www.php-note.com/article/detail/848)
**二：配置 Tomcat**
Step-seven:进入“Run Configurations”窗口 Run -> Edit Configurations

.
Step-eight:创建一个新的Tomcat容器 点击"+"-> Tomcat Server -> Local

![](http://upload-images.jianshu.io/upload_images/66256-ed572e50ae3973f5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-nine:在"Name"处输入新的服务名，点击“Application server”后面的“Configure...”，弹出Tomcat Server窗口，选择本地安装的Tomcat目录 -> OK

![](http://upload-images.jianshu.io/upload_images/66256-54690792f110c070.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-ten:在“Run Configurations”窗口的“Server”选项板中，去掉勾选“After launch”，设置“HTTP port”和“JMX port”，点击 Apply -> OK

![](http://upload-images.jianshu.io/upload_images/66256-65f5e18eb6486495.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**三：在 Tomcat中部署并运行项目**
Step-eleven:Run->Edit Configurations，进入“Run Configurations”窗口，选择之前配置好的Tomcat，点击“Deployment”选项卡，点击“+”->“Artifact”-> 选择创建的web项目的Artifact

![](http://upload-images.jianshu.io/upload_images/66256-53656a898e8a5936.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-twelve:修改“Application context”-> Apply -> OK

![](http://upload-images.jianshu.io/upload_images/66256-c380d56d38915285.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-thirteen:运行Tomcat，在浏览器中查看运行结果

![](http://upload-images.jianshu.io/upload_images/66256-f4f72d0a40745860.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Step-fourteen:浏览器测试http//：localhost:8080/javaWeb/

![](http://upload-images.jianshu.io/upload_images/66256-5e44605f24280ba7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

文／Alic灿（简书作者）原文链接：http://www.jianshu.com/p/30c09befc364著作权归作者所有


> 解决tomcat在mac 运行时的权限问题 
chmod 777 tomcat路径/*.sh
