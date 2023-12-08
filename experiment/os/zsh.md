# Z-Shell

Author: [@Eureka](https://github.com/Eureka-Maggie) [@Reed Qiuu](https://github.com/Iri-sated) 

### 安装zsh（无sudo权限版）
通常，服务器管理员会在服务器上安装好zsh，你只需要启用即可，执行以下命令进行检查
``` bash
cat /etc/shells
```
通常会返回
``` bash
/bin/sh
/bin/bash
/usr/bin/tmux
/bin/zsh
...
```
+ 如果你不是管理员，且**需要安装**`zsh`，请阅读本章。
+ 如果服务器上**已经安装**有`zsh`，请记住查询到的`zsh`位置，并从[此处](#zsh基本配置)开始阅读。

#### 下载安装文件
下载安装包
``` bash
wget -O zsh.tar.xz https://sourceforge.net/projects/zsh/files/latest/download
```
解压，这里下载下来的是xz格式，要先用xz解压一遍，再用tar解压
``` bash
xz -d zsh.tar.xz
tar -xf zsh.tar 
cd zsh-5.9 #这里的版本号需要先在当前目录ls进行查看解压出来的文件的版本号
```

#### 安装ncurses
由于configure需要ncurses的依赖，直接安装zsh的话会遇到报错，所以先安装ncurses。先在`.bashrc`中添加如下行：
``` bash
export CXXFLAGS="-fPIC"
export CFLAGS="-fPIC"
export NCURSES_HOME=$HOME/username/ncurses  # 你自己设置一个的 ncurses 目录
export PATH=$NCURSES_HOME/bin:$PATH
export LD_LIBRARY_PATH=$NCURSES_HOME/lib:$LD_LIBRARY_PATH
export CPPFLAGS="-I$NCURSES_HOME/include" LDFLAGS="-L$NCURSES_HOME/lib"
```
配置完成后，重新初始化。
``` bash
source ~/.bashrc
```
安装ncurses。
``` bash
cd ~ && mkdir ncurses && cd ncurses  # 新建一个ncurses的安装目录，记得路径和环境变量对应
wget http://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.1.tar.gz  # 下载ncurses-6.1
tar -xzvf ncurses-6.1.tar.gz  # 解压
cd ncurses-6.1
./configure --prefix="$HOME/username/ncurses" --with-shared --without-debug --enable-widec  # 指定路径configure
make && make install  # 安装
```

#### 完成zsh安装
配置与编译。--prefix选项指定安装目录
``` bash
./configure --prefix=$/home/username/zsh-5.9 #这里可以先pwd查看当前路径
make
make install
```
配置zsh环境
``` bash
vim ~/.bashrc
```
``` bash
export PATH=$HOME/username/zsh-9/bin:$PATH
```
``` bash
source ~/.bashrc
```
至此，`zsh`成功安装完毕。但由于`zsh`是手动安装在自己的`home`目录下，所以没有根目录的文件修改权限，进而也没有办法使用`chsh -s /bin/zsh`将`zsh`设置为默认shell。因此，每次登录服务器之后，需要使用命令`zsh`或`exec zsh`手动切换`bash`为`zsh`。或在`bash`的配置文件中加上下面这行以默认启动`zsh`。
``` bash
exec $HOME/username/zsh-9/bin/zsh -l
```

---
### zsh基本配置
#### 激活zsh
在`bash`等其他shell中，可以通过执行以下命令来激活`zsh`
``` bash
# 以下二者皆可，选其一即可
zsh
exec zsh
```
在第一次进入`zsh`时，如果用户目录下没有`.zshrc`配置文件，会出现以下界面，选2即可。
![exec zsh后界面](https://files.mdnice.com/user/52415/60f55d5e-e774-458a-80ff-852275a2bda3.png)

#### 设为默认shell
使用下面的命令设置为默认shell，`/bin/zsh`为查询到的`zsh`位置。这一过程通常需要输入密码。
``` bash
chsh -s /bin/zsh
> Changing shell for xxx.
> Password: 
```
通常，需要将`bash`配置文件中添加过的内容都写入`.zshrc`，如网络配置、默认激活`conda`等，以完成`zsh`的配置。如果你打算安装Oh-my-zsh等管理框架，可以将这一过程放到管理框架安装完成后进行。

#### Oh-my-zsh框架
*这个部分可以根据自己选择是否需要进行。*

先安装oh-my-zsh
``` bash
git clone https://github.com/ohmyzsh/ohmyzsh.git ~/.oh-my-zsh
# 或用脚本傻瓜式安装
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
安装完成后，你会看到下面这个酷炫的界面。
![](<截屏2023-12-08 10.47.49.png>)

##### 主题
在`.zshrc`中修改，其中`THEME_NAME`为你想要的主题名字
``` bash
ZSH_THEME="THEME_NAME"
```
> 可供选择的主题：https://github.com/ohmyzsh/ohmyzsh/wiki/Themes

##### 插件
`zsh`的插件都配置在`~/.oh-my-zsh/plugins/`目录下。该目录下已经有的一些插件是内置的，后续需要安装插件也装到该目录下即可。

当你需要启用某个名为`[xxx]`的插件时，在`.zshrc`中加入如下语句（或修改原语句）
``` bash
plugins=(
    # other plugins...
    [xxx]
)
```

##### 推荐的外置插件
从这里开始安装的插件都需要联网下载，请**确保你已经配置妥当**`.zshrc`。下载完成后，按照上面提到的方法修改`.zshrc`的值，并使用`source ~/.zshrc`重新加载。
- **语法高亮**：用不同记号标记处合法语句、非法语句和存在的文件
``` bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
下图分别展示了未开启高亮，合法语句`source`，存在的文件`./.zshrc`和非法语句`cccccc`展示出的效果。

![](image.png)

- **自动补全**：使用的时候，按键盘的→即可自动补全
``` bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
下图展示了补全前的效果。

![](image-1.png)

---
### zsh可能导致的问题及解决方案
#### zsh不能正确启动
在`tmux`和`Jupyter Lab`等应用中，可能无法正确启动`zsh`，具体表现为不会唤起任何shell。
##### 解决方法1：在相应配置文件中设置zsh为默认shell
可在`~/.tmux.conf`中添加如下语句（没有这个文件的话创建一个）
``` bash
set-option -g default-shell /bin/zsh
```
对于`Jupyter Lab`，先生成配置文件
``` bash
jupyter lab --generate-config
```
然后，在生成的`jupyter_lab_config.py`文件中，将相应行改为：
``` python
c.ServerApp.terminado_settings = {'shell_command': ['/bin/bash']}
```
注意，上面两个更改都要在`tmux`和`Jupyter Lab`关闭所有窗口重新启动后才会生效。

##### 解决方法2：通过bash唤起zsh
如果上面方法仍无效，可仿照解决方法1，将出错应用的默认终端设置为`bash`，正常进入`bash`后，通过`bash`唤起`zsh`。

