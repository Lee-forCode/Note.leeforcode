# 有关systemctl命令详解

>
>
>参考博客：https://blog.csdn.net/skh2015java/article/details/94012643
>
>​					https://www.cnblogs.com/zwcry/p/9602756.html

## 一、systemcl的由来

### 1、Linux最初启动进程`init`

- 启动慢，串行启动
- 只负责启动脚本

### 2、systemd

- systemd中的`d`=`daemon`守护进程缩写

- **systemd是Linux系统最新的初始化系统(init),作用是提高系统的启动速度，尽可能启动较少的进程，更多进程并发启动。**

- `systemd`对应一组系统管理命令：`systemctl`

## 二、systemd有关命令详解

>
>
>

### 1、systemctl – – 系统管理命令

### 2、systemd-analyze – – 启动耗时

### 3、hostnamectl – – 查看当前主机信息、修改主句名…

### 4、localctl – – 查看本地设置：语言

### 5、timedatectl – – 当前时区设置

### 6、loginctl – – 查看登录用户

## 三、Unit – – systemd所管理的系统资源统称

### 1、12种Unit

- `Service unit`：系统服务
- `Target unit：`多个 Unit 构成的一个组
- `````Device Unit`````：硬件设备
- `Mount Unit`：文件系统的挂载点
- Automount Unit：自动挂载点
- Path Unit：文件或路径
- Scope Unit：不是由 Systemd 启动的外部进程
- Slice Unit：进程组
- Snapshot Unit：Systemd 快照，可以切回某个快照
- Socket Unit：进程间通信的 socket
- Swap Unit：swap 文件
- Timer Unit：定时器

### 2、命令

#### 1）系统units – – `systemctl list-units`

#### 2）unit状态 – – `systemctl status`

#### 3）管理 – – start \ stop

#### 4）依赖 – – systemctl list-dependencies

## 四、Unit配置文件

>
>
>`systemd`默认从`/etc/systemd/system/ --> /usr/lib/systemd/system`读取配置文件

### 1、`systemctl enable`相当于将上面两个文件建立`符号链接`，相当于开机自启动

### 2、查看配置文件 列表– – `systemctl list-units-files`

```
# 查看配置文件
systemctl cat httpd.service
```

## 五、日志管理 – `journalctl`

>
>
>可以查看所有日志