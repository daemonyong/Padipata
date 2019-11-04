# Git

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

## GIT 分支

- git branch (分支名) 查看所有分支/新建某个分支
- git checkout 分支名 切换到某个分支
- git merge 分支名 将某个分支合并到当前分支下

## 将本地仓库上传到 GitHub

- SSH
- git remote add origin git@github.com:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/xxx.git
- git push -u origin master

## 创建 GitHub 仓库克隆到本地

- git clone git@github.com:xxxx，克隆仓库

# VSCode

## 插件

- [VSCode 的中文（简体）语言包](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-zh-hans) -> Chinese (Simplified) Language Pack for Visual Studio Code
- [代码运行器](https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner) -> Code Runner
- [翻译](https://marketplace.visualstudio.com/items?itemName=intellsmi.comment-translate) -> Comment Translate
- [Chrome 调试器 ](https://marketplace.visualstudio.com/items?itemName=msjsdiag.debugger-for-chrome) -> Debugger for Chrome
- [简单的 LESS](https://marketplace.visualstudio.com/items?itemName=mrcrowl.easy-less) -> Easy LESS
- [增强内置的 Git 功能](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens) -> GitLens—Git supercharged
- [CSS 支持 HTML](https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css) -> HTML CSS Support
- [jQuery 代码片段](https://marketplace.visualstudio.com/items?itemName=donjayamanne.jquerysnippets) ->jQuery Code Snippets
- [启动实时加载服务器](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) -> Live Server
- [在浏览器中打开](https://marketplace.visualstudio.com/items?itemName=techer.open-in-browser) -> open in browser
- [路径感知](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense) -> Path Intellisense
- [智能代码](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode) -> Visual Studio IntelliCode
- [代码拼写检查](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker) -> Code Spell Checker
- [代码格式化](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) -> Prettier-Code formatter
- [ES6 代码片段](https://marketplace.visualstudio.com/items?itemName=xabikos.JavaScriptSnippets) -> JavaScript (ES6) code snippets
- [即时反馈](https://marketplace.visualstudio.com/items?itemName=WallabyJs.quokka-vscode) -> Quokka.js
- [Vue 工具](https://marketplace.visualstudio.com/items?itemName=octref.vetur) -> Vetur
- [Vue2 代码片段](https://marketplace.visualstudio.com/items?itemName=hollowtree.vue-snippets) -> Vue 2 Snippets
