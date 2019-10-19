# OS

## Linux

```
cd                      //切换目录                  <-进入前一目录>
ls                      //显示当前目录下内容         <-l详细信息,-a所有文件>
pwd                     //查看当前所处目录
touch file              //创建空文件
mkdir file              //创建空目录                <-p建立多级目录>
rm                      //删除文件或目录             <-f强制删除>
cp a b                  //复制文件或目录             <-a保留链接、文件属性及目录下的所有内容>
mv a b                  //移动文件或目录(还可以重命名)
cat file                //查看文本文件内容
less file               //分页显示文本文件内容,前后翻看
diff a b                //比较两个文件的差异
whereis file            //在资料库中查找
find file               //按条件查询指定文件
grep                    //筛选符合条件的内容
------------------------------------------------------------
su                      //切换用户
sudo                    //以系统管理者身份执行指令
echo                    //打印输出
ifconfig                //显示或设置网络设备
netstat                 //显示网络状态               <-pantu>
useradd name            //添加用户                   <-r系统用户-g指定用户组>
usermod name            //修改用户                   <-u用户UID-g所属分组>
userdel name            //删除用户                   <-r删除相关文件>
reboot                  //重启
-------------------------------------------------------------
管道命令 | 将前面的结果给后面的命令
重定向 > 是覆盖模式，>> 是追加模式
```

## Window

```
whoami                //显示用户名
net user name *       //修改用户密码
net user              //查看存在用户账号
net user name         //查看当前用户信息
net user name password /add                    //创建用户
net localgroup administrators name /add        //提升权限
net user name /delete                          //删除用户
-------------------------------------

```
