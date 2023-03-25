# STA #

## 初始化阶段 ##

### 初始化 NVS ###

初始化 NVS ...

### 初始化 LwIP ###

初始化 LwIP 功能，以实现...

### 初始化事件 ###

初始化事件，监测 WiFi 的运行状态。

首先创建一个默认事件循环，然后初始化默认STA，最后将事件处理实例 `WIFI_EVENT`和`IP_EVENT` 注册到默认事件循环中。

### 初始化 WiFi ###

初始化 WiFi ，采取默认配置。

## 配置阶段 ##

将 WiFi 配置为 STA 模式，同时设置接入点的 SSID 和 PASSWORD 。

## 启动阶段 ##

启动 WiFi ...

## 连接阶段 ##

WiFi 驱动程序会将 `WIFI_EVENT_STA_START` 发布到事件任务，须在事件回调函数中处理 `WIFI_EVENT_STA_START` 事件，可以在此事件下执行 `esp_wifi_connect()` 。

一旦 `esp_wifi_connect()` 被调用，Wi-Fi驱动程序将开始内部扫描/连接过程。

## 获取 IP 阶段 ##

如果内部扫描/连接成功将触发 DHCP 进程，初始化 DHCP 客户端之后，将进入获取 IP 阶段。

如果从 DHCP 服务器成功接收到 IP 地址，则将触发 `IP_EVENT_STA_GOT_IP` 事件，并在事件任务中进行处理。

## 断开阶段 ##

由于各种原因， Wi-Fi 连接失败，会触发 `WIFI_EVENT_STA_DISCONNECTED` 事件并提供失败的原因。

可调用 `esp_wifi_disconnect()` 函数主动断开连接。

## IP 更改阶段 ##

如果 IP 地址发生变化，将触发 `IP_EVENT_STA_GOT_IP` 事件，在该事件中将 `ip_change` 设置为 `true` 。

## 清理阶段 ##

包括 `断开 Wi-Fi 连接` 、 `终止 Wi-Fi 驱动程序` 、 `清理 Wi-Fi 驱动程序` 等。

## 事件处理 ##

首先编写事件处理函数 `wifi_event_handler` ，在事件处理函数中对应位置加上事件组标志位更改语句，如： `xEventGroupSetBits()` 用来更改某一位。

然后在初始化函数中使用 `xEventGroupWaitBits()` 等待事件发生，此处的事件发生指的是事件组中需要监测的标志位被置1。
