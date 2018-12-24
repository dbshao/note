1.  停止 mysql server.  通常是在 '系统偏好设置' > MySQL > 'Stop MySQL Server'
2.  打开终端，输入：     sudo /usr/local/mysql/bin/mysqld_safe --skip-grant-tables
3.  打开另一个新终端，输入:    
 sudo /usr/local/mysql/bin/mysql -u root     
UPDATE mysql.user SET authentication_string=PASSWORD('新密码') WHERE User='root';    
 FLUSH PRIVILEGES;     
\q
4.  重启

*以上方法针对 MySQL V5.7.9, 旧版的mysql请使用：UPDATE mysql.user SET Password=PASSWORD('新密码') WHERE User='root';

mySql的三个命令：
sudo /usr/local/mysql/support-files/mysql.server start
sudo /usr/local/mysql/support-files/mysql.server stop
sudo /usr/local/mysql/support-files/mysql.server restart

登录命令：
/usr/local/mysql/bin/mysql -u root -p
