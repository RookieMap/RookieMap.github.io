# 性能调优工具 profiler 等

## 效率调优工具

Profiler


## 效果调优类工具

最简单暴力的就是自己写循环，用python或者shell做grid search，对learning rate、dropout、emb size，layer层数等各种hyper parameters在validation set上做验证，选择最佳参数

更高效的方法则是利用`optuna`等自动调优工具

### optuna

