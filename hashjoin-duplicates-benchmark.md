## benchmark/micro/join/hashjoin_dups_rhs.benchmark

This document is about understanding the `benchmark/micro/join/hashjoin_dups_rhs.benchmark` file in the duckdb repository. It looks like the following:

```text
1  # name: benchmark/micro/join/hashjoin_dups_rhs.benchmark
2  # description: Inner hash join using string comparisons with 4x duplicates on the rhs and 4096x duplicates on the lhs
3  # group: [join]
4  
5  name Inner Join (dups on rhs)
6  group join
7  
8  load
9  create table t1 as select 'verylargestring' || range % 32768 i from range(131072);
10 create table t2 as select 'verylargestring' || range % 32768 i from range(134217728);
11 
12 run
13 select count(*) from t1 join t2 using (i)
14 
15 result I
16 536870912
```

The code consists of two headers: lines `1-3` and lines `5-6`, where the latter appears to be some kind of a shortened version of the former. The name and description refer to the term `lhs` and `rhs`, which refer to the left-hand side, and right-hand side of the join operation. 

Line `8` declares the start to the SQL statements which generate the tables that the benchmark will be run on, which are locate in lines `9-10`. These create tables `t1` and `t2`. These feature a column named `i`, that looks like "verylargestring0", "verylargestring1", ... "verylargestring 32767", "verylargestring0", ..., where each of the 32768 unique strings repeat 4 times in table t1 and 4096 times in table t2. 

Line `12` finally declares the SQL statement that is run for the benchmark. It joins t1 (=lhs of the join) with t2 (=rhs). The operation count(*) counts the amount of output rows. Since each of the 32,768 distinct keys in t1 (4 copies each) matches 4096 copies in t2, you get 32,768 x 4 x 4096 = 536,870,917 joined rows.

The file is referred to by `.github/regression/micro_extended.csv`. I'm assuming that's where the benchmark "regression" testing is done".
