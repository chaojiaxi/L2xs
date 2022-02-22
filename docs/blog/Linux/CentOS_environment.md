## contOS-开发环境

**本系统是以contOS7.4为实验，手把手教学安装开发环境**

- **git 安装**

默认yum安装git版本，查看git版本`git --version`为1.8.3.1

```
yum install -y git
```

安装git最新版本 ， [官网](https://mirrors.edge.kernel.org/pub/software/scm/git/)下载git源码包

```ssh
# 安装wget 
yum install -y wget

# 安装所需的依赖
yum install curl-devel expat-devel gettext-devel openssl-devel zlibdevel gcc-c++ perl-ExtUtils-MakeMaker

# 进入 /usr/local ，新建一个git文件夹，进入git文件夹
cd /usr/local
mkdir git
cd git

# 不安全的方式连接至 mirrors.edge.kernel.org，使用“--no-check-certificate”
wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.26.2.tar.gz --no-check-certificate

# 解压git-2.26.2.tar.gz，命名为git2.26.2
tar -zxvf git-2.9.0.tar.gz

# make configure 失败则执行
yum -y install autoconf

# 进⼊到对应⽬录，执⾏配置、编译、安装命令
# chmod +x configure（configure权限）
make configure
./configure --prefix=/usr/local/git
make profix=/usr/local/git
make install

# 将Git加⼊环境变量,:wq 保存退出
vim /etc/profile
export PATH=$PATH:/usr/local/git/bin

source /etc/profile
git --version

```

- **node 安装**

```ssh
#final-Shell 上传文件到服务器可能因为权限不足，不建议在final-Shell上传文件，也不建议在final-Shell文件栏目李删除文件，建议使用命令行解决（rm -rf 文件夹名称），快捷简单

# 进入/usr/local 文件
cd /usr/local

# 下载最新安装包
wget https://nodejs.org/dist/v16.13.1/node-v16.13.1-linux-x64.tar.xz

# 解压
tar -xvf  node-v16.13.1-linux-x64.tar.xz

# 重命名为node
mv node-v16.13.1-linux-x64 node

# 安装node环境变量
vim /etc/profile

export PATH=$PATH:/usr/local/node/bin

source /etc/profile

# 查看版本
node -v
npm -v

```

- **mongoDB 安装**

```ssh
# 进入/usr/local 文件
cd /usr/local

# 下载最新安装包到local文件下
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.2.17.tgz

# 解压
tar -xvf mongodb-linux-x86_64-rhel70-4.2.17.tgz

# 重命名为mongoDB
mv mongodb-linux-x86_64-rhel70-4.2.17 mongoDB

# 安装node环境变量
vim /etc/profile

export PATH=$PATH:/usr/local/mongoDB/bin

source /etc/profile

# 创建数据库目录
cd /usr/local/mongoDB
touch mongodb.conf
mkdir db
mkdir log
cd log
touch mongodb.log

# 修改mongodb配置文件
vim /usr/mongodb/mongodb.conf

# 添加以下内容
port=27017 #端口
dbpath= /usr/local/mongoDB/db #数据库存文件存放目录
logpath= /usr/local/mongoDB/log/mongodb.log #日志文件存放路径
logappend=true #使用追加的方式写日志
fork=true #以守护进程的方式运行，创建服务器进程
maxConns=100 #最大同时连接数
journal=true #每次写入会记录一条操作日志（通过journal可以重新构造出写入的数据）。
#即使宕机，启动时wiredtiger会先将数据恢复到最近一次的checkpoint点，然后重放后续的journal日志来恢复。
storageEngine=wiredTiger  #存储引擎有mmapv1、wiretiger、mongorocks
bind_ip = 0.0.0.0  #这样就可外部访问了
auth = true        #校验权限

# 设置文件夹权限
cd /usr/mongodb
chmod 777 db
chmod 777 log

# 启动mongodb
mongod --config /usr/mongodb/mongodb.conf

# 通过MongoDB Campass远程连接服务器
```

- **nginx 安装**

```ssh
# 安装gcc环境
yum install gcc-c++

# 安装pcre库，用于解析正则表达式
yum install -y pcre pcre-devel

# 安装zlib解压和压缩依赖
yum install -y zlib zlib-devel

# 安装ssl安全加密协议
yum install -y openssl oppnssl-devel


# 进入/usr/local 文件
cd /usr/local

# 下载最新安装包到local文件下
wget http://nginx.org/download/nginx-1.14.2.tar.gz

# 解压
tar -xvf nginx-1.14.2.tar.gz

# 重命名为nginx
mv nginx-1.14.2 nginx

# 编译安装
./configure #生成makefile文件
make
make install #会报错，无碍

/usr/local/nginx/sbin/nginx # 此处报错是没有logs日志文件
cd /usr/local/nginx
mkdir logs
chmod 777 logs

/usr/local/nginx/sbin/nginx -t # 显示ok

# 启动
/usr/local/nginx/sbin/nginx
# 停止
/usr/local/nginx/sbin/nginx -s stop
# 修改文件之后重新加载文件
/usr/local/nginx/sbin/nginx -s reload
 
# 配置文件位于 /usr/local/nginx/conf/nginx.conf
# 输入IP地址即可访问
+
```

- **mysql 安装**

```ssh

```

