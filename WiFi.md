# STA #

## 初始化 ##

### 初始化 NVS ###

初始化 NVS ...

### 初始化 LwIP ###

初始化 LwIP 功能，以实现...

### 初始化事件 ###

初始化事件，监测 WiFi 的运行状态。

首先创建一个默认事件循环，然后初始化默认STA，最后将事件处理实例 `WIFI_EVENT`和`IP_EVENT` 注册到默认事件循环中。

### 初始化 WiFi ###

初始化 WiFi ，采取默认配置。

### 配置 WiFi ###

将 WiFi 配置为 STA 模式，同时设置接入点的 SSID 和 PASSWORD 。

### 启动 WiFi ###

启动 WiFi ...

## 事件处理 ##

首先编写事件处理函数 `wifi_event_handler` ，在事件处理函数中对应位置加上事件组标志位更改语句，如： `xEventGroupSetBits()` 用来更改某一位。

然后在初始化函数中使用 `xEventGroupWaitBits()` 等待事件发生，此处的事件发生指的是事件组中需要监测的标志位被置1。
