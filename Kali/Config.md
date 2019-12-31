# Kali Config

## 更新源

```
- 编辑: /etc/apt/sources.list

#阿里云
deb http://mirrors.aliyun.com/kali kali-rolling main non-free contrib
deb-src http://mirrors.aliyun.com/kali kali-rolling main non-free contrib

#清华大学
deb http://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free
deb-src https://mirrors.tuna.tsinghua.edu.cn/kali kali-rolling main contrib non-free

#中科大
deb http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib
deb-src http://mirrors.ustc.edu.cn/kali kali-rolling main non-free contrib

#东软大学
#deb http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib
#deb-src http://mirrors.neusoft.edu.cn/kali kali-rolling/main non-free contrib

#官方源
#deb http://http.kali.org/kali kali-rolling main non-free contrib
#deb-src http://http.kali.org/kali kali-rolling main non-free contrib
```

## 网络问题

```
service network-manager stop
rm /var/lib/NetworkManager/NetworkManager.state
service network-manager start
```

## 安装

```
apt-get install fcitx fcitx-googlepinyin  #谷歌输入法
apt-get install vsftpd                    #FTP
```

## Firefox

- 汉化

```
1.apt -y install firefox-esr-l10n-zh-cn (下载安装语言包)
2.打开火狐浏览器右上角的菜单，选择''首选项''
3.向下滑动,到达语言栏(language),点击右边的按钮
4.在 Add 左边选择框中找到 zh-cn,点击 Add 添加
5.点击“确定”，重启浏览器
```

- 关闭 detectportal

```
1.在 firefox 地址栏输入：about:config
2.搜索:network.captive-portal-service.enabled
3.双击改为 false
```

## nc,netcat

```
rm /usr/bin/nc
ln -s /usr/bin/nc.traditional /usr/bin/nc
rm /usr/bin/netcat
ln -s /usr/bin/nc.traditional /usr/bin/netcat
```
