# toolkits
常用命令,工具使用方式的集合

## genSSHKEy
一键生成各个端的sshkey
### window
```bash
ssh-keygen -t rsa -C "1619249966@qq.com"
cat C:\Users\dongn\.ssh\id_rsa.pub
```

## submodule
```bash
git clone <仓库地址> --recursive  # 递归的方式克隆整个项目
git submodule add <仓库地址> <本地路径>  # 添加子模块(git submodule)
git submodule update --init --recursive  # 初始化子仓库并更新
git rm --cached <本地路径>  # 删除子仓库
```