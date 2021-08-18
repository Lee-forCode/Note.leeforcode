# Git本地库与远程库交互

## 1、交互原理

![image-20210816003758738](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816003758738.png)

## 2、创建本地库、远程库

2.1 创建本地库

2.2 创建远程库

2.3 本地库创建远程库地址别名

1. 获取远程库地址（HTTP）
2. 创建远程库别名

```
git remote add [别名] [http address]    # 创建别名
git remote -v  			# 查看别名
```

![image-20210817155814465](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817155814465.png)

2.4 推送（push）

```
git push [别名/完整地址] 分支名
例：git push origin master
```

2.5 克隆（clone）

```shell
git clone [远程库地址]
```

- 完整的把远程库下载到本地
- 创建远程库别名
- 自动初始化本地库（git init）

2.6 邀请其他加入团队

- GitHub：Settings–Manage access – Invite a collaborator

2.7  远程库修改的拉取（pull）

```
pull = fetch + merge    #
git pull [地址/别名] [分支名] = 
git fetch [地址/别名] [分支名]    	# 远程库文件下载到本地
+
git merge [地址/别名] [分支名]		# 合并本地库文件和远程库文件
```

![image-20210817162607240](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817162607240.png)

![image-20210817162622309](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210817162622309.png)

2.8 克隆与拉取

| 克隆==clone==               | 拉取==pull==                                                 |
| --------------------------- | ------------------------------------------------------------ |
| git clone [远程库地址] 分支 | git pull [别名] 分支                                         |
| 本地库不存在远程区的资源    | 相当于对本地库资源的更新，本地库与远程库版本一致             |
|                             | 当本地库资源与远程库出现==版本不一致==，需要pull[^他人推送push，导致版本发生变化] |

2.9 解决冲突（不同人修改同一文件同一位置）

- 要点：1、如果不是基于GitHub远程库最新版资源所做的修改，==不能推送==，必须先拉取（pull）

  2、拉取（clone）下来进入冲突状态，按分支冲突解决

