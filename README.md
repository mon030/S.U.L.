# S.U.L. - Surfing Under Linspirer MDM 管控设备下网上冲浪指南

------

![Banner](https://s2.loli.net/2023/05/10/iAHPXwoDr5UFVEM.jpg)

### *Version:Pandora*

------



## 说明&许可证:

> **除特别授权外，本文采用[知识共享署名-非商业性使用 4.0 国际许可协议(CC-BY-NC)](https://creativecommons.org/licenses/by/4.0/legalcode.zh-Hans)进行许可**。
>
> 如无法关闭盈利功能，请将从本文获取的报酬捐赠给[UNICEF联合国儿童基金会](https://www.unicef.org/)

本文的测试环境:

Linspirer MDM版本：zijietiaodong_init_5.0.220,

使用设备:华为平板C3

安卓版本:7.0

Author: mon030

©3ON EM - [壁宿K-Labs ](https://hanako.eu.org/#/?id=壁宿k-labs-知识储存库) 2015-2023

------

## 此方案优点:

**1:无需使用数据线连接，只需要能开启个人热点的设备。**

**2:大部分的软件都支持此方案。**

**3:易开启&关闭,可轻易面对管理员的检查，linspirerMDM难以封禁此方案。**

------

## Step1——检查设备环境

首先我们要确认哪些应用支持此方案。

打开设备的文件管理器。

受控设备可以通过`网络设置>高级>安装证书`打开![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYyODAyOTcwXzE2NzA2NjI4MDI5MTk.png)

然后进入下面所给出的目录

```
storage
└── emulated
    └── 0
       └── Tencent
           └── tbs
```

此目录下的文件架名称即为可以使用此方案的应用包名

*如在tbs文件架内找到任何除backup文件架外的文件架,请打开backup文件架。

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYyOTM0NzMzXzE2NzA2NjI5MzQ3MzQ.png)

​      ![img](https://cdn.2zimu.com/CiAgICAgICAgICA1OTU2NS00NDE1Mi1tYmRfZmlsZS0xNjA5ODE4NTkwNDc2LTI3MjAKICAgICAgICA.png)      

## Step2——修改hosts

在锁定所使用的应用后,我们需要获得此应用所连接的域名。

我们可以使用抓包软件获取域名 或通过断网来获取域名

下文所使用的域名为翼◯网学生端 的[应用举报]活动的 *system.eduyun.cn*域名

*必须是以GET方法获取并使用WebView的页面域名!

设置开启网络热点设备的hosts

- *Windows电脑可打开*`*C:/windows/system32/drivers/etc/hosts*`*并添加所获取的hosts*
- *macOS系统需打开Finder,使用组合键*`*Shift+Command+G*`*打开”前往文件夹”，输入框中输入*`*/etc/hosts*`*,然后就会跳转到*`*hosts*`*文件位置。*
- *Linux:* 

```
vim /etc/hosts
```

> *已开启Root权限且解锁system分区的Android系统可前往*`*./system/etc/*`*打开hosts文件架并修改*

> **hosts修改后需重启网络才可生效*

另起一行,添加

```
45.55.142.122   system.eduyun.cn
```

​      ![img](https://cdn.2zimu.com/CiAgICAgICAgICA1OTU2NS00NDE1Mi1tYmRfZmlsZS0xNjA5ODE4NTkwNDc2LTI3MjAKICAgICAgICA.png)      

## Step3——连接&应用

开启热点的方法不再详细说明，如不清楚请自行搜索。

受控设备连接后打开之前访问网页的活动

如进入下面的页面就代表成功

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYzMjg4MDYxXzE2NzA2NjMyODgwNjg.png)



> *失败的原因可能是之前获取的域名错了/应用有进行保护/linspirerMDM开启了域名白名单*

划到网页的最下面,点击`Switchbru Dashboard`

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYzMTUyNjA2XzE2NzA2NjMxNTI2MDk.png)





然后点击`Enter URL`

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYzMzE3MDc1XzE2NzA2NjMzMTcwODM.png)





输入如上图所示的网址`**http://debugx5.qq.com**` (必须是http标头)

点击[信息]菜单，勾选「打开vConsole调试功能」

*如跳转后显示白屏，请重新操作，最后选择跳转至址`**http://debugtbs.qq.co****m**` 

X5内核初始化完整后进入[DebugX5]

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjYzOTc2MzM4XzE2NzA2NjM5NzYzNDY.png)





> *关闭(躲避检查)方法同理,进入x5内核调试页面，关闭vConsole调试功能即可。*

重启应用后即可看到在WebView页面的右下角会有一个vConsole的绿色按钮

在[Log]菜单下的command输入框内输入

```
location.replace("https://example.org")
```

![img](https://cdn.2zimu.com/mbd_file_OTEzMjE0XzM3NTAyM18xNjcwNjY0MjIwNTc5XzE2NzA2NjQyMjA1ODk.jpg)





并点击[OK]执行即可进行网上冲浪🏄

------

## 其他:

如果想交流或有疑问请提交 Issue.

也欢迎pr你的方案。