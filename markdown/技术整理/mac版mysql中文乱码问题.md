编码问题需要设置成统一的编码格式才行，命令行进去[MySQL](http://lib.csdn.net/base/mysql)
**mysql -u root -p**
输入命令查看当前[数据库](http://lib.csdn.net/base/mysql)的编码格式：

**show variables like 'character_set_%';**

如果和下面一致就没问题：
mysql> show variables like 'character_set_%';
+--------------------------+--------------------------------------------------------+
| Variable_name            | Value                                                  |
+--------------------------+--------------------------------------------------------+
| character_set_client     | utf8                                                   |
| character_set_connection | utf8                                                   |
| character_set_database   | utf8                                                   |
| character_set_filesystem | binary                                                 |
| character_set_results    | utf8                                                   |
| character_set_server     | utf8                                                   |
| character_set_system     | utf8                                                   |
| character_sets_dir       | /usr/local/mysql-5.6.26-osx10.8-x86_64/share/charsets/ |
+--------------------------+--------------------------------------------------------+
8 rows in set (0.00 sec)
如果不一致修改如下：
**1、停止mysql服务；**
**2、找到/etc/my.cnf文件，增加配置，并保存：**
**[mysqld]character-set-server=utf8[client]default-character-set=utf8**
**3、启动mysql服务；**
****
**注意如果还是不能插入汉字，重新创建数据库和表就可以了。**
