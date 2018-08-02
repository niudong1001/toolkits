# Toolkits
常用命令,工具使用方式的集合

## genSSHKey
一键生成各个端的sshkey
```bash
ssh-keygen -t rsa -C "1619249966@qq.com"
# window
cat C:\Users\dongn\.ssh\id_rsa.pub
# ubuntu
cat /home/niudong/.ssh/id_rsa.pub
```

## git http2ssh
将git的上传方式从http转成ssh
```bash
# config info 
git config --global user.name "Niudong-ubuntu"
git config --global user.email "1619249966@qq.com"
# change config(.git/config)
url = http://xxx.com/Name/project.git -> url = git@xxx.com/Name/project.git
```

## git submodule
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

## keep fork up to date
```bash
# in fork dir
git remote add upstream <原版仓库地址>
git pull upstream master
git push origin master
```

## scp file transfer
```bash
# 将ip为43.224.34.73主机的`/home/A`目录复制到`/B`目录下
scp -r root@43.224.34.73:/home/A /B
# 反向
scp -r /B root@43.224.34.73:/home/A
```

## 加速pip
- linux && mac: 修改`~/.pip/pip.conf`(没有就创建一个)  
- window: 修改`C:\Users\xx\pip\pip.ini`(没有就创建一个)  
- 文件中增加以下内容  
```bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```
> 源也可以选择：http://pypi.douban.com/simple/

## 安装virtualenv
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

## 使用virtualenv
```bash
mkpyenv py2 --python=python2  # 新建环境,会自动进入环境
workon py2  # 进入环境
deactivate  # 离开环境
rmpyenv py2  # 删除环境
```