# 无sudo权限安装zsh

作者：[Eureka](https://github.com/Eureka-Maggie)

1. 下载安装包
```
wget -O zsh.tar.xz https://sourceforge.net/projects/zsh/files/latest/download
```
2. 解压，这里下载下来的是xz格式，要先用xz解压一遍，再用tar解压
```
xz -d zsh.tar.xz
tar -xf zsh.tar 
cd zsh-5.9 #这里的版本号需要先在当前目录ls进行查看解压出来的文件的版本号
```
3. 由于configure需要ncurses的依赖，直接安装zsh的话会遇到报错，所以先安装ncurses
```
vim ~/.bashrc
```
```
export CXXFLAGS="-fPIC"
export CFLAGS="-fPIC"
export NCURSES_HOME=$HOME/username/ncurses  # 你自己设置一个的 ncurses 目录
export PATH=$NCURSES_HOME/bin:$PATH
export LD_LIBRARY_PATH=$NCURSES_HOME/lib:$LD_LIBRARY_PATH
export CPPFLAGS="-I$NCURSES_HOME/include" LDFLAGS="-L$NCURSES_HOME/lib"
```
```
source ~/.bashrc
```
```
cd ~ && mkdir ncurses && cd ncurses  # 新建一个ncurses的安装目录，记得路径和环境变量对应
wget http://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.1.tar.gz  # 下载ncurses-6.1
tar -xzvf ncurses-6.1.tar.gz  # 解压
cd ncurses-6.1
./configure --prefix="$HOME/username/ncurses" --with-shared --without-debug --enable-widec  # 指定路径configure
make && make install  # 安装
```

3. 配置与编译。--prefix选项指定安装目录
```
./configure --prefix=$/home/username/zsh-5.9 #这里可以先pwd查看当前路径
make
make install
```
4. 配置zsh环境
```
vim ~/.bashrc
```
```
export PATH=$HOME/username/zsh-9/bin:$PATH
```
```
source ~/.bashrc
```
至此，zsh成功安装完毕。但由于zsh是手动安装在自己的home目录下，所以没有根目录的文件修改权限，进而也没有办法使用chsh -s /bin/zsh将zsh设置为默认shell。

因此，每次登录服务器之后，需要使用命令zsh或exec zsh手动切换bash为zsh。或使用下面的命令设置为默认shell。
```
chsh -s /bin/zsh
```

5. 激活zsh
```
exec zsh
```
会出现如下界面

![exec zsh后界面](https://files.mdnice.com/user/52415/60f55d5e-e774-458a-80ff-852275a2bda3.png)

选2即可。

6. 将zsh设为默认shell
```
vim ~/.bash_profile
```
```
exec $HOME/username/zsh-9/bin/zsh -l
```
7. 安装oh-my-zsh
```
git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh 
```
8. 安装插件
- 高亮
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
```
plugins=(zsh-syntax-highlighting)#和其他plugins只需要一个空格，不要打别的符号
echo "source ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```
```
#重启zsh刷新
zsh
```

![使用前](https://files.mdnice.com/user/52415/8e1497ef-bcf2-494e-b85e-e1db13d2c4d2.png)


![使用后](https://files.mdnice.com/user/52415/5f97caeb-44ff-4e7d-95c8-7d577b8ad911.png)

- 自动补全
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
```
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
echo "source ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
```
```
#重启zsh刷新生效
zsh
```
使用的时候，按键盘的→即可自动补全

![按→前](https://files.mdnice.com/user/52415/2217c6dc-fd30-4807-aee9-cfebb80cb7ac.png)

![按→后](https://files.mdnice.com/user/52415/5f97caeb-44ff-4e7d-95c8-7d577b8ad911.png)
