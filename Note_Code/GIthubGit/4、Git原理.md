# GIt 原理

## 1.Hash简介

*1）*加密结果长度一致

*2）*同一数据，hash一致

## 2、Git文件管理工具

⭐增量式版本控制：集中式版本控制管理工具的文件管理机制<img src="C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817152104610.png" style="zoom:67%;" />

1. Git把数据/文件看成一组快照，每次==更新==提交时Git都会对当前全部文件制作一个快照并保存这个快照的索引。

2. 如果文件没有修改，Git则不会再次存储文件，只是通过链接/指针的方式指向源文件

   [^快照]:指针，如果没有修改，就是指向一个原文件的指针

<img src="C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817152923964.png" alt="image-20210817152923964" style="zoom:67%;" />

 ## 3、Git分支管理机构

3.1 创建分支：创建一个分支指针，指向当前版本

![image-20210817154122097](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817154122097.png)

3.2 分支切换

![image-20210817154257856](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817154257856.png)

![image-20210817154437406](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817154437406.png)

