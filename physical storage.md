---
tags: beginners, tutorial, postgresql, database
---

# Terms
- _relation_
	table or index
- _tuple_
	a row of data

# Structure
Every table and index is stored as an array of _pages_ of a fixed size (usually 8 kB, although a different page size can be selected when compiling the server). In a table, all the pages are logically equivalent, so a particular item (row) can be stored in any page. In indexes, the first page is generally reserved as a _metapage_ holding control information, and there can be different types of pages within the index, depending on the index access method.
	
page = page_header + page_payload
page_payload  = tuple_pointers + free_space + tuple_n + ... + tuple_3 + tuple_2 + tuple_1 + special_space
tuple = tuple_header + tuple_payload

tuple_payload is the actual row of user data.

more refer to [official documentation](https://www.postgresql.org/docs/current/storage-page-layout.html)


# Management
参考 【PostgreSQL指南：内幕探索】第 5 章 并发控制

## tuple operations
- add
- delete
	只是从逻辑上标记为删除
- update
	`delete` and `add`

## free space management
- use `FSM` file
- use `VM` file