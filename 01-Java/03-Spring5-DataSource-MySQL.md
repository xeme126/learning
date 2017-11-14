

url="jdbc:mysql://localhost:3306/test?characterEncoding=UTF-8&amp;autoReconnectForPools=true&amp;rewriteBatchedStatements=true&amp;useCursorFetch=true&amp;defaultFetchSize=20"

mysql超时时间分为time_out和interactive_timeout,ubuntu修改mysql配置：/etc/mysql/my.cnf
在[mysqld]添加如下设置：
wait_timeout = 86400  
interactive_timeout = 86400
设置完成后，用:show variables like '%timeout%' 查看有没有设置成功，注意到单引号。
设置完成后，重启mysql服务：sudo service mysql restart.