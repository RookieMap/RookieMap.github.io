# jupyter

Author: [@RuichenQiu](https://github.com/Iri-sated) & [@FeiSun](https://github.com/FeiSun) with the help of ChatGPT


以下是对Jupyter Lab的介绍、安装步骤以及常见问题的配置的补充：

---

## [Jupyter Lab](https://jupyterlab.readthedocs.io/en/stable/index.html)介绍
[Jupyter](https://jupyter.org/)是一个交互式的开发环境，用于数据科学、计算机科学教学和研究。它支持多种编程语言，如Python、R和Julia，并允许用户在一个统一的界面中创建和共享包含实时代码、方程、可视化和文本的文档。

而 Jupyter Lab 是下一代的Jupyter，是最新的基于Web的交互式开发环境，用于笔记本、代码和数据。其灵活的界面允许用户在数据科学、科学计算、计算新闻学和机器学习等领域配置和排列工作流程。模块化设计使得通过扩展来增强和丰富功能成为可能。

简单来说，Jupyter Lab比之前的jupyter notebook之类的功能更强大，可以在浏览器中直接启动多个terminal、notebook、python解释器，直接编辑各种文件，也可以安装插件，扩展功能。
现在用的话，推荐直接安装Jupyter Lab。

## 安装Jupyter Lab

1. 确保已安装Python和pip。

2. 通过pip或者conda安装Jupyter Lab：

   ``` bash
   pip install jupyterlab
   ```

3. 安装完成后，运行Jupyter Lab：
   ``` bash
   jupyter lab --port=XXXX --ip=0.0.0.0 --no-browser
   ```
一般需要指定监听ip为`0.0.0.0`，不然远程服务器上启动的jupyter，本地可能打不开。
根据程序输出log信息中提示，一般可在浏览器中访问`http://127.0.0.1:XXXX`或`http://localhost:XXXX`，其中XXXX是上面设置的端口号。上面的ip，如果是远程服务器的，修改为对应的服务器ip，前提是端口已开放，或者通过ssh方式中转。


## 配置

**配置文件（可选）**: 对于更高级的配置，可以编辑Jupyter配置文件。这个文件通常位于`~/.jupyter/jupyter_lab_config.py`。
*jupyter lab的配置文件名和里面的字段名，过去变化过，记不清了，大家在使用时自己确认*
如果文件不存在，可以通过以下命令生成：
   ```bash
   jupyter lab --generate-config
   ```
这个文件中可以设置Jupyter Lab的密码、端口和其他高级配置。


对于密码的设置，需要使用jupyter的密码生成接口，生成密码加密后的字符串，放到配置文件中。

```python
In [1]: from jupyter_server.auth import passwd

In [2]: passwd()
Enter password:
Verify password:
Out[2]: 'argon2:xxxxxxx:xxxxxxxx'
```

或者

``` bash
jupyter lab password
> Enter password:
> Verify password:
```

## Jupyter服务器配置（frpc版）

### 端口配置

挑一个喜欢的端口号，在服务器上运行检查端口是否被占用

``` bash
# 以下命令二选一即可
netstat -tlnp | grep [PORT_ID]
lsof -i :[PORT_ID]
```

对于端口的使用处理，用两种情况：
* 直接找服务器管理员，开放防火墙对应的端口，这种最简单直接，但是要确保设置强密码，防止端口被恶意利用，造成实验室负面影响
* 如果端口不方便开放，可以通过`ssh`方式转发端口数据

#### 端口转发

基本原理是：在SSH连接建立后，可以配置哪些端口的数据应该通过这个加密通道传输。可以让远程服务器上的xxxx端口被映射到本地机器的yyyy端口。一旦端口映射设置完成，所有发送到本地yyyy端口的数据都会被自动加密并重定向到远程服务器的xxxx端口。反过来，从远程xxxx端口发送到本地机器的数据也会通过同一个加密通道传输。

由于所有的数据都是通过一个已经建立的SSH连接传输的，因此可以绕过远程服务器上的防火墙规则。也就是说，即使远程端口xxxx被防火墙封锁，还是可以通过SSH隧道访问它。

```sh
ssh -C -N -f -L local_port:localhost:remote_jupyter_port username@remote_server_ip
```

在这里：

- `-C` 启用压缩，有助于提高传输效率。
- `-N` 表示不执行远程机器上的命令，这在只需要端口转发时很有用。
- `-f` 将 SSH 客户端放到后台运行。
- `-L` 指定本地端口转发。

需要将 `local_port` 替换为希望在本地机器上用来访问 Jupyter Lab 的端口，`remote_jupyter_port` 替换为远程服务器上 Jupyter Lab实际运行的端口，`username` 替换为远程服务器上的用户名，而 `remote_server_ip` 替换为远程服务器的 IP 地址。

例如，如果用户名是 `qiuruichen`，远程服务器的 IP 是 `10.208.61.133`，并且您想要在本地机器的 `7799` 端口访问 Jupyter，命令将是：

```sh
ssh -C -N -f -L 7799:127.0.0.1:7799 qiuruichen@10.208.61.133
```

运行此命令后，只要 SSH 隧道处于活动状态，就可以在本地机器上通过访问 `http://127.0.0.1:7799` 来使用 Jupyter Notebook。


#### frpc 配置

当然上面是在实验室内网的用法。如果是在计算所外面，走frp的时候，则需要在中转机器上执行这个命令，然后在机器上的frpc配置文件中加上对应的配置，就跟正常ssh差不多使用了。

内部运行frpc的机器上的配置文件，加入:

```sh
[jupyterlab_[SERVER_NAME]_[YOURNAME]]
type = stcp
sk = [sk] # token密码
local_ip = 10.208.61.133  # 如果是在机器上进行了ssh转发，则这里直接改为127.0.0.1
local_port = 7799
use_encryption = true
use_compression = true
```

本地配置文件参考如下格式进行添加

```sh
[jupyterlab_[SERVER_NAME]_[YOURNAME]_visitor]
type = stcp
role = visitor
server_name = jupyterlab_[SERVER_NAME]_[YOURNAME] # 这个名字需要于远程内网机器上运行的配置名一致
sk = [SK]
bind_addr = 127.0.0.1
bind_port = [PORT_ID]
use_encryption = true
use_compression = true
```

这样frpc连接后，就可以直接浏览器`http://127.0.0.1:PORT_ID`使用jupyter lab。

这种方式其实也适用于`tensorboard`等其他网页应用。


## Jupyter Lab 插件

Jupyter Lab目前有一定的插件生态，最简单的安装方式可以在Jupyter Lab界面里直接开启，安装。一些插件推荐list如下：
[https://github.com/mauhai/awesome-jupyterlab](https://github.com/mauhai/awesome-jupyterlab)
[https://github.com/Yogayu/awesome-jupyterlab-extension](https://github.com/Yogayu/awesome-jupyterlab-extension)

### [ipympl](https://matplotlib.org/ipympl/)
  - ipympl允许在Jupyter Notebooks、Jupyter Lab、Google Colab和VSCode notebooks中使用matplotlib的交互式特性。

``` bash
pip install ipympl
# or 
conda install -c conda-forge ipympl
```

#### Basic Example

To activate the `ipympl` backend all you need to do is include the `%matplotlib ipympl` magic in the notebook. Alternatively you can use `%matplotlib widget` which will have the same effect.

``` python
%matplotlib ipympl
import matplotlib.pyplot as plt
import numpy as np

fig, ax = plt.subplots()


x = np.linspace(0, 2*np.pi, 100)
y = np.sin(3*x)
ax.plot(x, y)
```

### [Plotly](https://plotly.com/python/)

The plotly Python library is an interactive, open-source plotting library that supports over 40 unique chart types covering a wide range of statistical, financial, geographic, scientific, and 3-dimensional use-cases.

Built on top of the Plotly JavaScript library ([plotly.js](https://plotly.com/javascript/)), plotly enables Python users to create beautiful interactive web-based visualizations that can be displayed in Jupyter notebooks, saved to standalone HTML files, or served as part of pure Python-built web applications using Dash. The plotly Python library is sometimes referred to as "plotly.py" to differentiate it from the JavaScript library.

``` bash
pip install plotly==5.18.0
# or conda
conda install -c plotly plotly=5.18.0
```
更方面的使用，可能是安装[`jupyter-dash`](https://github.com/plotly/jupyter-dash)。


### 常见问题配置
- **内核管理**：可以安装和管理不同的Jupyter内核，以支持多种编程语言。
- **扩展安装**：Jupyter Lab支持各种扩展，如可视化工具、代码格式化等。
- **主题定制**：用户可以选择或自定义Jupyter Lab的主题以改善视觉体验。

---

