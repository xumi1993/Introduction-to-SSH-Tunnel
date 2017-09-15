# SSH 隧道与端口转发

## SSH tunnel 
中文可以称为SSH隧道，是SSH的一项非常重要的功能。它可以建立一条安全的SSH通道，并把任意的TCP连接放到这条通道中。通过建立这条隧道，用户可以从客户端直接访问服务器端基于TCP协议的服务如HTTP。

举个例子如果有一台接入教育网的服务器，同时我们又可以从公网访问之，那么我们可以从无法接入教育网的客户端与服务器端建立SSH Tunnel。这样客户端也可以访问教育网。这个过程分为两个步骤：
1. 建立SSHTunnel
2. 设置本地代理

### Linux/Macos 系统建立SSH Tunnel
在登录终端时输入
```Bash
ssh -D 2080 user@server
```
这样就成功建立了服务器端22端口与本地2080的端口的隧道。本地端口可以任意设置这要不与其他服务冲突即可，根据规则自定义端口号应该设置在1000以上。


### Windows 系统建立SSH Tunnel
Windows操作系统中需要通过客户端建立SSH Tunnel。例如Xshell、Putty。这里以Putty为例

1. 在Session面板中输入Host Name 或 IP Address

![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig1.png)

2. 在左侧边栏SSH/Tunnels面板设置本地端口号和动态转发

![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig2.png)

最后保存配置并连接服务器即可。

### 设置本地代理服务器
这个过程和任何设置代理服务器的方式一样，可以使用IE中默认的代理配置工具，也可以使用各种浏览器的代理工具，这里以Chrome浏览器中SwitchyOmega为例
![](https://github.com/xumi1993/Introduction-to-SSH-Tunnel/blob/master/images/fig3.png)

## 通过中间服务器远程连接内网服务器
刚才我们介绍了如何将服务器端口转发到本地。现在设置这样一个场景：
- 有两台服务器 Server1 和 Server 2; 一台客户端PC Client
- Server 1 可以连局域网和公网，Server 2只能连局域网，Client 只能连公网
- 我们想通过Client远程登录Server 2
在这样的场景下我们该如何去做呢，原理上是这样的：我们可以将Server 2的22端口通过Server 1映射到本地的一个自定义端口，然后SSH登录本机的这个端口即可。具体步骤如下
### 1. 创建端口转发
这里以Linux/Macos系统为例
```bash
ssh -N -f -L 127.0.0.1:1022:server2:22 user1@server1
```
- -N 表示该命令不执行远程命令
- -f 表示该命令在后台运行
- -L 表示设置端口转发， `127.0.0.1:1022`为本地的目标端口，`server2:22`表示将转发局域网内服务器的22号端口

### 2. 从本地端口登录局域网服务器
这时在新的终端中从本地的1022号端口登录即可
```
ssh user2@127.0.0.1 -p 1022
```
注意这里的`user2`是`server2`中的用户名而不是本机的
