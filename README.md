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
            
(2)BluetoothDevice类
该类代表了一个远端的蓝牙设备，使用它请求远端蓝牙设备连接或者获取远端蓝牙设备的名称、地址、种类和
绑定状态(其信息封装在BluetoothSocket中)。

                                         BluetoothDevice类中部分
            ----------------------------------------------------------------------------------------
	          | createRfcommSockettoServiceRecord(UUID uuid) | 根据UUID创建并返回一个BluetoothSocket |
	           ---------------------------------------------------------------------------------------
	          | getAddress()                                 | 返回蓝牙设备的物理地址                |
	           ---------------------------------------------------------------------------------------
	          | getBondStatus()                              | 返回远端设备的绑定状态                |
	           ---------------------------------------------------------------------------------------
	          | getName()                                    | 返回远端设备的蓝牙名称                |
	           ---------------------------------------------------------------------------------------
	          | getUuids()                                   | 返回远端设备的UUID                    |
	           ---------------------------------------------------------------------------------------
	          | toString()                                   | 返回代表蓝牙设备的字符串              |
	          ----------------------------------------------------------------------------------------
				   
(3)BluetoothServerSocket类
该类代表打开服务连接来监听可能到来的连接请求(属于server端)，为了连接蓝牙设备必须有一个服务器打开一个
服务套接字。当远端设备发起连接请求时，并且已经连接上时，BluetoothServerSocket类将会返回一个Bluetooth
Socket。

                                     BluetoothServerSocket类中部分方法
          ------------------------------------------------------------------------------------------
          | accept()                 | 直到接收到客户端请求继而建立连接，否则会一直阻塞线程。因而一|
          |                          | 般应放在新线程里运行                                        |
          ------------------------------------------------------------------------------------------
          | accept(int timeout)      | 直到接收到了客户端的请求继而建立连接(或者超时),否则会一直阻 |
          |                          | 塞线程                                                      |
          ------------------------------------------------------------------------------------------
          | close()                  | 关闭Socket,释放所有相关资源                                 |
          ------------------------------------------------------------------------------------------

注：accept方法返回的一个BluetoothSocket，服务器端与客户端的连接最后是两个BluetoothSocket间的连接.

(4) BluetoothSocket类
该类代表客户端，跟BluetoothServerSocket相对。代表一个蓝牙连接套接字的接口(类似于TCP中的套接字)，它是
应用程序通过输入、输出流与其它蓝牙设备通信的连接点。

                                    BluetoothSocket类中部分方法
                                    
          ------------------------------------------------------------------------------------------
          | close()                     | 关闭Socket，释放所有相关资源                             |
          ------------------------------------------------------------------------------------------
          | connect()                   | 允许连接远端设备                                         |
          ------------------------------------------------------------------------------------------
          | getInputStream()            | 获取输入流                                               |
          ------------------------------------------------------------------------------------------
          | getOutputStream()           | 获取输出流                                               |
          ------------------------------------------------------------------------------------------
          | getRemoteDevice()           | 获取跟这个Socket相连的远程设备                           |
          ------------------------------------------------------------------------------------------
          | isConnected()               | 得到Socket连接状态,判断是否连接                          |
          ------------------------------------------------------------------------------------------
          
蓝牙支持point-to-point和multipoint两种连接。利用Android Bluetooth API,可以做到：
1.设置本地和搜索其他蓝牙设备；
2.寻找网内匹配的蓝牙设备；
3.建立RFCOMM通道;
4.通过服务发现建立与其他蓝牙设备的连接;
5.设备之间的数据传输；
6.管理多个连接。

![image](https://github.com/szuhqh/bluetoothBasic/blob/master/images/qrcode_for_gh_134f1744e99c_258.jpg)