# Vagrant



## 一、Vagrant（以win为例）

1. 简介

   - [Vagrant官网](https://www.vagrantup.com/)
   - 快速便捷的安装虚拟机，搭建开发/测试环境
   - 无图形化界面，单纯通过==命令行==实现

2. 安装

   - 官网下载对应操作系统的版本

   - Vagrant安装无需特别注意，按照提示安装即可

   - Vagrant安装程序会自动将安装路径加入到==PATH==中去

     ```
     vagrant -v
     ```

3. 命令（vagrant [options]）

|  参数   |                备注                 |
| :-----: | :---------------------------------: |
|   ✨up   |             开启虚拟机              |
|  halt   | 关闭虚拟机，相当于虚机终端 poweroff |
| reload  | 重载虚拟机，重载 vagrantfile的内容  |
| destroy |     删除虚拟机，包括虚拟机文件      |
| suspend |             暂停虚拟机              |
| resume  |             恢复虚拟机              |
|  以上   |      在vagrantfile所在目录执行      |
|   box   |             box相关操作             |
|   ssh   |             ssh相关操作             |

1. 配置

   - 后续创建虚拟机要导入镜像（即box），默认存储在==**.vagrant.d**==目录下（Windows默认在家目录下的该文件夹）

   - 更改==box==默认存储位置，添加系统环境变量中

     ![image-20210920103358776](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210920103358776.png)

   - 参考笔记：http://www.linuxeye.com/Linux/2125.html

   

   - 2️⃣添加box：==add==后面跟的是下载的box存放的路径；==--name centos7==命名

     

2. **创建虚拟机**

## 二、VirtualBox 和 VMware

1. 简介（VirtualBox为例）

   - [VirtualBox官网](https://www.virtualbox.org/)

   - 跨平台的虚拟化操作系统，适应多种操作系统

2. 安装

   - 官网下载主程序，按照步骤安装即可，无特别注意
   - ✨扩展程序包下载（在主程序安装完成后安装）

3. **配置**

   - 创建虚拟机需要占用过多的磁盘，选择一个足够大小的磁盘存放虚拟机文件
   - 更改==默认虚拟电脑位置==：‘管理 - - 全局设定’
   - ![image-20210920102324954](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210920102324954.png)

## 三、Windows下，Vagrant + VitualBox统一部署环境

1. 部署步骤

   ✅**下载镜像（box)**

   - 1️⃣官网下载box到本地（速度可能较慢）：[Vagrant的boxes库](https://app.vagrantup.com/boxes/search)

   - 2️⃣Centos官网下载：https://cloud.centos.org/centos/

     [^注意]: 选择需要的版本，在其目录下有个 ==vagrant==目录，选择==**.box文件**==下载

   ✅**导入box**

   - 1️⃣终端输入下面代码(可选）：第一次运行时，会在==VAGRANT_HOME==指定的目录下生成若干文件和文件夹，有一个 ==**boxes文件夹**==就是存放box的

     ```
     # 查看box列表
     vagrant box list
     ```

   - 2️⃣添加box：==add==后面是box存放的路径，==- -name==是命名

     ```
     # 添加镜像，并命名
     vagrant box add f:boxes\CentOS-7.box --name centos7
     # 查看是否添加成功
     vagrant box list
     ```

   ✅**创建虚拟机**

   - 1️⃣创建目录，用来存放初始化所需的文件==vagrantfile==

     ```dos
     # 创建
     mkdir demo
     # 进到目录下
     cd demo
     # 初始化，init后的参数（可写/可不写）表示我们所要用到的 box
     vagrant init centos7
     ```

   ✅**启动虚拟机（初始化的目录下启动）**

   ```
   vagrant up
   ```

   - ==Setting the name of the VM（虚拟机名称）==: demo1_default_1632108452580_2196（可改）
   - 网卡（Adapter）：**Adapter 1: nat**，第一块网卡，NAT模式，固定的
   - 端口转发（Forwarding ports）:**22 (guest) => 2222 (host) (adapter 1)**，把虚拟机 ==22端口==映射到宿主机 ==2222 端口==，这样可以通过 ==127.0.0.1：2222==访问虚拟机（访问？）
   - SSH地址：127.0.0.1:2222
   - ==SSH用户名==：==vagrant==，这里使用==private key==登录
   - ==密码登录虚拟机==：用户名 vagrant/root 密码：vagrant

   ✅查看虚拟机状态

   ```
   vagrant status
   ```

   ✅登录虚拟机（默认）

   ```
   vagrant ssh
   # 什么名字/ID？
   ❗ vagrant ssh [name|id] 
   ```

   ✅有关虚拟机的操作

   ```
   # 停止虚拟机
   vagrant halt
   # 暂停虚拟机
   vagrant suspend
   # 恢复虚拟机
   vagrant resum
   # 重载虚拟机，重载 vagrantfile 中的信息
   vagrant reload
   # 删除虚拟机，删除整个虚拟机文件
   vagrant destroy
   ```

2. 注意事项

   - ​	登陆虚拟机（SSH），vagrant ssh 命令后追加 [name|id]是什么意思？

## 四、Vagrantfile

1. 简介

   - Ruby语法编写的配置文件
   - 文件名大小写严格：Vagrantfile
   - [官方文档](https://www.vagrantup.com/docs)

2. 初始的==Vagrantfile==

   ```ruby
   # -*- mode: ruby -*-
   # vi: set ft=ruby :
   
   
   Vagrant.configure("2") do |config|
     # 对应的box文件，必须写
     config.vm.box = "centos7_1"
     
   end
   
   ```

3. 自定义配置 Vagrantfile

   - **配置端口转发**：将虚拟机的某个端口（guest），映射到主机的某个端口（host），就可以通过宿主机访问虚拟机的服务

     ✅比如：默认映射，``22（guest）=> 2222（host) (adapter 1)``通过``127.0.0.1:2222 ``直接访问虚拟机的ssh服务，等价于访问虚机的·`22	`口

     ❓如何更改默认SSH映射？

     ```ruby
     config.vm.network "forwarded_port", guest: 22, host: 2222, id: "ssh", disable: "true"
     config.vm.network "forwarded_port", guest: 22, host: 22222
     ```

     ❗ 此功能并不实用，如启用多个虚拟机，容易出现宿主机上端口冲突问题

   - **配置私有网络**:`config.vm.network "private_network", ip: "IP"`

     - 建议取消``DHCP`分配IP：Virtualbox–管理 - 主机网络管理 - 取消DHCP

     ```ruby
     # IP对应virtualBox Host-Only网段
     config.vm.network "private_network", ip: "192.168.58.10"
     # 使用DHCP模式（不推荐）
     config.vm.network "private_network", type: dhcp
     ```

     ❗修改后`vagrant reload`重载虚拟机，设置才能生效

   - **配置公有网络**(==没必要==)：对应着桥接网络，将==虚机暴露在公共网络==，这样没必要也，不安全！

     ```
     # 配置public network
     config.vm.network "public_network"
     ```

     

   - **配置同步文件夹**：将本地目录中的==项目文件==同步到 虚拟机上

     1️⃣`Rsyncing folder: /cygdrive/d/vagrant_all/demo1/ => /vagrant`

     - `/cygdrive/d/vagrant_all/demo1/`：对应本地主机文件，`Vagrantfile`所在的目录

     - `/vagrant`：虚机内部的位置

     - `Rsyncing`：同步方式 `Rsync`

     - 缺点：单向的，只能从宿主机拷贝文件到虚机；一次性的，只有在开启虚拟机时同步

     - 更改同步目录：明确同步类型type，系统默认同步类型是 `vboxsf`

       ```
       config.vm.synced_floder "../data", "/vagrant/data", type: "rsync"
       ```

       

   - **更改虚拟机规格**（Provider）

     ✅``vagrant 官网``提及的`provider`类型：`virtualbox`、`vmware`、`docker`、`hyper-V`；实际上`vagrant cloud`提及可供下载的box有22种：`vmware_desktop`、`vmware_workstation`、`vmware`、`vmware_fusion`等

     ```ruby
     # provider有 virtualbox
     config.vm.provider "virtualbox", do |vb|
     	vb.cpus = 2
     	vb.memory = 2048
     end
     
     ```

     ✅``Vagrant Provider`相关配置

     ```ruby
     # 头
     config.vm.provider "virtualbox" do |vb|
     	# 虚拟机名称
     	vb.name = "my_vm"
     	# 设置默认网卡类型,默认网络接口非NIC类型
     	vb.default_nic_type = ""
     	# XboxManager自定义
         vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
     
     ```

     ``✅ vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]``

     - 虚机 CPU使用率不得超过 50%
     - `:id`：用来代替虚机的ID，而不需要明确的ID

## 五、Virtualbox  Guest Addition安装

1. 下载
   - https://download.virtualbox.org/virtualbox
2. 安装
   - 

