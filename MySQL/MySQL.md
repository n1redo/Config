**第一步**

官网：https://dev.mysql.com/downloads/installer/

下载安装包。



**第二步**

解压到指定位置。

==在环境变量path中添加mysql路径。==

MySQL5需要创建`my.ini`文件

```ini
【mysqld】
#设置3306端口
port=3306
#设置mysql的安装目录
basedir=
#设置mysql数据库的数据的存放目录
datadir=\data
#允许最大连接数
max_connections=200
#允许连接失败的次数。这是为了防止有人从该主机试图攻击数据库系统
max_connect_errors=10
#服务端使用的字符集默认为UTF8
character-set-server=utf8
#创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
#默认使用“mysql_native_password”插件认证
default_authentication_plugin=mysql_native_password

【mysql】
#设置mysql客户端默认字符集
default-character-set=utf8
【client】
#设置mysql客户端连接服务端时默认使用的端口
port=3306
default-character-set=utf8
```



**第三步**

以管理员的方式打开cmd命令行，输入以下指令。

```
# 初始化数据库，并设置默认root为空，初始化完成后，在mysql根目录中会自动生成data文件
mysqld --initialize-insecure --user=mysql

# 为windows安装mysql服务，默认服务名为mysql,出现service successfully installed.表示配置完成
mysqld -install

# 启动数据库
net start mysql

# 不用输入密码直接回车
mysql -u root -p

# 修改密码
alter user user() identified by "密码";

# 退出
mysql>quit;

# 关闭数据库
net stop mysql

```

