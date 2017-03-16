# mysql

## 配置公网访问
**绑定公网地址**  
```shell
[mysqld]
bind-address = 0.0.0.0
```
**配置 root 用户公网访问**  
```sql
-- mysql 5.6+ test
Grant all on *.* to 'root'@'%' IDENTIFIED by 'password';

-- 新建一个用户
CREATE USER 'im_rw'@'%' IDENTIFIED BY 'password';

-- 配置用户只能读取指定库
Grant all on im.* to 'im_rw'@'%' IDENTIFIED by 'password';

-- 查看权限
show grants for im_rw;

-- 记得刷新权限配置
flush privileges;
```

## CURD
**删除数据库**  
```sql
-- 库名如果含有特殊字符，可用 `` 包含
Drop database `33939`;
```
