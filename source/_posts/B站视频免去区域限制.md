---
title: B站视频免去区域限制
date: 2021-05-09 12:34:55
top: false
cover: false
password:
toc: true
math:
mermaid:
summary:
tags: 
- bilibili
- 云函数
categories: 技术
index_img: 2021/05/09/B站视频免去区域限制/001_bili_area_limit.png
---

## 前言
如果你身在国外，想观看大陆限定的番剧，或是说你身在内地，却想看港澳台限定的番剧，就会发现B站提示视频不支持在当前区域播放。这是由于B站出于版权方面的问题，会根据用户不同的位置信息提供不同的服务。如果你仍然希望和大家一起边畅聊弹幕边观看番剧的话，可以采用下面的方法绕过B站的区域限制。而这些方法的原理其实很简单，就是通过代理服务器访问观看的番剧页面，从而得到真实可用的视频地址。

{% asset_img 001_bili_area_limit.png 视频找不到了 %}



## 准备工作
### PC端
1. 可以使用油猴插件脚本来更改代理服务器。油猴的下载地址是：[油猴脚本(Chrome)](https://chrome.google.com/webstore/detail/tampermonkey/dhdgffkkebhmkfjojejmpbldmpobfkfo);或者在[油猴官网](https://greasyfork.org/zh-CN)下载其他浏览器版本插件(Safari并不支持)。
2. 安装[解除B站区域限制](https://greasyfork.org/zh-CN/scripts/25718-%E8%A7%A3%E9%99%A4b%E7%AB%99%E5%8C%BA%E5%9F%9F%E9%99%90%E5%88%B6)脚本，如果存在问题，可以在其[github主页](https://github.com/ipcjs/bilibili-helper)寻找解决方案。

### 安卓端
[哔哩漫游](https://github.com/yujincheng08/BiliRoaming)提供了相关功能的Xposed模块，如果你是root用户，且使用过Xposed框架，根据指引安装此模块即可。如果系统并未root，可以使用[太极](https://taichi.cool/zh/)来运行这个模块，具体步骤稍有麻烦，参见两者的介绍即可

## 服务器
由于之前的公用服务器为B站所封锁，所以现在需要自己搭建解析服务器。当然，如果你嫌麻烦，也可以直接购买服务。比如：

1. 加速器或对应地区的代理。这样也就不需要更改解析地址了，直接使用加速器就可以了。
2. [公共解析服务器](https://github.com/yujincheng08/BiliRoaming/wiki/%E5%85%AC%E5%85%B1%E8%A7%A3%E6%9E%90%E6%9C%8D%E5%8A%A1%E5%99%A8)。联系上边的提供者来获取稳定的服务。

如果你不嫌麻烦，就可以[页面](https://github.com/ipcjs/bilibili-helper/blob/user.js/packages/unblock-area-limit/README.md#%E8%87%AA%E5%AE%9A%E4%B9%89%E4%BB%A3%E7%90%86%E6%9C%8D%E5%8A%A1%E5%99%A8)按照所述的方法搭建个人解析服务器。

如果你已经拥有对应地区的服务器，那么直接在服务器上配置反向代理即可；如果你希望在内地观看香港的番剧，可以通过云CDN或者云函数的方式，更为便宜也方便。如果你身在境外，想要观看内地的番剧的话，使用服务器或是云CDN就有一定麻烦了。因为此时需要将域名指向境内服务器或者云CDN境内解析，这都要求备案域名。如果你懒得备案的话，云函数是最简单的实现方案了。具体步骤如下：

1. 注册腾讯云账户，开启serverless里的云函数功能；
2. 新建一个自定义函数，地域选择你需要的地区，环境选择PHP7，或者你也可以自行编写js或是python的程序。
3. 使用 [zzc10086](https://github.com/zzc10086) 提供的[函数](https://github.com/zzc10086/grocery_store/blob/master/bili_proxy/Tencent_SCF_BPplayurl.php)。他也提供了阿里云函数，也可以使用。
4. 触发器选择API网关触发，然后完成即可。
5. 从函数的触发管理中得到访问路径。填写到对应的自定义服务器地址就可以了。

注意，如果你的油猴脚本无法自动弹出设置界面的话，可以在浏览器的 console 里输入
```
bangumi_area_limit_hack.showSettings();
```
来打开配置界面。