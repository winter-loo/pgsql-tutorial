https://www.postgresql.org/docs/current/xfunc-c.html#XFUNC-C-TYPE-TABLE

| SQL Type                      | C Type          | Defined In                             |
| ----------------------------- | --------------- | -------------------------------------- |
| `boolean`                     | `bool`          | `postgres.h` (maybe compiler built-in) |
| `box`                         | `BOX*`          | `utils/geo_decls.h`                    |
| `bytea`                       | `bytea*`        | `postgres.h`                           |
| `"char"`                      | `char`          | (compiler built-in)                    |
| `character`                   | `BpChar*`       | `postgres.h`                           |
| `cid`                         | `CommandId`     | `postgres.h`                           |
| `date`                        | `DateADT`       | `utils/date.h`                         |
| `float4` (`real`)             | `float4`        | `postgres.h`                           |
| `float8` (`double precision`) | `float8`        | `postgres.h`                           |
| `int2` (`smallint`)           | `int16`         | `postgres.h`                           |
| `int4` (`integer`)            | `int32`         | `postgres.h`                           |
| `int8` (`bigint`)             | `int64`         | `postgres.h`                           |
| `interval`                    | `Interval*`     | `datatype/timestamp.h`                 |
| `lseg`                        | `LSEG*`         | `utils/geo_decls.h`                    |
| `name`                        | `Name`          | `postgres.h`                           |
| `numeric`                     | `Numeric`       | `utils/numeric.h`                      |
| `oid`                         | `Oid`           | `postgres.h`                           |
| `oidvector`                   | `oidvector*`    | `postgres.h`                           |
| `path`                        | `PATH*`         | `utils/geo_decls.h`                    |
| `point`                       | `POINT*`        | `utils/geo_decls.h`                    |
| `regproc`                     | `RegProcedure`  | `postgres.h`                           |
| `text`                        | `text*`         | `postgres.h`                           |
| `tid`                         | `ItemPointer`   | `storage/itemptr.h`                    |
| `time`                        | `TimeADT`       | `utils/date.h`                         |
| `time with time zone`         | `TimeTzADT`     | `utils/date.h`                         |
| `timestamp`                   | `Timestamp`     | `datatype/timestamp.h`                 |
| `timestamp with time zone`    | `TimestampTz`   | `datatype/timestamp.h`                 |
| `varchar`                     | `VarChar*`      | `postgres.h`                           |
| `xid`                         | `TransactionId` | `postgres.h`                           |