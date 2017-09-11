# Introduction-to-SSH-Tunnel

## SSH tunnel 
中文可以称为端口转发，是SSH的一项非常重要的功能。它可以建立一条安全的SSH通道，并把任意的TCP连接放到这条通道中。通过建立这条隧道，用户可以从客户端直接访问服务器端基于TCP协议的服务如HTTP。

举个例子如果有一台接入教育网的服务器，同时我们又可以从公网访问之，那么我们可以从无法接入教育网的客户端与服务器端建立SSH Tunnel。这样客户端也可以访问教育网。这个过程分为两个步骤：
1. 建立SSHTunnel
2. 设置本地代理

## Linux/Macos 系统建立SSH Tunnel
在登录终端时输入
```Bash
ssh -D 2080 user@server
```
这样就成功建立了服务器端22端口与本地2080的端口的隧道。本地端口可以任意设置这要不与其他服务冲突即可，根据规则自定义端口号应该设置在1000以上。


## Windows 系统建立SSH Tunnel
Windows操作系统中需要通过客户端建立SSH Tunnel。例如Xshell、Putty。这里以Putty为例

1. 在Session面板中输入Host Name 或 IP Address

![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig1.png)

2. 在左侧边栏SSH/Tunnels面板设置本地端口号和动态转发

![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig2.png)

最后保存配置并连接服务器即可。

## 设置本地代理服务器
这个过程和任何设置代理服务器的方式一样，可以使用IE中默认的代理配置工具，也可以使用各种浏览器的代理工具，这里以Chrome浏览器中SwitchyOmega为例
![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig3.png)
