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
# gen (win&&linux&&mac)
ssh-keygen -t rsa -C "1619249966@qq.com"
# window
cat C:\Users\dongn\.ssh\id_rsa.pub
# linux&&mac
cat /home/niudong/.ssh/id_rsa.pub
```

## Git HTTP2SSH

将git的上传方式从http转成ssh

```bash
# config info 
git config --global user.name "Niudong-ubuntu"
git config --global user.email "1619249966@qq.com"
# change config(.git/config)
url = http://xxx.com/Name/project.git -> url = git@xxx.com/Name/project.git
```

## Git Submodule

git子仓库操作

```bash
# load submodule
git clone <仓库地址> --recursive  # 递归的方式克隆整个项目
git submodule update --init --recursive  # 初始化子仓库并更新
# add submodule
git submodule add <仓库地址> <本地路径>  # 添加子模块(git submodule)
# delete submodule
git rm the_submodule
rm -rf .git/modules/the_submodule
```

## Keep Fork Up To Date

让fork up的仓库更新到源仓库的最新状态

```bash
# must in fork dir(local)
git remote add upstream <原版仓库地址>
git pull upstream master
git push origin master
```

## Scp File Transfer

使用`scp`在两台主机间传输文件

```bash
# 从远程主机到本地：将ip为43.224.34.73主机的`/home/A`目录复制到`/B`目录下
scp -r root@43.224.34.73:/home/A /B
# 从本地到远程主机：-
scp -r /B root@43.224.34.73:/home/A
```

## 加速pip

- `linux && mac`: 修改`~/.pip/pip.conf`(没有就创建一个)  
- `window`: 修改`C:\Users\xx\pip\pip.ini`(没有就创建一个)
- 文件中增加以下内容  

```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

> 源也可以选择：http://pypi.douban.com/simple/

## 安装virtualenv

### Mac && Linux

- 安装

```bash
sudo pip install virtualenv
sudo easy_install virtualenvwrapper
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
mkpyenv py2 --python=python2  # 新建环境,会自动进入环境
workon py2  # 进入环境
deactivate  # 离开环境
rmpyenv py2  # 删除环境
```

## 为windows增加alias

- 编写`bat`  

如将`mkvirtualenv`命令用别名`mkpyenv`表示，`bat`文件路径存储为如`D:\Libraries\alias\alias.bat`

```bash
@doskey mkpyenv=mkvirtualenv
```

- 编写`reg`

```bash
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\Command Processor]
"AutoRun"="D:\\Libraries\\alias\\alias.bat"
```

- 运行`reg`文件