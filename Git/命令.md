## 配置 Git

- git config --global user.name "Your Name"
- git config --global user.email "email@example.com"

## SSH Keys

- ssh-keygen -t rsa -C "email@example.com" 生成 RSA 公钥和密钥
- 将公钥(id_rsa.pub)上传到 Github 的 SSH Keys 中 (生成时会显示公钥的路径)
- ssh-keyscan -H github.com >> ~/.ssh/known_hosts 将 GitHub 添加到授权主机列表
- ssh -T git@github.com 验证是否成功

## Git 操作

- git init 初始化本地仓库 .git
- git status -sb 显示当前所有文件的状态
- git add 文件路径/.(所有文件) 用来将变动加到暂存区
- git commit -m "信息" 用来正式提交变动，提交至 .git 仓库
- git log/git log --oneline 查看提交的版本信息
- git reflog 查看全部的历史版本信息
- git reset --hard '版本号' 通过版本号回退到某一个版本
- git pull 从 github 上拉取最新的代码
- git push 将代码推送到 github 上

## 将本地仓库上传到 GitHub

- SSH
- git remote add origin git@github.com:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/xxx.git
- git push -u origin master

## 创建 GitHub 仓库克隆到本地

- git clone git@github.com:xxxx，克隆仓库
