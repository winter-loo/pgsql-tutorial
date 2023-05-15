# Concepts

In computer science, a _window_ includes a range of values over a stream of values.

... 1 2 3 |< 4 5 6 7 8 >| 9 10 11 12 ...

`... 1 2 3 ... 9 10 11 12 ...` is a stream of values.
`4 5 6 7 8` is a windows surrounded by `|<` and `>|`

Window can move from left to right. So the next window is like:

... 1 2 3  4 |< 5 6 7 8 9 >| 10 11 12 ...

In PostgreSQL, a simple query returns many rows of data, i.e., a stream of values. And you could _partition_ the rows of data by a key. Even further, inside each partition, you could perform some calculation over several values or whole values. That range of values could be called a window.

Aggregate function turn groups of data into a single output row, however, window function outputs its result for each row.

# Window bound
In PostgreSQL, the window is create by `OVER (...)` clause. There are many ways to express a window bound. Here are three common methos: 
1. whole partition as a whole big window by `OVER ()` 
2. right window bound is determined by current row, left window bound is the start of the partition, and this window includes some values which equal to the current value. This kind of window is created by `OVER (order by <column name>)`
3. more advanced and lengthy way to set window bound is `OVER (order by <column name> range between <prev_offset> preceding and <next_offset> following)`. The offset is relative to the value of current row. Say, the value of current row is 5, `prev_offset` is 0 and `next_offset` value is 1, then the window should include values equal 5 or 6.
More reference to [SYNTAX-WINDOW-FUNCTIONS](https://www.postgresql.org/docs/current/sql-expressions.html#SYNTAX-WINDOW-FUNCTIONS)


# Show me the code

First, create some data:

```sql
create table foo(a int, b int);
insert into foo select 1, generate_series(10, 12);
insert into foo select 2, generate_series(10, 12);
insert into foo select 3, generate_series(12, 14);
insert into foo select 5, generate_series(20, 22);
```

The simplest case, use the whole data as a big window,
```sql
select a, sum(b) OVER () from foo;
```

The next case, let's use `order by` inside `(...)`:
```sql
select a, sum(b) OVER (order by b) from foo;
```

Partition the data,
```sql
select a, sum(b) OVER (partition by a) from foo;
```

and order the partition data,
```sql
select a, sum(b) OVER (partition by a order by b) from foo;
```

Define custom window,
```sql
select a, sum(a) OVER (order by a range between 0 preceding and 1 following) from foo;
```

