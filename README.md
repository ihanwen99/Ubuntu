# Ubuntu
瀚文的Ubuntu学习之路

用这个README文件记录我的Ubuntu配置过程，方便之后重新配置使用

## 190515配置PyTorch

Conda是一个包管理器；Anaconda是一个python发行版。

pip可以允许你在任何环境中安装python包，而conda允许你在conda环境中安装任何语言包（包括c语言或者python）

### Github Desktop学习
https://www.jianshu.com/p/06a960d991aa
### Github 中 md 文件
在线的Markdown编辑器

http://mahua.jser.me/

https://blog.csdn.net/shaukon/article/details/78173911

https://www.jianshu.com/p/399e5a3c7cc5

### 安装Conda
#### 选择适合自己的版本，用wget命令下载。

wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

这里选择的是latest-Linux版本，所以下载的程序会随着python的版本更新而更新（现在下载的版本默认的python版本已经是3.7了）

#### 安装命令
chmod 777 Miniconda3-latest-Linux-x86_64.sh #给执行权限

bash Miniconda3-latest-Linux-x86_64.sh #运行
