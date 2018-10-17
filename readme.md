# Toolkits

常用命令,工具使用方式的集合

<!-- TOC -->

- [Toolkits](#toolkits)
    - [GenSSHKey](#gensshkey)
    - [Git HTTP2SSH](#git-http2ssh)
    - [Git Submodule](#git-submodule)
    - [Keep Fork Up To Date](#keep-fork-up-to-date)
    - [Scp File Transfer](#scp-file-transfer)
    - [加速pip](#加速pip)
    - [安装virtualenv](#安装virtualenv)
        - [Mac && Linux](#mac--linux)
        - [Windows](#windows)
    - [使用virtualenv](#使用virtualenv)
    - [为windows增加alias](#为windows增加alias)

<!-- /TOC -->

## GenSSHKey

一键生成各个端的sshkey

```bash
# gen key in win && linux && mac
ssh-keygen -t rsa -C "1619249966@qq.com"
# get key in window
cat C:\Users\dongn\.ssh\id_rsa.pub
# get key in linux && mac
cat /home/niudong/.ssh/id_rsa.pub
```

## Git HTTP2SSH

将git仓库中的上传方式从http转成ssh

```bash
# change .git/config
url = http://xxx.com/Name/project.git 
-> url = git@xxx.com/Name/project.git
```

## Git Submodule

git子仓库操作

```bash
# load submodule
git clone <仓库地址> --recursive  # 1. 递归的方式克隆整个项目
git submodule update --init --recursive  # 2. 正常拉取后,初始化子仓库并更新
# add submodule
git submodule add <仓库地址> <本地路径>
# delete submodule
rm -rf the_submodule
rm -rf .git/modules/<submodule_name>
```

## Keep Fork Up To Date

让fork up的仓库更新到源仓库的最新状态

```bash
# must in local fork dir
git remote add upstream <原版仓库地址>  # 与原版仓库关联
git pull upstream master  # 从原版仓库更新
git push origin master  # 向自己fork up的远程仓库更新
```

## Scp File Transfer

使用`scp`在两台主机间传输文件

```bash
# 从远程主机到本地：将ip为43.224.34.73主机root用户的`/home/A`目录复制到`/B`目录下
scp -r root@43.224.34.73:/home/A /B
# 从本地到远程主机：将`/B`传送到远程主机
scp -r /B root@43.224.34.73:/home/A
```

## 加速pip

- `linux && mac`: 修改`~/.pip/pip.conf`(没有就创建一个)  
- `window`: 修改`C:\Users\xx\pip\pip.ini`(没有就创建一个)
- 文件中增加以下内容 :

```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

> `index-url`也可以选择：http://pypi.douban.com/simple/

## 安装virtualenv

### Mac && Linux

- 安装

```bash
pip install virtualenv
pip install virtualenvwrapper
```

- 配置virtualenvwrapper

```bash
export WORKON_HOME='~/workon_home'  # 创建虚拟环境是所在的目录
source /usr/local/bin/virtualenvwrapper.sh
# 可以增加别名
alias mkpyenv='mkvirtualenv'
alias rmpyenv='rmvirtualenv'
alias lspyenv='lsvirtualenv'
alias cppyenv='cpvirtualenv'
```

### Windows

- 安装

```bash
pip install virtualenv
pip install virtualenvwrapper-win
```

- 配置virtualenvwrapper

```bash
set WORKON_HOME=C:\Users\dongn\workon_home
```

## 使用virtualenv

```bash
mkvirtualenv py2  # 新建环境,会自动进入环境，需要注意的是：系统需要已经安装了对应的python版本
workon py2  # 进入环境
deactivate  # 离开环境
rmvirtualenv py2  # 删除环境
```

对于使用非默认的python(window):

- 安装其他python版本到如：`C:\Python36`

- 设置并新建环境

```bash
set python36=C:\Python36\python.exe  # 设置环境变量
mkvirtualenv -p %python36% py3  # 使用环境变量新建环境
```

## 为windows增加alias

- 编写`bat`  

如将`mkvirtualenv`命令用别名`mkpyenv`表示，`bat`文件路径存储为如`D:\Libraries\alias\alias.bat`。`$*`表示这个命令还可能有其他参数

```bash
@doskey mkpyenv=mkvirtualenv $*
```

- 编写`reg`

```bash
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Command Processor]
"AutoRun"="D:\\Libraries\\alias\\alias.bat"
```

- 运行`reg`文件

## Install and use oh-my-zsh

### Install on ubuntu

```bash
# install dependency
apt-get install zsh
apt-get install git-core
# install zsh
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | zsh
# change default bash
chsh -s `which zsh`
# restart
sudo shutdown -r 0
```

### Common config of `~/.zshrc`

```bash
ZSH_THEME="ys"  # set themes
pugins=(git zsh-syntax-highlighting)  # set pugins
```

Download highlight plugins mentioned before:

```bash
git clone git://github.com/jimmijj/zsh-syntax-highlighting ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

增加自动补全插件:

```bash
wget -P ~/.oh-my-zsh/plugins/incr http://mimosa-pudica.net/src/incr-0.2.zsh
chmod 777 ~/.oh-my-zsh/plugins/incr/incr-0.2.zsh
# add folowing to ~/.zshrc
source ~/.oh-my-zsh/plugins/incr/incr-0.2.zsh
```

## Common bashrc set

```bash
# alias
alias profileconfig="sudo gedit /etc/profile"
alias bashconfig="code ~/.bashrc"  # 'code' can be set to another editor
alias zshconfig="code ~/.zshrc"
alias source_profile="source /etc/profile"
alias source_bash="source ~/.bashrc"
alias source_zsh="source ~/.zshrc"
alias probe_gpu="watch -n 10 nvidia-smi"
alias probe_cuda="cat /usr/local/cuda/version.txt"
```

## Where dpkg installed to

```bash
# If you don't know what is your package name, try to find it using this command
dpkg -l
# Find where the package installed to
dpkg -L <deb_name>
```