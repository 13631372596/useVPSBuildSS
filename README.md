# 如何使用VPS搭建SS(翻墙)
### 1.首先购买VPS，笔者用的是[Vultr](https://www.vultr.com/)
大家可以尝试使用搬瓦工、DigitalOcean或者其他VPS运营商。注意仅有搬瓦工支持支付宝，其他一律需要使用PayPel(国外的支付宝)绑定VISA或者是信用卡。VPS费用最低一般为5美金一个月，相对国内的阿里云等性价比还是很不错，而且还可以用来搭建SS。

![]("/img/001.png")
选好服务器类型和地区，其他默认即可。随后可看到自己服务器的信息(运行情况、IP地址以及密码)
![]("/img/002.png")

### 2.安装XSHell远程管理服务器
新建会话，主机填写服务器的IP地址，其他默认。然后选择用户身份验证填写服务器的账号和密码。
![]("/img/003.png")
成功后可到看到控制台中显示Connection established(链接已建立)
然后输入命令
	
	注意以下命令仅适用Vultr中版本为CentOS7x64的系统，经尝试Vultr中的CentOS6x64并不适用。Vultr中的Ubuntu16.04也同样不适用，但经测试可通过不同命令搭建成功，详情在最后。

>$ yum install m2crypto python-setuptools
>
>$ easy_install pip
>
>$ pip install shadowsocks
>
>$ vi  /etc/shadowsocks.json

写入配置如下

![]("/img/004.png")

配置防火墙并开启防火墙相应的端口(443为上面设置的端口)
>$ yum install firewalld
>
>$ systemctl start firewalld
>
>$ firewall-cmd --permanent --zone=public --add-port=443/tcp
>
>$ firewall-cmd --reload

启动Shadowsocks，改为“-d stop”可停止
>$ ssserver -c /etc/shadowsocks.json -d start

此时，整个SS已经搭建完毕。上文提及的Ubuntu16.04所有命令如下
>$ apt-get update
>
>$ apt-get install python-pip
>
>$ pip install shadowsocks
>
>$ sudo ssserver -p 443 -k 123456 -m aes-256-cfb --user nobody -d start


###3.下载[影梭客户端](http://www.iyingsuo.com/)进行代理
官网有简单教程，可分别在PC、Android以及IOS上安装，
设置完毕便可以翻墙。此外开发者还能利用该VPS进行其他操作。
![]("/img/005.png")
