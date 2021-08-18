Git 的结构

## 一、本地结构

### 1、工作区（写代码）、暂存区（临时存储）、本地库（历史版本）

![image-20210816001238039](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816001238039.png)

### 2、 Git和代码托管中心

2.1 局域网

- GitLab服务器

2.2 外网环境

- [GitHub](https://github.com/)
- [码云](https://gitee.com/)

### 3、本地库与远程库的交互

3.1 团队内协作

![image-20210816003758738](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816003758738.png)

3.2 跨团队协作

![image-20210816004528698](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816004528698.png) 

### 4、Git命令行操作【本地库】

| 状态查看命令：git status                                     | 工作区、暂存区状态          |
| ------------------------------------------------------------ | --------------------------- |
| 文件添加：git add [file]                                     | 工作区新建/修改添加到缓存区 |
| 文件提交：git commit -m “commit message” [filename]          | 缓存区提交到本地库          |
| 历史版本查看：①git log ②简洁模式 git log –oneline / –pretty=oneline ③git relog 【查看所有版本】 |                             |
| 版本前进/后退【删除文件找回】：git reset –hard [索引值]      | 前进/后退均可【推荐】       |

4.1 本地库初始化![image-20210816152849973](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816152849973.png)

- 命令：==git init==
- 效果：本地库初始化就是生成  ==.git==文件![image-20210816153042095](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816153042095.png)
- 注意事项：==.git==目录存放本地库相关的子目录和文件，不能删改  

4.2 设置签名

- 形式

  用户名：tom

  E-mail地址：goodmorning_pro@gemail.com

- 作用：区分不同开发人员身份，*与登录远程库（代码托管中心）账号无关*

- 命令

  - 项目级别/仓库级别：仅在本地库范围内生效![image-20210816154851782](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816154851782.png)
    - git config  user.name tom_pro
    - git config user.email  goodmorning@gmail.com
    - ==信息保存位置：.git/config==
  - 系统用户级别(登陆当前操作系统的用户)
    - git ==config --global==  tom_glb
    - git ==config –global== goodmorning@gmail.com
    - 信息保存：==当前用户家目录==![image-20210816155223641](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816155223641.png)
  - *级别优先级*
    - 项目级别 优先于 系统用户级别
    - ==二者都没有是不允许的==

  4.3  添加提交及查看状态

  - ​	查看状态：==git status==![image-20210816155955803](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816155955803.png)

    ​	==*vim good.txt*==后，git状态![image-20210816160039881](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816160039881.png)

    

  - 添加到暂存区：==git add  文件==

    添加到暂存区：==*git add good.txt*==

    ![image-20210816160644080](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816160644080.png)

  - 提交到本地库==git commit  文件名==

  - ![image-20210816161348099](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816161348099.png)

  - *已提交但修改文件，git状态*

    ![image-20210816161744674](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816161744674.png)

    - 两种处理：  1) ==git add==![image-20210816162307770](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816162307770.png)

      ​					2) ==git commit -a==

  4.4 版本前进后退

  - 4.4.1 历史记录查看：*1)*==git log==

    ![image-20210816163354749](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816163354749.png)

    *2)* 简洁模式：==$ git log --pretty=oneline==![image-20210816163634068](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816163634068.png)

    *3）* ==$ git log --oneline==

    ![image-20210816163858880](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816163858880.png)

    *4）*版本移动步数 ==gie reflog==

    [^HEAD]:指针，{数} 移动到当前版本的步数

    ![image-20210816164044375](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816164044375.png)

    

  - 4.4.2 ==版本前进后退   git reset== **可用于删除文件找回！！**

    ​		参数：

    ​			–soft：仅在本地库移动head指针

    ![image-20210816171319247](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816171319247.png)

    ​			–mixed：1）本地库移动HEAD指针 2）重置暂存区

    ![image-20210816171520036](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816171520036.png)

    ​			–hard：1）本地库移动HEAD指针 2）重置暂存区 3）重置工作区

    - 【推荐】基于索引：==git reset –hard [索引值】==

      [^索引值]:通过 ==git reflog==获取

      

      ![image-20210816165234085](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210816165234085.png)

    - 使用~符号【 ~[num]后退 num步】：==git reset –hard HEAD ~[num]==

    - 使用^符号【一个 ‘ ^ ’只能退一个版本】:==git reset –hard HEAD^==

  - 4.4.3 删除文件找回

    - 前提删除前，文件存在状态提交到了本地库
    - 使用命令 git reset –hard [索引值]回到找回版本

  - 4.4.4 文件比较差异[*工作区*]

    - ==git diff [filename]==:工作区文件和暂存区比较

    - ==git diff HEAD [filename]==：文件历史版本比较

      [^git diff]: 多文件比较

