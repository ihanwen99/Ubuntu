# Ubuntu

瀚文的Ubuntu学习之路

用这个README文件记录我的Ubuntu配置过程，方便之后重新配置使用

## 190515 配置Conda

Conda是一个包管理器；Anaconda是一个python发行版。

pip可以允许你在任何环境中安装python包，而conda允许你在conda环境中安装任何语言包（包括c语言或者python）

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

#### 添加清华源（但是清华源也要倒闭了）

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/

conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda/

#### conda的进阶使用

https://www.jianshu.com/p/edaa744ea47d

## 190523 Ubuntu下使用Conda

1. 输入conda,进入conda环境

2. conda create -n *（环境名称） python==3.7

   此处输入你要创建的环境名称，和你需要的python版本

3. 随后会提示确认或者取消，输入y确认创建

4. 到此环境就创建成功了：输入source activate *(环境名) 进入我们创建的环境

#### 删除自己添加的源

`conda config --remove-key channels`

#### Conda的信息

`conda info`

#### 现在使用交大源（也不行诶。。。）

后记：为什么要用源，我们可以直接使用交大的网络来链接官方原本的源。。。

- pkgs/free: `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/free`
- pkgs/main: `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/main`
- pkgs/mro: `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/mro`
- pkgs/msys2: `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/msys2`
- pkgs/pro: (deprecated) `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/pro`
- pkgs/r: (empty) `conda config --add channels https://anaconda.mirrors.sjtug.sjtu.edu.cn/pkgs/r`

#### 设置搜索时显示通道地址

`conda config --set show_channel_urls yes`

#### Conda常用命令整理
https://blog.csdn.net/menc15/article/details/71477949
