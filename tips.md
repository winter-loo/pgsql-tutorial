---
tags: beginners, tutorial, postgresql, database
---

- 以行的方式显示结果
在 psql 中输入 `\x` 开启 expanded display, 再次输入 `\x` 关闭 expanded display. 如果你只想看列名，则在 select 查询后，输入 `\gdesc`.

- show window function result with fixed precision and fixed scale.
	```sql
	select n, (avg(n) over())::numeric(10, 4) as total_avg, (avg(n) over(order by n))::numeric(10, 4) from foo;
	```