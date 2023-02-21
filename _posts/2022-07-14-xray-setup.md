---
title: "Xray Set-up"
date:   2022-07-14 22:23:18 +0800
categories: 
  - Network
tag:
  - set-up
---

> 2023/01/05: [[一键安装Xray服务器教程2023]使用国外VPS搭建 Xray/VLESS+XTLS 模式服务器及配置Xray客户端实现科学上网](https://iyideng.net/black-technology/cgfw/xray-xtls-one-click-script-building-and-using-tutorial.html) `bash <(curl -Ls https://raw.githubusercontent.com/atrandys/xray/main/install_triple_config.sh)`   


> 实践时间：2021/11/02 - 2021/11/04
>
> 参考相关博客使用Xray实现了科学上网。具体步骤如下：
>
> 1. PayPal国内账户的设置——用于购买
> 2. 购买了国外VPS（Virtual Private Server）
> 3. 购买了伪装域名，进行了DNS解析
> 4. 服务器端设置：在VPS上安装Xray
> 5. 客户端设置：Mac和iOS系统的Xray客户端配置
>
> 参考的主线博客: [Xray一键脚本 - V2ray XTLS黑科技 (v2xtls.org)](https://v2xtls.org/xray一键脚本/)
>
> 本文作为个人记录和个人遇到的问题的补充，仅供参考。个人使用主力设备为Mac，相关博客中也有相关Linux、Windows、安卓等系统等设置。

## PayPal

一个国区PayPal的账号，绑定的都是国内的真实信息（还上传了身份证照）。

添加了一张银联的招商银行借记卡，作为付款账户。

## 国外VPS

购买一个国外的服务器（这个说法可能不太准确）。主要参考文章：[稳定靠谱的国内/国外便宜VPS云服务器商家整理与推荐 - VPS GO](https://www.vpsgo.com/vps-tuijian.html) ｜ [一些VPS商家整理 - tlanyan](https://tlanyan.pp.ua/vps-merchant-collection/) 

仔细比较之后，~~贫穷的~~我选择了 Vultr (此时有绑定PayPal送100刀优惠，不过显示2021-11-18过期，有点慌，到时候再看看)。主要参考文章：[购买vultr服务器超详细图文教程 - V2ray XTLS黑科技 (v2xtls.org)](https://v2xtls.org/购买vultr服务器超详细图文教程/)

购买之后，可以用ssh连接这个服务器。可供参考文章：[Mac电脑连接Linux教程 - V2ray XTLS黑科技 (v2xtls.org)](https://v2xtls.org/mac电脑连接linux教程/)

## 伪装域名

这个步骤其实可有可无，在安装V2ray（对，一开始打算是安装V2ray，而不是Xray）时，发现了伪装域名这个功能。出于之前作为伸手党搭乘其他科学上网路径挂了无数次经历的恐惧，~~对抗懒惰本能~~进行了伪装域名功能的研究和实践。

1. 参考[适合国人的域名注册商推荐 - tlanyan](https://tlanyan.pp.ua/domain-register-for-mainland/)，从NameCheap上购买了一个域名。选择时要注意第一年付和后续价格：![NameCheap价格示例](https://z3.ax1x.com/2021/11/05/InJq4x.png) 
2. 在NameCheap网站之间对域名进行DNS解析，参考文章：[How do I set up host records for a domain? - Domains - Namecheap.com](https://www.namecheap.com/support/knowledgebase/article.aspx/434/2237/how-do-i-set-up-host-records-for-a-domain/)。域名解析记录需要同步到全球的DNS服务器，所以需要一天时间。是否解析完成可以通过命令行输入`nslookup 域名`进行检验，如果返回出现对应服务器IP地址，即解析完成。

> 注意，NameCheap购买后，需要在期限内进行邮箱验证：![邮箱验证](https://s1.ax1x.com/2022/07/11/jcCPHO.png)

## 安装Xray

ssh连接服务器，命令行输入：

```C++
bash <(curl -sL https://s.hijk.art/xray.sh)
```

回车，安装：

![安装选项](https://z3.ax1x.com/2021/11/05/Inr4BV.png)

阅读主线博客后，决定安装VLESS+TCP+XTLS的方式。然后是输入伪装的网站域名等一系列选项。

> 根据博客，脚本默认会申请域名证书，证书存放在和xray配置文件同一个文件夹内（即`/usr/local/etc/xray`目录下）

安装成功之后，可以直接访问伪装域名，如果安装成功，伪装的网站可以正常使用。![伪装网站](https://z3.ax1x.com/2021/11/05/In6lmq.png)

## Mac和iOS系统的客户端设置

Mac客户端设置参考这篇文章[V2Ray mac客户端下载 - V2ray XTLS黑科技 (v2xtls.org)](https://v2xtls.org/v2ray-mac客户端下载/)，因为行文时只有Qv2ray支持VLESS，所以下载了Qv2ray。

配置参考了这篇文章：[苹果MacOS电脑使用Qv2ray客户端上国外网站的方法 – 黑玫瑰 (iyuantiao.me)](https://iyuantiao.me/qv2ray.html)。值得补充的是：V2Ray内核一般放在`/Users/用户名/Library/Preferences/qv2ray/vcore/`下，在设置里V2Ray核心可执行文件路径指定vray，V2Ray资源路径指定这个文件夹。 ![Qv2ray设置](https://z3.ax1x.com/2021/11/05/IncEuR.png)

设置后检查V2Ray核心设置没问题后，就可以添加节点了。根据Xray安装之后给出的信息填写对应。这里奇怪的一点是，TLS设置里选择XTLS无效，选择TLS才可以。

iOS系统里，因为此时只有Shadowrocket支持VLESS，所以又用美区AppleID花了2.99刀购买了APP。添加节点根据对应信息填写就可以。

> 其他[V2Ray客户端配置](https://v2xtls.org/v2ray%e5%ae%a2%e6%88%b7%e7%ab%af/)

---

## 总结

1. 以上，服务器10刀（66.33¥）+域名1.98刀（12.13¥）+Shadowrocket2.99刀（淘宝礼品卡充值），目前支出大概100¥。但是不知道Vultr赠送的100刀啥时候过期，过期就每月5刀，也就是每年60刀，加上域名每年33¥续费，每年大概400元~~qaq它好贵我好穷~~。如果赠送过期还是买现成的服务吧，风险+花费+折腾考虑。
2. ssl证书这个东西好像是XTLS自动设置了，这块一直不太懂，需要补一下加密、HTTPS模块了
3. 感谢一键安装，小白不懂原理，还好应用没出啥bug~~fornow~~

---

### 附录

> [Reference] BashXray.txt



