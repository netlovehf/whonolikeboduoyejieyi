# 所谓授人以鱼不如授人以渔
## 这里是简短的编译OpenWrt入门秘籍

截至2021.06.07，除了[ImmortalWrt](https://github.com/immortalwrt/immortalwrt)缝合好了几大爬墙插件可供直接make编译，其他的Op分叉都或注释或分离或隐藏了，为了照顾新人定制编译属于自己的固件，故有了这篇高考期间的openwrt小作文...     

### 选择op分叉主体         

从设备支持范围、魔改及新写插件丰富度来看，毫无疑问推荐使用[coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)（最近竟然有openwrt官方成员来[吐槽](https://github.com/coolsnowwolf/lede/issues/6942)不pr到上游,真是太不了解中国大陆环境了...）
此部分[操作说明](https://github.com/coolsnowwolf/lede#readme)已经很详细了            

### 需要手动添加ssrp、passwall、openclash等插件     
这部分开始前先大声对火星来的说“[passwall](https://github.com/xiaorouji/openwrt-passwall)没有删库跑路，只是曾经私有库过一段时间，目前是xiaorouji own并主导开发中”          
此部分操作说明：    
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

### 
