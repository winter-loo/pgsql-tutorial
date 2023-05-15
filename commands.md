---
tags: beginners, tutorial, postgresql, database
---


# shell commands

## DUMP DATA
```shell
pg_dump mydb > mydb.sql

pg_dump -h 192.168.0.123 -U ldd mydb  > mydb.sql

# custom dump format
pg_dump -Fc -h 192.168.0.123 -U ldd mydb > mydb.dump

# dump specific table
pg_dump -t foo > mydb.foo.sql

# include all tables which name begins with job but not 'job_log'
pg_dump -t 'public.job*' -T public.job_log mydb > mydb.public.job.sql

# exclude all database objects but no object ends with '_log'
pg_dump -T '*_log' mydb > mydb.sql
```

## RESTORE DATA
```shell
createdb my_another_db
pg_restore -d my_another_db mydb.dump

pg_restore -h 192.168.0.123 -Uldd -C -d mydb mydb.dump
```

# psql commands
```sql
select version();

select pg_background_pid();

select current_catalog;

select inet_client_addr(), inet_client_port();

select inet_server_addr(), inet_server_port();

-- current WAL file
select pg_xlogfile_name(pg_current_xlog_location());

select pg_is_in_backup(), pg_backup_start_time();

select pg_is_in_recovery();

-- size of database, table, index
select pg_size_pretty(pg_database_size('mydb'));
-- not include index size
select pg_size_pretty(pg_relation_size('mydb.foo'));
-- include index size
select pg_size_pretty(pg_total_relation_size('mydb.foo'));
select pg_size_pretty(pg_indexes_size('mydb'));

-- cancel long running task
select pid, username, query_start, query from pg_stat_activity;
select pg_cancel_backend(567);
select pid, username, query_start, query from pg_stat_activity;
select pg_terminate_backend(567);


-- get transaction id inside a transaction
begin;
select txid_current();
end;
```