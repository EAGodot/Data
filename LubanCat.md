## 记录
1. 在线文档地址
[LubanCat](https://doc.embedfire.com/products/link/zh/latest/linux/ebf_lubancat_doc.html)

2. 账号：root 密码：root，账号：Cat 密码：temppwd
3. SSH登录(USB)参考在线文档，串口登录波特率：1500000
   
4. 遠程桌面
  
    **VNC(Virtual Network Console)是虚拟网络控制台的缩写。 它是一款优秀的远程控制工具软件，由著名的AT&T的欧洲研究实验室开发。**
    
    VNC分为客户端和服务端，我们首先进行鲁班猫上服务端的配置
    
    安装VNC服务
    
    `sudo apt install x11vnc`
    
    创建连接密码
  
    `x11vnc -storepasswd`
  
    使用cat用户创建VNC连接密码，密码默认保存在/home/cat/.vnc/passwd文件中
   
    後續内容實戰后補充上
