---
tags: beginners, tutorial, postgresql, database
---

# 架构

- 多进程
	- 为每一个客户端连接分配一个进程
	- 内部一个主进程、多个辅助进程
- 数据存储 
	- 所有的数据放在一个指定的目录中，可以用环境变量 PGDATA 表示


# 备份
- 热备份
	- 搞一个从数据库服务，异步或同步将 DDL/DML 操作在从数据库上重放
	- 使用文件系统快照完成数据备份，可以使用 [LVM](https://tldp.org/HOWTO/LVM-HOWTO/) 的快照功能。
- 冷备份
	停止服务，将 $PGDATA 目录拷贝到另一台机器上