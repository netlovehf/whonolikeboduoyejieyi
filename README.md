![1](https://user-images.githubusercontent.com/73426989/121419280-5e5b7580-c99e-11eb-8a32-57956bf0572f.png)
# OpenWrt中国大陆分叉圈       

* 本仓库的博客页面(被墙中)：[链接](https://boduoyejieyi666.github.io/whonolikeboduoyejieyi/)            
* 请有恩山账号的老手留言顶下这个 [帖子](https://www.right.com.cn/forum/thread-4053643-1-1.html) ：越过长城，走向世界！            
* 提醒：以下链接需要翻墙访问，且最好有telegram（电报）账号登录telegram客户端           
* [telegram客户端下载](https://telegram.org/apps)           
* [telegram汉化简体(推荐第三方)](https://t.me/setlanguage/classic-zh)     
* [telegram汉化简体(官方测试版本)](https://t.me/setlanguage/zh-hans-raw)      
* [telegram汉化繁体(官方测试版本)](https://t.me/setlanguage/zh-hant-raw)    
* [单线程测速](http://speed.cloudflare.com)   
* [ping检测](http://ping.chinaz.com)             
* [查询IP地址](http://www.ip111.cn)     
* [几种加密算法下传输速度测试脚本](https://github.com/boduoyejieyi666/whonolikeboduoyejieyi/blob/main/sh/ss_test.md)             
* [OpenWrt编译入门秘籍](https://github.com/boduoyejieyi666/whonolikeboduoyejieyi/blob/main/fishtool.md)           
* [GitHub各项服务状态](https://www.githubstatus.com)     
* [主流网站的可用状态](https://downdetector.com)        
* passwall芝麻开门命令：     
```
touch /etc/config/passwall_show        
```
       

———————————————————       
## 缝合怪矮小少AXS软路由专区(目前长期分发固件的设备型号：* x86_64 * 树莓派4B * R1SH5 * R1PLUS * R2S * R4S)
矮小少AXS：缝合了ssrp+passwall+openclash+其他杂交品种翻墙插件+铁头娃们写的一些经常失效的违反非恶法的盗版及破解插件           

* [矮小少AXS软路由固件分发地址](https://github.com/boduoyejieyi666/immortalWrt/releases)         
* [矮小少AXS软路由固件电报同步分发频道](https://t.me/aixiaoshao)         
    
———————————————————      
## 垃圾佬刚刚好GGH硬路由专区(目前长期分发固件的设备型号：* ACRH17 * 竞斗云2.0P2W * K2P * AC2100 * 新三D2)
刚刚好GGH：独宠ssrp        

* [刚刚好GGH硬路由固件分发地址](https://github.com/boduoyejieyi666/immortalWrt/releases)             
* [刚刚好GGH硬路由固件电报同步分发频道](https://t.me/joinchat/KemVTSG0XyEwMjVl)            
           
———————————————————      
## x86_64原生态专区     
下面三大频道的固件编译自各个爬墙插件作者原生适配自己爬墙插件的op源码分叉，避免了杂交爬墙插件和op源码分叉可能导致的bug，最大限度发挥各个爬墙插件作者的本来意图，保证你反馈的bug各个爬墙插件作者最大可能复现并解决！       
.7z文件用 [压缩软件](https://cn.bandisoft.com/bandizip/) 解压后，里面一个是非EFI引导（BIOS引导）的固件、一个是EFI引导的固件，.img.gz可以进一步解压到.img文件（需不需要进一步解压根据实际情况而定）         

### 推荐小白及不爱折腾用户使用。多插件版本采用 [ssrp](https://github.com/fw876/helloworld) 所属 [原生OpenWrt分叉](https://github.com/coolsnowwolf/lede)       
ssrp_TIPS：目前分流只有一个netflix，且无法手动添加更多分流规则。      

* [x86_64 ssrpOpenWrt软路由固件半官方频道](https://t.me/ssrpOpenWRT)      
或      
* [x86_64 ssrpOpenWrt半官方软路由固件GitHub同步分发地址](https://github.com/boduoyejieyi666/ssrpOpenWRT/releases)      

### 推荐喜爱自定义更多用户使用。多插件版本采用 [passwall](https://github.com/xiaorouji/openwrt-passwall) 所属 [原生OpenWrt分叉](https://github.com/Lienol/openwrt) 
passwall_TIPS：自带分流覆盖netflix、telegram等，已经满足大部分人需求，且可以手动导入新的分流规则，可以说是能够完全满足所有分流人群的需求。所以passwall是最佳推荐翻墙插件。   

* [x86_64 passwallOpenWrt软路由固件半官方频道](https://t.me/passwallOpenWRT233)      
或      
* [x86_64 passwallOpenWrt半官方软路由固件GitHub同步分发地址](https://github.com/boduoyejieyi666/passwallOpenWRT/releases)           

————————————————————        
## 入门教程区        

* [总频道](https://t.me/OpenWRTcn)（教程/导航）      
* [VPS/虚拟专用服务器/小鸡](https://github.com/boduoyejieyi666/whonolikeboduoyejieyi/blob/main/MyFanFan.md)       
* [机场/梯子/广义VPN](./youlian/jichang.md)            

————————————————————        
## 其他推荐         
* [ssrp及其他主流插件的ipk文件分发](https://t.me/ssrpIPKnb)      
* [passwall及其他主流插件的ipk文件分发](https://t.me/passwallIPKnb)      
* [Lean的官方ssrpOpenWrt编译Actions](https://github.com/coolsnowwolf/lede/actions) (测试源码编译通过性目的)              
* [Lean的稳定版OpenWrt分叉](https://github.com/coolsnowwolf/openwrt)              
* [Hyird倾情打造源安装插件OpenWrt固件](./youlian/Hyird1.md)               
* [专注Pi/派固件](./youlian/Pi.md)        
* [ssrp开发者Lean的电报群](https://t.me/joinchat/JhKgAA6Hx1uiihA7RaTW1w)          
* [Lean人雕语频道](https://t.me/LeanSaidWTF) （Lean官方消息/Lean发布源码更新通知......）               
* [Lean@全体成员频道](https://t.me/LeanAtYou) （Lean权威发布潘多拉/OpenWrt固件、Lean魔改ESXI/BIOS/Windows/MacOS、破解、游戏......）       
* [小报频道](https://t.me/FQnews) （数码资讯搬运、群友日常吐槽）         
* [passwall初代开发者Lienol的电报群](https://t.me/openwrtcs) (Lienol目前已经不参与passwall开发。passwall由xiaorouji接手开发中)                
* [openclash开发者vernesong主要出没群](https://t.me/ctcgfw_openwrt_discuss)     
* [天灵的频道](https://t.me/nanopi_r2s)                             
* [奈菲影视](https://www.nfmovies.com/)      
* [东东油管频道](https://www.youtube.com/c/BIGdongdong/videos)        
* [老毛子Padavan固件发布](https://t.me/pdcn1)           
* [AX3600固件源码](https://github.com/robimarko/openwrt/tree/AX3600-5.10-restart)              
* [ImmortalWrt官方发行地址](https://firmware.download.immortalwrt.eu.org/)       

————————————————————    
![1](https://user-images.githubusercontent.com/73426989/121643642-9f4daa00-cac4-11eb-88dc-c07ecbee6bf3.png)

## about
本页面打理目前由 [总裁助理](https://t.me/AudreyHB1314) 负责，有事请联系它(仅限于友链等正事。其他的BUG反馈什么的请在发布的固件说明里找到对应issues去反馈)      
