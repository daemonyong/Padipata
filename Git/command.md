#配置Git
* git config --global user.name "Your Name"
* git config --global user.email "email@example.com"
#使用Git创建版本库
* git init，初始化本地仓库 .git
* git status -sb，显示当前所有文件的状态
* git add 文件路径，用来将变动加到暂存区
* git commit -m "信息"，用来正式提交变动，提交至 .git 仓库
#将本地仓库上传到GitHub
* SSH
* git remote add origin git@github.com:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/xxx.git
* git push -u origin master
#创建GitHub仓库克隆到本地
* git clone git@github.com:xxxx，克隆仓库
