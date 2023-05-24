## 1.下载安装文件：
```
wget https://dev.mysql.com/get/Downloads/MySQL-8.0/mysql-8.0.33-linux-glibc2.28-x86_64.tar.gz
```

## 2.解压文件：
```
tar -xvf mysql-8.0.33-linux-glibc2.28-x86_64.tar.gz
```

## 3.将解压后的文件夹移动到 /opt/mysoftware 目录下：
```
sudo mv mysql-8.0.33-linux-glibc2.28-x86_64 /opt/mysoftware/mysql
```

## 4.安装 libaio 软件包：

### -对于 Ubuntu/Debian 系统：
```
sudo apt-get install libaio1
```
### -对于 CentOS/RHEL 系统：
```
sudo yum install libaio
```
### -对于 Manjaro/Arch 系统：
```
sudo pacman -S libaio
```

## 5.创建 "mysql" 用户：
```
sudo useradd -r mysql
```

## 6.为 "mysql" 用户设置正确的用户组：
```
sudo usermod -aG mysql mysql
```

## 7.确保 MySQL 安装目录 /opt/mysoftware/mysql 的所有权归 "mysql" 用户所有：
```
sudo chown -R mysql:mysql /opt/mysoftware/mysql
```

## 8.进入 MySQL 安装目录：
```
cd /opt/mysoftware/mysql
```

## 9.初始化 MySQL 数据目录：
```
sudo -u mysql bin/mysqld --initialize --basedir=/opt/mysoftware/mysql --datadir=/opt/mysoftware/mysql/data
```

## 10.启动 MySQL 服务器：
```
sudo -u mysql bin/mysqld_safe --user=mysql &
```

## 11.连接到 MySQL 服务器：(执行9.后的输出中有默认密码例如: 2023-05-23T23:03:50.833947Z 6 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: ehlVGi<S!3kp)
```
/opt/mysoftware/mysql/bin/mysql -u root -p
```

## 12.修改根用户的密码为 "123"：
```
ALTER USER 'root'@'localhost' IDENTIFIED BY '123';
```

## 13.刷新权限：
```
FLUSH PRIVILEGES;
```

## 现在，MySQL 8.0.33 版本已经安装并启动完成，并将根用户的密码设置为 "123"。你可以使用以下命令连接到 MySQL 服务器：
```
/opt/mysoftware/mysql/bin/mysql -u root -p
```
