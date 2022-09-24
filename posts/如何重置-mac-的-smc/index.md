# 如何重置 Mac 的 SMC




![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437045272-4d2c8ef2-804a-4ed7-bb53-b241152c780c.png?x-oss-process=image/resize,w_960,m_lfit)



MacBookPro 雷电口不可用了不着送修，尝试下一下方法；可以为您省下大几千块钱哟 ~



## 什么是 SMC ？



SMC 全称 系统管理控制器负责管理与以下功能相关的行为：

- 电源，包括电源按钮和 USB 端口的电源
- 电池和充电
- 风扇和其他热能管理功能
- 指示灯或感应器，例如状态指示灯（睡眠状态、电池充电状态等）、突发移动感应器、环境光传感器和键盘背光
- 打开和合上笔记本电脑盖时的行为



------

## SMC 常见问题

由于Mac的雷电接口经常需要插拔外接设备，而外接设备的接口电流电压不一致，Mac在遇到异常电涌时会触发  SMC 的自我保护机制，通常意义是雷电口不可用。



通过重置系统管理控制器 (SMC) 可以解决某些与电源、电池、风扇和其他功能相关的问题。



------



## 注意事项

新款 Apple M1 设备的重置步骤本文不一致，后续会补充更新



------



## 配备 T2 芯片的笔记本电脑

1. 将 Mac 关机
2. 在内建键盘上，按住以下所有按键。Mac 可能会开机。

- - 键盘左侧的 **Control** ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437210613-0f478f9a-1f5b-4b51-8060-6f9af28a4ae0.png?x-oss-process=image/resize,w_960,m_lfit)
  - 键盘左侧的 **Option** (Alt) ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437216356-d0ba8e9e-ebb9-4756-8459-124876d0c332.png?x-oss-process=image/resize,w_960,m_lfit)
  - 键盘右侧的 **Shift** ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437210667-cdfb2059-1d3d-4cb4-bb6c-88e38c1c3054.png?x-oss-process=image/resize,w_960,m_lfit)

1. 按住**全部三个按键** 7 秒钟，然后在不松开按键的情况下按住**电源按钮**。如果 Mac 处于开机状态，它将在您按住这些按键时关机。

![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437286162-81a557b7-7f54-49b2-9ad6-32716f0b8488.png?x-oss-process=image/resize,w_960,m_lfit)

1. 继续按住**全部四个按键** 7 秒钟，然后松开这些按键。
2. 等待几秒钟，然后按下**电源按钮**以将 Mac 开机。



------



## 配备 T2 芯片的台式电脑

1. 将 Mac 关机，然后拔下电源线。
2. 等待 15 秒钟，然后重新接回电源线。
3. 等待 5 秒钟，然后按下**电源按钮**以将 Mac 开机。



------



## 在其他电脑上重置 SMC



如果您的 Mac 没有配备 Apple T2 安全芯片，请按照以下步骤操作。



### 装有不可拆卸电池的笔记本电脑

这类电脑包括 2009 年中至 2017 年推出的 MacBook Pro 机型、2017 年或之前推出的 MacBook Air 机型，以及所有 MacBook 机型，但 MacBook（13 英寸，2009 年中）除外。

1. 将 Mac 关机。
2. 在内建键盘上，按住以下所有按键：

- - 键盘左侧的 **Shift** ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437453096-c4dd55c9-dea8-4ece-810d-d0a6bf880b5a.png?x-oss-process=image/resize,w_960,m_lfit)
  - 键盘左侧的 **Control** ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437452982-7bdab59b-e4d2-4aa0-863d-59d224b081a9.png?x-oss-process=image/resize,w_960,m_lfit)
  - 键盘左侧的 **Option** (Alt) ![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437453069-12f401d8-bfbf-4657-9323-67169460f2fa.png?x-oss-process=image/resize,w_960,m_lfit)

1. 在按住**全部三个按键**的情况下，按住**电源按钮**。


![img](http://ipic-typora-samzong.oss-cn-qingdao.aliyuncs.com//uPic/1617437452835-44611990-1f9b-49c4-a49b-446cef022d56.png?x-oss-process=image/resize,w_960,m_lfit)

1. 按住**全部四个按键** 10 秒钟。
2. 松开所有按键，然后按下**电源按钮**以将 Mac 开机。


### 装有可拆卸电池的笔记本电脑

这类电脑包括 2009 年初或之前推出的所有 MacBook Pro 和 MacBook 机型，以及 MacBook（13 英寸，2009 年中）。 

1. 将 Mac 关机。
2. 拆下电池。
3. 按住**电源按钮** 5 秒钟。
4. 重新安装电池。
5. 按下**电源按钮**以将 Mac 开机。



### 台式电脑

1. 将 Mac 关机，然后拔下电源线。
2. 等待 15 秒钟，然后重新接回电源线。
3. 等待 5 秒钟，然后按下**电源按钮**以将 Mac 开机。
