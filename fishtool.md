# 授人以鱼不如授人以渔
## 这里是简短的编译OpenWrt入门秘籍

截至2021.06.07，除了[ImmortalWrt](https://github.com/immortalwrt/immortalwrt)缝合好了几大爬墙插件可供直接make编译，其他的Op分叉都或注释或分离或隐藏了，为了照顾新人定制编译属于自己的固件，故有了这篇高考期间的openwrt小作文...     

### 选择op分叉主体         

从设备支持范围、魔改及新写插件丰富度来看，毫无疑问推荐使用[coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)（最近竟然有openwrt官方成员来[吐槽](https://github.com/coolsnowwolf/lede/issues/6942)不pr到上游,真是太不了解中国大陆环境了...）
此部分[操作说明](https://github.com/coolsnowwolf/lede#readme)已经很详细了(git clone 结束后此部分结束)            

### 需要手动添加ssrp、passwall、openclash等插件     
这部分开始前先大声对火星来的说“[passwall](https://github.com/xiaorouji/openwrt-passwall)没有删库跑路，只是曾经私有库过一段时间，目前是xiaorouji own并主导开发中”          
此部分操作说明（保存编辑过的feeds.conf.default后此部分结束）：    
```
#在拉取的op分叉主体的源码的feeds.conf.default文件(lede目录下即可找到)中添加：  
src-git helloworld https://github.com/fw876/helloworld
#这是ssrp插件的最新库地址，只是库名字叫helloworld，包名字其实还是ssrplus这个比，安装好后是界面是shadowsocksR plus +这个比，千变万化我是你爸...
src-git passwall https://github.com/xiaorouji/openwrt-passwall   
#这是passwall插件的最新库地址，库名、包名、菜单名目前统一，之前菜单名是 科学上网、...还有什么名字瞎几把改的我忘了...
src-git OpenClash https://github.com/vernesong/OpenClash
#这是openclash插件的最新库地址
src-git lienol https://github.com/Lienol/openwrt-package
#这是Lienol的package库，里面有一些lede里没有的包
#其他的比如argonv3主题什么的，也都可以按照人家readme文档提示添加进feeds.conf.default文件中
```
![1](https://user-images.githubusercontent.com/73426989/121067460-a7c08f00-c7fd-11eb-86ed-487ef6344690.png)      

### 接下来就可以继续按照[操作说明](https://github.com/coolsnowwolf/lede#readme)中的三步走

```
./scripts/feeds update -a
```
```
./scripts/feeds install -a
```
```
make menuconfig
```

### menuconfig怎么选            
如何选到你的设备，例如R2S、X86_64、ACRH17这些设备怎么选到，请你谷歌一下“xxx openwrt编译”，找几个博客看一下就知道位置在哪了...        
选好设备后，接下来几个你可能刚需的设置点：       

① Target Images > Root filesystem partition size >         
建议软路由玩家设置大些，如果你的硬盘4GB以上，那么root分区大小改为1024MB推荐，硬路由玩家不要改动这里。        

② Extra Packages > autocore、autosamba、automount、ipv6helper         
无论软硬路由都可勾选了，没坏处。         

③ Network > Firewall > ip6tables > ip6tables-extra、ip6tables-mod-nat        
都勾了。         

④ LuCI > Themes >          
一般不建议勾选bootstrap之外的主题，实在想玩花里胡哨，就在前面步骤的手动添加包时找个argon v3的主题放到feeds.conf.default中，然后还要在LuCI > Appliactions中勾选argon_config。     

⑤ LuCI > Applications >         
MTK MIPS架构的几个K2P、新三什么的必选mtwifi否则没无线信号,如果没看到mtwifi选项那就无所谓了，可能大雕调整了mtwifi的位置并且默认选上了，你不用操心了。          
其他的软路由无需操心wifi驱动。            
Docker是很占用编译时间的，嫖Actions的必定不能选Docker，几乎必定超时。         
硬路由一般爬墙插件类只勾选ssrplus : ssr client + xray (xray兼容v2ray、trojan、ss，硬路由勾选ssrp下面这两个就够用了，再多K2P一定超空间出不来固件)       
其他的爬墙插件则不建议为硬路由勾选(注意：别忘记进passwall二层目录里把默认勾选的协议组件取消掉)           
还有一些adbyby plus什么的几把玩意就别为硬路由勾选了,软路由也没必要勾选，去广告本来就不可避免有误伤，道义上也犯贱。![1](https://user-images.githubusercontent.com/73426989/121066548-99be3e80-c7fc-11eb-91a6-bebd60f084d9.png)   
docker想进硬路由的是傻逼。             
软路由就无脑ssrp全勾+passwall全勾+openclash全勾+其他你知道的用过的一些什么各种文件服务器、VPN服务端、qos、TTYD、CPU频率调节、uu加速器、Qbtorrent......眼熟的都可以选，不熟的别选。     

### 编译  
一般都是个人半年编译一次自用，所以什么二次编译、DL预下载，这种情况下都是扯淡，编译完就在op目录下 rm -rf * 全部给扬了，下次编译重新拉源码就行了，费那么多事干嘛，半年编译一次自用，还学个鸡巴二次编译，学会了能涨工资还是能嫖娼不怕抓？![1](https://user-images.githubusercontent.com/73426989/121065702-a42c0880-c7fb-11eb-862e-6498f28eb4d4.png)                     

[我都会了，但是我不想自己编译了,我只需要嫖现成的固件](https://github.com/boduoyejieyi666/whonolikeboduoyejieyi/blob/main/README.md)              

