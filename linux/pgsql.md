# PostgreSQL

> 以Centos 7.4，PostgreSQL11.x为例  

### 安装

```bash
# 1、官网获取下载地址
# https://www.postgresql.org/download/linux/redhat/

# 2、安装存储库RPM
yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# 3、安装pgsql服务
yum install -y postgresql11 postgresql11-server

# 4、初始化数据库
/usr/pgsql-11/bin/postgresql-11-setup initdb

# 5、启动
systemctl start postgresql-11

# 6、设置自动启动
systemctl enable postgresql-11

# 7、设置postgres用户密码
# 删除原密码
sudo passwd -d postgres
# 设置新密码
sudo -u postgres passwd
```

### 配置

```bash
# 1、修改配置
vim /var/lib/pgsql/11/data/postgresql.conf

# 修改监听地址，允许远程访问
listen_addresses = '*' # line.59
# 修改端口，云服务器配置开放端口，默认端口：5432
port = 5432 # line.63
```

### 卸载

```bash
# 1、查询安装的包
rpm -qa | grep postgresql

# 2、卸载，多个包，空格隔开
yum remove <包1 包2 包3>
```

### 创建数据库、用户

```bash
# 1、切换到postgres用户
su postgres

# 2、启用sql shell
psql
```

```sql
-- 3、创建用户
CREATE USER <user> WITH PASSWORD 'password';

-- 修改密码
ALTER USER <user> WITH PASSWORD 'password';

-- 4、创建数据库
CREATE DATABASE <db>;

-- 5、授权
GRANT ALL PRIVILEGES ON DATABASE <db> TO <user>;
```

```bash
# 6、返回shell
\q

# 7、退出shell，切换回root用户
su root

# 8、配置允许远程访问
vim /var/lib/pgsql/11/data/pg_hba.conf

# 最末尾加入
# TYPE DATABASE USER ADDRESS METHOD
host <db> <user> 0.0.0.0/0 md5

# 9、重启服务
systemctl restart postgresql-11
```


### 基本语法

```bash
# 查看所有数据库
\l

# 切换当前数据库
\c <db>

# 查看当前数据库下所有表
\d

# 退出数据库返回shell
\q
```