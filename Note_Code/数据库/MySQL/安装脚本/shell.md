# shell

```shell
#!/bin/bash
mkdir /usr/local/mysql
cd /usr/local/mysql
wget http://mirrors.sohu.com/mysql/MySQL-5.6/mysql-5.6.48.tar.gz
tar -zxvf mysql-5.6.48.tar.gz
cd mysql-5.6.48
cmake . -DCMAKE_INSTALL_PREFIX=/usr/local/mysql \
-DMYSQL_DATADIR=/usr/local/mysql/data \
-DSYSCONFDIR=/etc
-DMYSQL_UNIX_ADDR=/var/lib/mysql/mysql.sock  \
-DMYSQL_TCP_PORT=3306   
-DDEFAULT_CHARSET=utf8 \
-DDEFAULT_COLLATION=utf8_general_ci \
-DWITH_EXTRA_CHARSETS=all \
-DWITH_INNOBASE_STORAGE_ENGINE=1 \
-DWITH_FEDERATED_STORAGE_ENGINE=1 \
-DWITH_BLACKHOLE_STORAGE_ENGINE=1 \
-DWITHOUT_EXAMPLE_STORAGE_ENGINE=1 \
-DWITH_ZLIB=bundled \
-DWITH_SSL=yes \
-DENABLED_LOCAL_INFILE=1 \
-DWITH_EMBEDDED_SERVER=1 \
-DENABLED_DOWNLOADS=1 \
>-DWITH_DEBUG=0
echo $?
make
echo $?
make install

```

