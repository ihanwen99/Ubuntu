# Linux ssh

瀚文的Ubuntu学习之路

用这个README文件记录我的Ubuntu配置过程，方便之后重新配置使用



## 190515学习Linux ssh

第一篇文章链接：<https://www.cnblogs.com/ftl1012/p/ssh.html>

### SSH(远程连接工具)连接原理：

ssh服务是一个守护进程(demon)，系统后台监听客户端的连接，ssh服务端的进程名为sshd,负责实时监听客户端的请求(IP 22端口)，包括公共秘钥等交换等信息。

ssh服务端由2部分组成： openssh(提供ssh服务)  、 openssl(提供加密的程序)。

ssh的客户端可以用 XSHELL，Securecrt, Mobaxterm等工具进行连接。

### SSH的工作机制 

服务器启动的时候自己产生一个密钥(768bit公钥)，本地的ssh客户端发送连接请求到ssh服务器，服务器检查连接点客户端发送的数据和IP地址，确认合法后发送密钥(768bits)给客户端，此时客户端将本地私钥(256bit)和服务器的公钥(768bit)结合成密钥对key(1024bit),发回给服务器端，建立连接通过key-pair数据传输。  

### SSH的加密技术

加密技术：传输过程，数据加密。

1.SSH1没有对客户端的秘钥进行校验，很容易被植入恶意代码 。
2.SSH2增加了一个确认联机正确性的Diffe_Hellman机制，每次数据的传输，Server都会检查数据来源的正确性，避免黑客入侵。
 	SSH2支持RSA和DSA密钥 
       	 DSA:digital signature Algorithm  数字签名
        	RSA:既可以数字签名又可以加密  

### SSH知识小结

1.SSH是安全的加密协议，用于远程连接Linux服务器

2.SSH的默认端口是22，安全协议版本是SSH2 

3.SSH服务器端主要包含2个服务功能SSH连接和SFTP服务器   

4.SSH客户端包含ssh连接命令和远程拷贝scp命令等

### 如何防止SSH登录入侵 

1.密钥登录,更改端口

2.牤牛阵法                

3.监听本地内网IP(ListenAddress 192.168.25.*)

