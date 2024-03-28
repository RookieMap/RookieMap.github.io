# 代码调试

## pdb
**Author**: [@Jiajun](https://github.com/Sumsky21)

> [pdb --- Python 的调试器 — Python 3.12.0 文档](https://docs.python.org/zh-cn/3/library/pdb.html)  
- python的很有用的调试器
- 在代码内（侵入式）设置断点
	- `import pdb`; `pdb.set_trace()` 
	- `breakpoint()`  
- 非侵入式设置断点
	- `python -m pdb script.py` 直接启动
	- `b 行号`在当前文件对应行设置断点，或者`b 文件路径:行号`在指定文件设置断点，仅当次运行有效
- 在断点处停下后可以查看变量值，执行表达式等操作
- 一些常用操作  
	- n - next
	- c - continue
	- q - quit
	- s可以进入调用内层函数  
	- j 行号，直接跳转到指定行，跳过的部分不执行；  
	- unt：行号比当前大或者在指定行号处停止，可以用于跳出当前循环到下一语句  
	- u/d：在当前函数调用栈内上/下移动
- 其它隐藏功能，比如命令行加减断点、交互式调试，事后调试等，参考文档
	- 事后调试：需要使用  python -m pdb，报错后不会退出程序而是停在报错的代码处

------
如果你愿意提供任何信息、资源或观点，请在下方评论区留言，网站维护者会在第一时间看到，且会酌情将其添加为本页面的内容⚡️
