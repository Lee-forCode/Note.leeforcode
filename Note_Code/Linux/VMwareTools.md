# VMware Tools安装

### *1、环境、工具*

系统：Win10

虚拟机软件：VMware workstation Pro

安装镜像：Centos7

### *2、具体步骤*

*1）安装VMware tools*

选择状态栏 **虚拟机–安装VMwaretools** （相当于将一个 CDROM 硬盘插入系统）

![image-20210912005201923](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210912005201923.png)

*2）命令行安装*

```bash
  #!/usr/bash
  # 创建CD临时挂载目录
  mkdir /mnt/cdrom
  # 将CD光盘挂载在临时目录下
  mount /dev/cdrom /mnt/cdrom
  # 提示：mount: /dev/sr0 写保护，将以只读方式挂载
  
  # 查看是否挂载
  mount 
  # 提示：/dev/sr0 on /mnt/cdrom type iso9660 (ro,relatime)
  cd /mnt/cdrom/
  # 解压VMwaretools.xxx.tar.gz到指定目录下(存储系统安装软件的安装包):/opt/
  tar -zvxf VMwaretools.x.tar.gz -C /opt/
  # 进入vmware-tools-distrib目录并执行脚本.pl
  cd vmware-tools 
  ./vmware***.pl
  # 一直回车，直到“enjoy”
  
  
```

## 注意事项

1、运行.pl文件时出现

![image-20210912012456032](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210912012456032.png)

缺少 **perl （脚本语言）**

```
 yum install -y kernel-devel perl gcc
```

