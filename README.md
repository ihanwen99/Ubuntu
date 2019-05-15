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

http://mahua.jser.me/ #好像不支持中文输入诶

https://www.zybuluo.com/mdeditor #我现在用这个，就是反应速度有一丢丢的延迟
这个也不行，因为显示的效果和GitHub上面的不一样

https://blog.csdn.net/shaukon/article/details/78173911

https://www.jianshu.com/p/399e5a3c7cc5

### 安装Conda
#### 选择适合自己的版本，用wget命令下载。

wget -c https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

这里选择的是latest-Linux版本，所以下载的程序会随着python的版本更新而更新（现在下载的版本默认的python版本已经是3.7了）

#### 安装命令
chmod 777 Miniconda3-latest-Linux-x86_64.sh #给执行权限

bash Miniconda3-latest-Linux-x86_64.sh #运行

安装成功后，打开一个新的terminal，使用which python命令查看python的路径是否已经指向miniconda中的python。
#### 如果需要修改路径
修改~/.bashrc，添加以下这行（设置环境变量）

export PATH="/你的miniconda路径/bin:$PATH"

然后执行

source ~/.bashrc
#### 进入conda的环境
使用 conda list 来测试就好啦
#### conda的进阶使用
https://www.jianshu.com/p/edaa744ea47d


### CUDA从入门到精通
https://blog.csdn.net/qq_30263737/article/details/81235580
