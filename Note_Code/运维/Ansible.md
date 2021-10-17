# Ansible

![](H:\笔记\Note_Code\images\Ansible.png)

## 一、Ansible简介（做什么的？怎么实现？需要注意什么？）

### 1、Ansible是什么

- 一种配置管理工具


[^配置管理]:编写一个描述所有服务器状态的配置文件，并使用工具确保所有服务器都保持在这个状态上

- 也可用于==批量部署==，（编配？置备？）


### 2、Ansible如何运作？

- 通过Ansible的脚本（script）– *playbook*，来实现配置管理、部署

  ```
  #!/bin/bash
  # ex.yml
  ---
  - name: 例
    hosts: all
    remote_user: root
    tasks:
      - name: install nginx
        apt: name=nginx
      - name: xxx
        module: args
  ```

  

  - playbook：描述了哪些==主机==需要配置，以及需要在那些主机上运行的有序==任务列表==![image-20210916161549873](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210916161549873.png)

  ```shell
  ansible-playbook <playbook.yml>
  # 执行playbook
  ```

  - playbook脚本执行规则，按照任务清单==顺序==执行：

    a.  基于模块和参数==（执行一个task）==生成==Python程序==（脚本）

    b.  将此程序复制到==远程服务器==

    c.  在远程服务器上执行此程序

### 3、Ansible的特点

- **易读： **基于YAML语法的playbook脚本

- **远程主机无依赖**

- **基于推送模式： **本地更改playbook – 运行新的playbook – 连接服务器并执行那些改变服务器状态的模块

  [^基于拉取模式]: 服务器上的agent程序==定时==向配置管理中心==报备==状态并==拉取==相应配置信息

- **管理小规模集群**

- **内置模块**

- **幂等性：** 同一服务器多次执行同一个playbook时，不会出现报错/bug等

- 

### 4、注意事项

- Ansible按照顺序执行任务列表每一个任务
- 执行下一个任务前，Ansible会等待所有主机完成上一个任务

## 二、Ansible安装

### 1、EPEL源的yum安装

```
# 导入EPEL源
yum install epel-release -y
# 安装ansible模块
yum install ansible -y
```

### 2、源码包安装

### 3、pip安装

```
# 1、直接使用python包管理工具 pip安装Ansible
$ sudo pip install ansible
# 2、不使用root，安装ansible到 Python virtualenv--使用 pipsi 工具安装


```

### 4、Git安装

```
# 最新版本安装
git clone https://github.com/ansible/ansible.git --rescursive

```

## 三、Ansible架构

1. **inventory（清单）文件**

   - 主机清单：单个/群组，IP/域名

     ```
     # 独立主机:主机名 [inventory行为参数]
     delaware.example.com ansible_ssh_port=2222
     # 群组形式:
     [vagrant]
     # 别名形式！
     vagrant1 ansible_ssh_host=127.0.0.1 ansible_ssh_port=2222
     等价于<hostname>:port
     	127.0.0.1：2222
     
     ```

   - **inventory行为参数**（主机/群组变量）

     |             名称             |  默认值  |        备注         |
     | :--------------------------: | :------: | :-----------------: |
     |      *ansible_ssh_host*      | 主机名字 |  ssh目的主机名/IP   |
     |       ansible_ssh_port       |    22    |     ssh目标端口     |
     |       ansible_ssh_user       |   root   | ssh登录使用的用户名 |
     |       ansible_ssh_pass       |   none   |  ssh认证使用的密码  |
     |      ansible_connection      |  smart   | ansible连接主机方式 |
     | ansible_ssh_private_key_file |   none   |  ssh认证使用的私钥  |

   - 📕**动态inventory**

   - 主机/群组变量

     - **inventory内部**

       ```
       # 单主机变量设置
       web1.example.com color=red
       web2.example.com color=yellow
       
       # 群组变量设置[<groupname>:vars]
       [all:vars]
       color=green
       ntp_server=ntp.ubuntu.com
       ```

     - 在各自文件中？– – 存在与**host_vars**目录 和**group_vars**目录的==变量文件==

       -  ansible会使用YAML格式解析这些变量文件

         ```
         例：组变量文件
         路径：/home/lee/playbook/group_vars/production
         db_name=lee_production
         db_user=lee
         db_password=123
         db_primary_host=web.example.com
         另一种格式,YAML字典
         db:
         	name: lee_production
         	user: lee
         	password: 123
         	primary:
         		host: web.example.com
         	
         ```

         

## 四、Ansible之模块modules

### 必知信息

- Ansible模块文档

  ```
  # 查看service模块的文档
  $ ansible-doc service
  ```

  

### 1、命令执行模块

### 2、 文件类型（copy、fetch、压缩/解压缩、文件属性

### 3、各类管理模块（主机、服务、用户/组）

### 4、计划任务模块

### 5、系统信息模块



## 五、Ansible剧本–playbook

![image-20210916161655808](C:\Users\LGB\AppData\Roaming\Typora\typora-user-images\image-20210916161655808.png)

### 1、简介

- 执行配置管理服务的脚本文件

- 一个playbook是由一组==*play*==组成的列表

  - play（必须包含一组 ‘name & tasks’ ）

    ```
    - name: Configure webserver with nginx
      hosts: webserver
      sudo: True
      task:
        - name: install nginx
          yum: name=nginx
    - name 
    ```

    旧版语法：action 

    ```
    task:
      - name: install nginx
        action: yum name=nginx
    ```

### 2、Play

```yaml
- name: Configure webserver with nginx and tsl
  hosts: webserver
  sudo: True
  vars:
    key_file: /etc/nginx/ssl/nginx.key
    ...
    
```

#### 		说明

1）**vars**区段：声明自定义变量并赋值

​			**调用**：{{braces}}   ：braces用变量替换

```yaml

- name: copy TLS key
  copy: src=files/nginx.key dest={{ key_file }} owner=root mode=0600
```



### 3、YAML语言

1）特点

2）语法

```yaml
# 1、文件起始
---
# 2、注释
# This is a YAML comment
# 3、数据类型
	# 字符串：无需引号
	this is a sentence 
	# 布尔型
	True/False
	# 列表:'-'或者[  ]
	- this 
	- is
	- list
	# 字典:'key: value'或者{ , }
	province： anhui
	city： chuzhou 
	# 换行/折行：'>'
	
```

### 3、模板（一般应用在配置文件方面）

- [Jinja2](http://jinja2.pocoo.org)
- 基于Jinja2模板引擎的一种文本文件，Jinja2语法

### 4、Handlers和Notify

- 应用在playbook中，是一种特殊的额条件触发机制

  - 当task发生变化（changed），则触发notify（通知），task根据通知内容启动对应的==handler==

- handlers和task很像（如下）

  ```yaml
  tasks:
    - name: install nginx
      yum: name=nginx
    - name: set configure file
      file: srt=xx dest=xxx
      notify: restart nginx
      ...
  
  handlers:
    - name: restart nginx
      service: name=nginx state=restart
      ...
  ```

- 注意：handler按照play中被定义的顺序执行，比如handlers放置play末尾，前面tasks的执行优先级高于它！ 即使在tasks中被通知多次（多次执行 notify），它仍然是最后执行，并且只执行一次！

### 4、Playbook的文件列表

- **/playbook/templates/: **存放模板文件

### 5、Ansible运行后变化

### 6、变量

- 主机与群组变量

  

## 六、Ansible角色–roles

### 1、简介

### 2、Roles的目录编排

### 3、创建roles

### 4、调用roles



## 七、Ansible的实战