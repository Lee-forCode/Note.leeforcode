Git分支

## 1、什么是分支？

多线进行开发

特点：1）各分支之间互不影响，彼此独立

2）并行开发，效率提升

![image-20210816175617519](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816175617519.png)

## 2、分支操作

2.1 创建分支

```shell
git branch  [branch name]
```

![image-20210816180305833](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816180305833.png)

2.2 查看分支

```shell
git branch -v
```

2.3 切换分支

```shell 
git checkout [branch name]
```

2.4 合并分支

```shell
git checkout [要修改的分支名]
git merge [branch name]
```

2.5 合并分支后冲突解决

- 不同分支修改==文件同一位置==而造成的

  ![image-20210816183001678](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816183001678.png)

- 冲突表现

  ![image-20210816181709759](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816181709759.png)

- 冲突解决

  ```shell
  # 1、修改文件到自己满意的程度
  # 2、提交到暂存区
  git add [文件名]
  # 3、提交到本地库
  git commit -m "日志内容"
  ```

  ### 流程图

  ![image-20210817094051123](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817094051123.png)

