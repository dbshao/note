这几天接触到的项目是前端和后端分离的，前端使用了angular，原来没有接触过这方面的项目，咋一上手懵逼了，在不修改ajax访问路径的情况下如何实现与后台的交互？前期查到的一些资料作用不大，直到看到了一篇博客《angular2 使用更改默认端口，并配置proxy.config.json进行跨域访问》才解决问题。 
思路就是用angular-cli代理配置来解决跨域请求问题：

1. 创建一个proxy.config.json配置文件
```
    {
      "/****(你所需要拦截的请求)": {
        "target": "http://localhost:8080"(你要进行转发的路径)
      }
    }

2. 在package.json中修改start
    "scripts": {
        "ng": "ng",
        "start": "ng serve --proxy-config proxy.config.json",(修改后)
        "build": "ng build",
        "test": "ng test",
        "lint": "ng lint",
        "e2e": "ng e2e"
    },
```
设置完成后，在IDEA中再次启动angular项目就OK了
--------------------- 
