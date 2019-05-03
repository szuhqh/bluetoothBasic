# bluetoothBasic
简单蓝牙通信示例
蓝牙简介：
蓝牙是一种支持设备短距离通信(一般10米内)的无线数据通信技术，能在包括移动电话、PDA、无线耳机、笔记本电脑、相关外设等众多
设备之间进行无线信息交换。Android平台支持蓝牙网络协议栈，可以实现蓝牙设备之间的无线通信。Android蓝牙开发是从Android 2.0
版本的SDK才开始支持的，而且模拟器不支持，测试需要至少两部手机。

Android蓝牙API分析
Android支持蓝牙开发的类在android.bluetooth包下。编程主要涉及的类简介如下：
(1)BluetoothAdapter类
该类代表一个本地的蓝牙适配器。它是所有蓝牙交互的入口点。利用它可以发现其他蓝牙设备，查询绑定了的设备，使用已知的MAC地址实例
化一个蓝牙设备和建立一个BluetoothServerSocket(作为服务器端)来监听来自其他设备的连接。

                                       BluetoothAdapter类中的部分方法
                                       
            --------------------------------------------------------------------------------
            | cancelDiscovery()                        | 取消当前设备的搜索过程            |
            --------------------------------------------------------------------------------
            | checkBluetoothAddress(String address)    | 检查蓝牙地址字符串的有效性，如 0:43|                        
            |                                          | :A8:23:10:F0，字母必须大写才有效   |
            --------------------------------------------------------------------------------
            |disable()/enable()                        | 关闭/打开本地蓝牙适配器           |
            --------------------------------------------------------------------------------
            |getAddress()                              | 获取默认的BluetoothAdapter        |
            --------------------------------------------------------------------------------
            |getDefaultAdapter()                       | 获取本地蓝牙设备                  |
            --------------------------------------------------------------------------------
            |getName()                                 | 获取本地蓝牙名称                  |
            --------------------------------------------------------------------------------
            |getRemoteDevice(String address)           | 根据特定蓝牙地址获取远程蓝牙设备  |
            |getRemoteDevice(byte [] address)          |                                   |
            --------------------------------------------------------------------------------
            |getState()                                | 获取本地蓝牙适配器当前状态        |
            --------------------------------------------------------------------------------
            |isDisCovering()                           | 判断当前是否正在查找设备          |
            --------------------------------------------------------------------------------
            |isEnabled()                               | 判断蓝牙是否打开                  |
            --------------------------------------------------------------------------------
            |listenUsingRfcommWithServiceRecord(String | 根据名称，UUID创建并返回BluetoothS|
            |name, UUID uuid)                          | erverSocket                       |
            --------------------------------------------------------------------------------
            |startDiscovery()                          | 开始搜索                          |
            --------------------------------------------------------------------------------