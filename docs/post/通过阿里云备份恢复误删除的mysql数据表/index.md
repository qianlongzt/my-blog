在有阿里云 RDS 备份的情况下，恢复误删除的 MySQL 数据表

阿里云 RDS 环境 MySQL 5.6，恢复环境 5.7

## 数据找回

还好 Aliyun 数据库有备份文件（数据目录备份），我下载后使用数据表的对应文件 `.ibd` `.frm` 进行[还原](https://www.zixundingzhi.com/jizhu/4edb1d2fc656decd.html)(16日0:37)，

但是出现
`RROR 1808 (HY000): Schema mismatch (Table has ROW_TYPE_DYNAMIC row format, .ibd file has ROW_TYPE_COMPACT row format.)`错误(16日1:26)

[解决](http://veryyoung.me/blog/2016/06/21/restore-innodb-data-physical.html)后出现`error 2013 (hy000): lost connection to mysql server during query`错误

我发觉可能数据版本的原因，阿里云RDS是5.6，我用来还原数据库MySQL是5.7，
最后我决定，把MySQL的数据目录全部替换成阿里云的备份，然后在 `skip grant tables` 的情况下启动数据库，这个时候可以读出数据

但是在导出数据库的时候会出现 ```Couldn't execute 'SHOW VARIABLES LIKE 'gtid_mode': Table 'performance_schema.session_variables' doesn't exist (1146)``` 错误，

运行`mysql_upgrade -u root -p --force`
就可以[解决](http://grx.no/kb/2016/11/15/mysqldump-couldnt-execute-show-variables-like-gtid_mode-table-performance_schema-session_variables-doesnt-exist-1146/)(16日3:20)

至此，前一天（15日6点）数据已经找回。

后面下载binlog，通过 `mysqlbinlog --database database  test-150-bin.000002 >database.sql` 发现没有出现数据更改操作（16日3:42）


## 总结与教训

1. MySQL 5.6 与 5.7 版本`ibd`似乎不兼容
1. 备份数据用SQL语句最好
1. 最好不要手动修改数据库
1. 重要操作前一定要备份