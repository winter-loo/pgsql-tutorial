# extension in c

# Hello World

Here is a step-by-step guide on how to write an extension for PostgreSQL using C:

1. Download and install the PostgreSQL server and development libraries on your machine.
2. Create a new directory for your extension and navigate into it.
3. Create a new file called 'Makefile' with the following content:
	```makefile
	EXTENSION = hello_world
	MODULE_big = hello_world
	OBJS = hello_world.o
	DATA = hello_world--1.0.sql
	
	PG_CONFIG = pg_config
	PGXS := $(shell $(PG_CONFIG) --pgxs)
	include $(PGXS)
	```

4. Create a new file called 'hello_world.c' with the following content:
	```c
	#include "postgres.h"
	#include "fmgr.h"
	#include "utils/builtins.h"
	
	PG_MODULE_MAGIC;
	
	PG_FUNCTION_INFO_V1(hello_world);
	
	Datum
	hello_world(PG_FUNCTION_ARGS)
	{
	  char *str = "Hello, world!";
	  PG_RETURN_TEXT_P(cstring_to_text(str));
	}
	```
	This code defines a new function called 'hello_world' that returns a text value.

5. Create a new file called 'hello_world.control' with the following content:
	```
	# extension_name extension
	comment = 'hello world'
	default_version = '1.0'
	module_pathname = '$libdir/hello_world'
	relocatable = true
	```

6. Create a new file called ‘hello_world—1.0.sql’ with the following content:
	```sql
	CREATE OR REPLACE FUNCTION hello_world()
	RETURNS text
	-- 1. module path to the library filename without extension, here is just the filename
	-- 2. function name
	AS 'hello_world', 'hello_world'
	LANGUAGE C STRICT;
	```
	
7. Add the control file to the same directory as your C file and Makefile.
8. Run `make` in the terminal to build your extension.
9. Run `sudo make install` to install your extension into the PostgreSQL server.
10. Connect to your PostgreSQL server and run the following command:
	```sql
	CREATE EXTENSION hello_world;
	select hello_world();
	```

[code here](https://github.com/winter-loo/snippets-pgsql/tree/main/hello_world)



# Deal with more data types

## text

## array

## record

## table



# Trigger

https://github.com/pgq/pgq

RegisterXactCallback(my_xact_callback, NULL); 



# Synchronization

shared memory and LWLocks