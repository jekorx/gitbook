# Maven（Linux环境下）

> 以Centos 7.4，Maven 3.6.0 为例  

```bash
# 下载二进制文件压缩包http://mirrors.shu.edu.cn/apache/maven/maven-3/
# 或者直接下载然后通过ftp工具上传到服务器
wget http://mirrors.shu.edu.cn/apache/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz

# 解压
tar -xzvf apache-maven-3.6.0-bin.tar.gz

# 修改profile
vim /etc/profile
export M2_HOME=/home/apache-maven-3.6.0 # 最后面添加
export PATH=$PATH:$JAVA_HOME/bin:$M2_HOME/bin # 修改PATH

# 重新初始化profile
source /etc/profile

# 查看配置结果
mvn -v
```