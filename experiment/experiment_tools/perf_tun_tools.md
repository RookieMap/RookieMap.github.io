# 性能调优工具

## 显存跟踪
**Author**: [@Jiajun](https://github.com/Sumsky21)  

在GPU上跑实验时，有时会遇到显存不够用的情况（CUDA Out of Memory etc.），这时往往需要跟踪是哪些tensor占据了显存，以针对性地进行修复或优化。这里推荐两款工具：
### Pytorch-Memory-Utils
> 仓库地址：https://github.com/Oldpan/Pytorch-Memory-Utils

使用方法很简单：
* 将仓库中的`gpu_mem_track.py`放到你自己项目的任意目录下
* 在需要跟踪的py脚本内引入其中定义的tracker并实例化：
  ```python
  from gpu_mem_track import MemTracker
  gpu_tracker = MemTracker()
  ```
* 在程序中任意需要查看GPU显存使用情况的位置，添加一行代码：
  ```python
  gpu_tracker.track()
  ```
这时，tracker将在程序的当前目录下创建一个txt文件（仅第一次调用时创建，后续在文件中写入），在其中以追加模式 (`mode = 'a+'`) 输出自上一次调用`gpu_tracker.track()`以来，GPU显存的变化情况，类似下面的内容：
  ```
  At main.py line 12: <module>                          Total Tensor Used Memory:76.4   Mb Total Allocated Memory:76.4   Mb
  + | 1 * Size:(60, 3, 512, 512)    | Memory: 180.0 M | <class 'torch.Tensor'> | torch.float32
  - | 1 * Size:(40, 3, 512, 512)    | Memory: 120.0 M | <class 'torch.Tensor'> | torch.float32
  ```
包括当前位置、显存使用总量、新加入`(+)`和移除`(-)`的tensor及对应的显存占用。
* 根据tensor的size、class和dtype等属性，可以识别具体对应程序中的哪个张量；
* 由于显存记录是实时追加写入，可以一边以调试模式运行程序，一边打开记录文件，即时跟踪显存占用情况；
* 如果需要将该文件储存在其它位置或者修改命名规则，可以自行到MemTracker的__init__方法中修改相应变量的值。

这个工具主要优势在于轻量、便捷，但已经有较长时间没有更新，总之做一些简单分析时还是比较好用的。

### Pytorch_memlab
> 仓库地址：https://github.com/Stonesjtu/pytorch_memlab

功能和用法多于上面的工具，显示信息也更全面，发布时间较新而且一直在维护，还能在jupyter notebook中使用。  
TBD...用过后再来更新

-------------------------

如果你愿意提供任何信息、资源或观点，请在下方评论区留言，网站维护者会在第一时间看到，且会酌情将其添加为本页面的内容⚡️
