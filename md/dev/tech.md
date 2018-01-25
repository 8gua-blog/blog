# 八卦博客 · 开发者导读
## 主要构成

八卦博客主要由以下几个项目构成

*   前端代码 [https://github.com/8gua-blog/blog](https://github.com/8gua-blog/blog)  
    前端打包发布用了一个单独的仓库 [https://gitee.com/blog-8gua/blog-8gua](https://gitee.com/blog-8gua/blog-8gua)
    
*   命令行 [https://github.com/8gua-blog/8gua-cli](https://github.com/8gua-blog/8gua-cli)
    
*   后端服务器(本机启动) [https://github.com/8gua-blog/8gua-srv](https://github.com/8gua-blog/8gua-srv)
    

## 实现原理

用户在本地启动一个服务进程，然后就可以在浏览器中直接写作。

当用户发布文章时，服务进程能自动推送更新到事前绑定git仓库。

## 技术碎碎念

前端基于coffeescript、scss 、[slm](https://github.com/slm-lang/slm)，构建工具为webpack，轻度使用了vue，重度使用了jquery。

导航基于vue router，github page中通过自定义404页面实现了任意路径访问。只是，微信客户端会把404响应都重定向到寻找失踪小孩，太囧，想避免此问题，只能靠部署到私有服务器。

首页站点标题的中文字体使用了 font-spider来生成，由于github page缓存的原因，通常需要等十分钟才能生效。

文本编辑器基于medium-editor，发布时会通过turndown将html转为markdown，保存在 ./-/md 目录下（[比如，此文档的内容](https://gitee.com/i8gua/i8gua/tree/master/-/md/help)）。

后端基于[fastify](https://github.com/fastify)、[websockets/ws](https://github.com/websockets/ws) 。

更多依赖库参见 [前端的package.json](https://github.com/8gua-blog/blog/blob/master/src/package.json) ，[后端的package.json](https://github.com/8gua-blog/8gua-srv/blob/master/package.json) 。

所有图标都来自 [ICONFONT.CN](http://iconfont.cn/) ，这是神器。

## 小技巧

目录 \- 和 ! ，命令行直接操作(比如 cd -)会保存，请用 cd ./- 即可。

之所以用奇怪的目录，是为了网址的美观。

## 次要组件

#### 跑步健身用的打卡工具

目前还没为插件开发进行完整的架构设计。

但是，如果你只是想写个页面，给自己做个临时的小工具，还是有挺方便的方式。

比如，我为自己写了一个跑步健身用的打卡工具 [https://8gua.blog/timer](https://8gua.blog/timer) 。

[实现代码见这里](https://gitee.com/u8gua/plugin-timer)，插件启用参见 [blog/src/coffee/plugin.coffee](https://gitee.com/u8gua/blog/blob/master/src/coffee/plugin.coffee) ，需要重新打包发版。

#### https证书

[https://github.com/8gua-blog/8gua-blog-ssl](https://github.com/8gua-blog/8gua-blog-ssl)  
safari浏览器ajax请求127.0.0.1时如不使用https， 会被阻断，所以需要一个https证书

## 后续开发

接下来，我第一序列的任务是用户和评论系统，第二序列的任务是适配windows系统。

也有很多小的细节优化可以去做，比如支持图片压缩剪裁、利用service worker加速网站访问、编写linux init.d启动脚本等等。

[任务列表见这里](https://github.com/i8gua/i8gua.github.io/issues?q=is%3Aissue+is%3Aopen+label%3ATODO)，欢迎大家参与并贡献代码。

我的邮箱 [i@8gua.blog](mailto:i@8gua.blog)