# 环境管理 conda 类工具

Author: [@pujiayue](https://github.com/pujiayue)


以下是对环境管理conda类的介绍、安装步骤以及常见问题的配置的补充：

---

## [Conda]介绍
Conda 是一个开源的跨平台包管理系统和环境管理系统，用于安装、管理和运行软件包。它最初是为 Python 程序员设计的，但也可以用于其他编程语言和领域。

下面是 Conda 的一些主要特点和功能：

1. 包管理：Conda 可以轻松地安装、更新和删除软件包。它提供了一个广泛的预编译软件包仓库，其中包含了许多常用的科学计算、数据分析和机器学习工具。你可以使用 Conda 命令来搜索、安装和管理这些软件包。

2. 环境管理：Conda 允许你创建和管理多个独立的环境，每个环境都可以拥有不同的软件包和版本。这对于在不同项目之间隔离依赖关系非常有用，以避免冲突和版本不一致的问题。你可以使用 Conda 创建新环境、复制环境、切换环境等。

3. 跨平台支持：Conda 可以在多个操作系统上运行，包括 Windows、macOS 和 Linux。这使得在不同平台之间共享和复制环境变得更加容易。

4. 虚拟环境支持：Conda 可以与虚拟环境管理工具（如 venv 和 virtualenv）一起使用，以提供更灵活的环境管理选项。

5. 扩展性：Conda 是一个可扩展的系统，允许用户创建和发布自己的软件包。你可以将自己的软件包上传到 Conda 仓库，供其他人使用和安装。

总的来说，Conda 是一个功能强大的包管理和环境管理工具，适用于各种编程语言和领域。它简化了软件包的安装和管理过程，并提供了灵活的环境隔离和管理选项。无论是在个人项目中还是在团队合作中，Conda 都是一个有用的工具，可以帮助你管理软件包依赖关系和创建一致的开发环境。

## 安装conda ##

以下为在远程服务器上安装conda的详细步骤 <br />
以133服务器的2219端口为例

### 1. ###
  开始页面会提示conda安装包在哪个目录下 使用cd命令进入对应目录

  ``` bash
  #如:“/data22/public/tools/目录下有anaconda的安装脚本”
  >>cd /data22/public/tools/
  ```
  用ls命令确认是否有conda安装包
  ``` bash
  >>ls
  >>Anaconda3-2023.09-0-Linux-x86_64.sh
  ```

### 2. ###
  直接bash进行安装
  ```bash
  >>bash Anaconda3-2023.09-0-Linux-x86_64.sh
  ```

  一直按enter键 直到出现Do you accept the license terms? [yes|no] *（注意不要按过头了）*
  输入>>yes

  ####
  注意在等待配置时要注意进度
  Do you wish the installer to initialize Anaconda3 by running conda init? [yes no]时及时输入yes
  然后关掉当前终端窗口（shell） 重新登录即可看到直接进入了base环境
  ####

### 3.修改配置 ###
  ```bash
  >>vim ./.bashrc
  #在最后一行加上如下配置
  export http_proxy="http://10.61.3.12:7788"
  export https_proxy="http://10.61.3.12:7788"
  # 然后使其生效:
  >>source ./.bashrc
  ```

### 4.换清华源 ###
  ```bash
  >>vim ~/.condarc
  ```
  在condarc文件中加入如下信息
  ```bash
  channels:
    - defaults
  show_channel_urls: true
  default_channels:
    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
    - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
  custom_channels:
    conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
    deepmodeling: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
  ```

## 其余配置 ##

### 1.安装pytorch ###
在base环境中执行以下命令行
  ```bash
  >>conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
  ```

### 2.指定Hugging Face库的安装路径 ###
  在.bashrc中设置HF_HOME`HF_HOME(用于指定Hugging Face模型和缓存文件的默认根目录)
  ```bash
  >>vim ./.bashrc
  ```

  在文件最后插入（按i进入编辑模式）
  ```bash
  export HF_HOME="/data/public/huggingface"
  ```
  保存并退出(按esc后按“：wq”)

  重新source一下
  ```bash
  >>source ./.bashrc
  ```
### 3. Jupyter Notebook相关包 ###
```bash
>>conda install nb_conda_kernels
>>conda install ipykernel
>>conda install ipywidgets
```

如果你愿意提供任何信息、资源或观点，请在下方评论区留言，网站维护者会在第一时间看到，且会酌情将其添加为本页面的内容⚡️
