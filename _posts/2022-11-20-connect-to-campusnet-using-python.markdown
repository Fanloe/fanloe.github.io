---
title: "Python脚本自动重连校园网"
date:   2022-11-20 08:23:60 +0800
categories: 
  - Network
tag:
---
### 参考
> [自动登录校园网脚本(Python实现)](https://zhuanlan.zhihu.com/p/370801224)  
> [校园网掉线自动重连小助手--Python](https://blog.csdn.net/qq_48551625/article/details/111408883)  
> [安装pyinstaller](https://blog.csdn.net/qq_49349528/article/details/121929161)  

## 版本一：登陆校园网
参考链接一：`response = requests.post(url, data, headers=header).status_code  # POST 方式向 URL 发送表单，同时获取状态码`  
## 版本二：定时检测网络状态，断网重连
参考链接二：python类  
用pyinstaller生成.exe文件运行（在pycharm中运行熄屏程序中止）  
