---
title: MacOS 10.15 开启 HiDPI
tags:
  - mac
toc: true
abbrlink: 2389
---

以前手抖买了台 HKC 32 寸 2K 显示器, 接上 MacBook 发现原生的分辨率设置在 2K 显示器上字体很小, 换成 1080P 分辨率显示效果又特别模糊. 上网查了一下发现可以为 MacBook 强行开启 HiDPI. 


  下文的教程结合了 Github 上用户 ZeRo° Xu 在 一键开启 HiDPI 脚本 里的 Github Issue 和一篇博文 《为 Mac 连接的 2k 显示器开启 HiDPI》. 


## 什么是 HiDPI


> 引用自 Github 用户 ZeRo° Xu : 

  它使用横纵 2 个物理像素也就是 4 个物理像素来显示 1 个像素区域, 结果就是图像的--细节得到翻倍, 更清晰, 边缘更平滑--. 拿 13 寸的 MacBook Pro 举例, 它的屏幕物理分辨率是 2560 x 1600, 所以原生的 HiDPI 分辨率就是 1280x800. 更高的一档 1440x900 HiDPI 缩放分辨率, 则是虚拟出一个 2880x1800 的分辨率, 再进行软缩放输入. 所以你能发现苹果的电脑总是有很高的分辨率. 好了, 既然你的屏幕是 1080p, 本身就没有那么多像素去合成 HiDPI, 如果以原生的显示计算, 你这屏幕的 1080p 分辨率应该是 960x540, 这么低的分辨率你是没法用的. 这个脚本的功能就是虚拟出比你的屏幕物理分辨率更高的假分辨率……如果你要开启 1080p 的 HiDPI 分辨率, 就虚拟一个 3840 x 2160 的假分辨率, 然后 macOS 会使用 4 个像素来显示 1 个像素区域, 也就是和你物理分辨率一样的 1080p 分辨率. 

## 自动配置 HiDPI

> 上文 链接 里提到一键配置脚本, 你不妨先按照脚本的步骤开启 HiDPI 试试. 

但是脚本并没有适配所有显示器的情况 (至少我的 Dell P2416D 使用后无效) , 所以就有了下面的步骤. 


## 手动配置 HiDPI

> 本教程测试环境: 


- 笔记本：MacBook Pro (Retina, 15-inch, Mid 2018)
- 显示器：HKC 32寸2K
- 操作系统：MacOS Catalina (Version 10.15.3)

## 0. 安装 RDM

  相信很多人已经装过这个工具了, 它是用来修改显示分辨率的, 如果没装, 请在 RDM 下载页面 安装它. 

## 1. 关闭 macOS 的 SIP

  SIP 全称为「System Integrity Protection」即「系统完整性保护」, 是苹果公司为防止你胡乱篡改系统文件用的保护机制, 请先按照下面步骤把它关闭, 以便后续操作: 

1. 关机（最好先手机拍个照把这 4 步记录下来）
2. 按`command（⌘）+ R+电源键`开机，自动进入恢复模式
3. 选择上边菜单栏的`实用工具`中的`终端`
4. 输入命令`csrutil disable`

  最后终端显示 「Successfully……」 等一大堆文字就说明你成功了. 你可以输入 reboot 重启. 等下文的全部设置都完成后, 你如果想恢复 SIP, 就重复步骤 1 到 3, 在第 4 步输入 csrutil enable 就好了. 

## 2. 开启 macOS 的 HiDPI 选项

  再次重启后进入系统, 打开终端输入

```sh
sudo defaults write /Library/Preferences/com.apple.windowserver.plist DisplayResolutionEnabled -bool true
```

## 3. 查询你的外接显示器的编号

> 这一步相当重要, 先介绍两个命令


```sh
ioreg -l | grep "DisplayVendorID"
ioreg -l | grep "DisplayProductID"
```


  这两条命令用来查询你的显示器供应商 ID DisplayVendorID 和产品 ID DisplayProductID. 接下来你要找到你的显示器对应的 DisplayVendorID 和 DisplayProductID: 


1. 拔掉显示器的 HDMI 或者 DP 线

1. 分别输入上面两个命令之后`return(↩)`，每个命令会返回一个带有数字的结果。那个数字就是 MacBook 默认的`DisplayVendorID`和`DisplayProductID`了

1. 接入显示器

1. 再分别输入那两个命令，每个命令会分别返回两条带有数字的结果。对比刚才 MacBook 默认的结果，另一个数字就是你显示器的`DisplayVendorID`和`DisplayProductID`了

1. 把这两个数字分别转成对应的 16 进制数，用这个 [进制转换工具](https://tool.oschina.net/hexconvert)。


  现在, 回到桌面, 新建一个文件夹命名为 DisplayVendorID-[你刚才查到的 DisplayVendorID 的 16 进制数], 例如 DisplayVendorID-10ac. 


  之后在这个刚建好的文件夹下增加一个文件, 命名为 DisplayProductID-[你刚才查到的 DisplayProductID 的 16 进制数], 例如 DisplayProductID-a0c3. 


### 4. 为你的显示器生成 plist 文件


  到 这个网站 , 在左侧的空里分别输入显示器型号, DisplayProductID 和 DisplayVendorID, 注意填 16 进制的数字, 并且检查下后边 10 进制的数字是不是和你刚才命令查到的一致. 如果需要添加自己额外的分辨率, 直接在下边新建一条分辨率配置就行. 最后, 复制右边生成 XML 格式文本, 粘贴到刚才新建的文件里.  (也可以直接从网站下载文件, 去掉文件名后缀 .plist ) 


![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1606281680751-9a99cf5c-3e0d-4028-af33-ebac7e889ff8.jpeg?x-oss-process=image/resize,w_960,m_lfit)


  XML 文本类似下边这样: 


```sh
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>DisplayProductID</key>
    <integer>41155</integer>
    <key>DisplayVendorID</key>
    <integer>4268</integer>
    <key>scale-resolutions</key>
    <array>
        <data>AAAKAAAABaAAAAABACAAAA==</data>
        <data>AAAFAAAAAtAAAAABACAAAA==</data>
        <data>AAAPAAAACHAAAAABACAAAA==</data>
        <data>AAAHgAAABDgAAAABACAAAA==</data>
        <data>AAAMgAAABwgAAAABACAAAA==</data>
        <data>AAAGQAAAA4QAAAABACAAAA==</data>
        <data>AAAKAgAABaAAAAABACAAAA==</data>
        <data>AAAKrAAABgAAAAABACAAAA==</data>
        <data>AAAFVgAAAwAAAAABACAAAA==</data>
    </array>
</dict>
</plist>
```


### 4. 复制 plist 配置文件到系统配置目录


  这一步就是把刚才新建的配置文件复制到你系统目录里, 你直接复制通常会提示你系统目录是「只读」的, 不允许你胡作非为. 所以你先要在终端执行下面的命令: 


```sh
sudo mount -uw /
```


  这样, 你就可以复制到系统的文件夹了.  (这个命令重启后失效) 


  接下来打开系统文件夹/System/Library/Displays/Contents/Resources/Overrides/, 你会发现一大堆跟你刚才文件夹命名相似的目录. 把你新建的文件夹丢进去, 和它们混在一起, 假装它原来就是其中一员. 重启. 


### 5. 修改分辨率


  重启之后又进入系统, 首先打开 RDM, 你会在菜单栏看见它: 


![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1606281680731-6c912092-1a63-4298-bfbe-54e98f27b67a.jpeg?x-oss-process=image/resize,w_960,m_lfit)


  Main Display 和 Display 2 就分别是你的外接显示器和 MacBook 的显示器分辨率设置 (位置有可能对调, 自己尝试一下) . 带有 ⚡️ 符号的分辨率设置项就是开启 HiDPI 后新增出来的. 如果你像我一样是 24 寸 2K 显示器, 可以给显示器选择 1920x1080⚡️那个配置. 


> 是不是比原生分辨率的 UI 和字体更大更清晰了? 


## 小结

  本文教你强行开启 MacBook 的 HiDPI 设置, 并针对 2K 显示器新增了配置文件到系统配置目录里, 最后用  RDM 自由设置适合你显示器的分辨率. 附带问题

> 用本文的方式开启 HiDPI, 合上 Mac 屏幕, 外接显示器黑屏. 将外接显示器分辨率切换到屏幕原始分辨率后可以正常地仅使用外接显示器, 原因未知. 因对我的工作方式没有影响, 没有继续研究下去. 