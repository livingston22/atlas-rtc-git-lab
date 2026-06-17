# Atlas RTC 驱动定位记录

## 目标

本实验需要使用 Git 对 Atlas 开发板上的 RTC 驱动进行修改，因此首先需要在 Atlas 23.0.RC3 SDK 解压后的 Linux kernel 源码中定位 RTC 驱动文件。

## 已执行的定位方式

1. 在 Linux kernel 源码中搜索 drivers/rtc 目录。
2. 使用 rtc_class_ops 搜索 RTC 驱动注册结构。
3. 搜索 CONFIG_RTC_DRV_PL031 判断内核配置。
4. 搜索设备树中的 rtc@、compatible、pl031 字段判断板端实际绑定的 RTC 设备。

## 判断原则

不能随意选择任意 RTC 驱动文件。需要优先选择与 Atlas ARM 平台、设备树 compatible 字段、内核配置项匹配的 RTC 驱动。

如果设备树或内核配置显示使用 PL031，则优先修改：

kernel/drivers/rtc/rtc-pl031.c
