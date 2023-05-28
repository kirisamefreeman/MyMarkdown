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

## 自启mysql server
## 1.打开终端并输入以下命令以编辑MySQL启动脚本：
```
sudo vim /etc/init.d/mysql
```

## 2.在编辑器中，将以下内容复制并粘贴到文件中：
```
#!/bin/bash
### BEGIN INIT INFO
# Provides:          mysql
# Required-Start:    $local_fs $remote_fs $network $syslog
# Required-Stop:     $local_fs $remote_fs $network $syslog
# Should-Start:      $syslog
# Should-Stop:       $syslog
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: MySQL Server
# Description:       MySQL Server daemon
### END INIT INFO

basedir=/opt/mysoftware/mysql
datadir=/opt/mysoftware/mysql/data
mysqld=/opt/mysoftware/mysql/bin/mysqld_safe
mysqladmin=/opt/mysoftware/mysql/bin/mysqladmin
mysql_user=mysql

# Check if binary exists
test -x $mysqld || exit 0

case "$1" in
    start)
        # Start MySQL server
        sudo -u $mysql_user $mysqld --user=$mysql_user --datadir=$datadir >/dev/null &
        ;;
    stop)
        # Stop MySQL server
        sudo -u $mysql_user $mysqladmin --user=$mysql_user --password shutdown
        ;;
    restart)
        # Restart MySQL server
        $0 stop
        sleep 1
        $0 start
        ;;
    *)
        # Print usage if invalid command is given
        echo "Usage: $0 {start|stop|restart}"
        exit 1
        ;;
esac

exit 0
```

## 3.接下来，需要对启动脚本进行一些权限设置。运行以下命令：
```
sudo chmod +x /etc/init.d/mysql
sudo update-rc.d mysql defaults
```

## 4.现在，MySQL服务器将在系统启动时自动启动。你可以使用以下命令来启动、停止或重启MySQL服务器：
```
sudo service mysql start
sudo service mysql stop
sudo service mysql restart
```

## 这样，你就无需每次重启都手动输入命令来启动MySQL服务器了。希望对你有所帮助！如有任何问题，请随时提问。

## 如果你想将 MySQL 的可执行文件路径添加到系统的环境变量中，以便可以在任何位置直接执行 mysql 命令，你可以按照以下步骤将 MySQL 添加到 /etc/profile 文件中：
## 1.打开终端并以管理员身份运行以下命令以编辑 /etc/profile 文件：
```
sudo vim /etc/profile
```

## 2.在文件末尾添加以下行（假设 MySQL 的安装路径是 /opt/mysoftware/mysql）：
```
export PATH=/opt/mysoftware/mysql/bin:$PATH
```

## 3.运行以下命令以使更改生效：
```
source /etc/profile
```

## 或者重新启动终端窗口。

## 现在，你应该能够在任何位置直接执行 mysql 命令来登录到 MySQL。请注意，这将使得 mysql 命令在所有用户中都可用。如果你只想在特定用户中使其可用，可以将上述步骤中的 /etc/profile 更改为 ~/.bashrc（如果使用的是 Bash shell）或 ~/.profile（如果使用的是其他 shell）。
