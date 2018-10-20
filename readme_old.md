# Toolkits

常用命令,工具使用方式的集合

<!-- TOC -->

- [Toolkits](#toolkits)
    - [安装virtualenv](#安装virtualenv)
        - [Mac && Linux](#mac--linux)
        - [Windows](#windows)
    - [使用virtualenv](#使用virtualenv)
    - [为windows增加alias](#为windows增加alias)
    - [Install and use oh-my-zsh](#install-and-use-oh-my-zsh)
        - [Install on ubuntu](#install-on-ubuntu)
        - [Common config of `~/.zshrc`](#common-config-of-zshrc)

<!-- /TOC -->

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