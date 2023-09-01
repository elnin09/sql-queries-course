#### Data Cleansing

##### COALESCE

- Take two or more expressions and returns the first expression that is not-null from the list of expressions
- Ordering is important
- Only if all expressions are null , coalesce is null
- The datatypes can't be dynamic
- Syntax

```SQL
COALESCE(expresion1,expression2,expression3,expression4)

SELECT store_name,web_address,coalesce(web_address,store_name) as webaddress_first , 
coalesce(store_name,web_address) as storenamefirst from stores;

```

##### NVL

- Replaces null value from an expression with a specified string. It takes 2 params, expression and replacement string.

- If first param a character then convert replacement string to char

- If first param is numneric, oracle determines which argument has the higher numeric precedence implicitly converts the other argument to that datatype

- Sytanx  
``` SQL
nvl()
SELECT emp.* , nvl(comm,0) from emp; -- this works

SELECT emp.* , nvl(comm,'0') from emp; -- this also works

SELECT emp.* , nvl(comm,'char') from emp; -- this won't work as comm is of int type 
```


##### TRIM
- Trim enables you to trim leading or trailing charecters(or both) from a charecter string.

``` SQL
trim(leading|trailing|both trim_charecter from trim_source) 
SELECT trim(' ' from  ' whitespace  ') from emp;

-- In above query space is trailing charecter we haven't specidied leading or trailing hence we woul remove all whitespaces from the string
```

##### LPAD and RPAD

- It pads the left or the right of a string until it reaches a specified length
- If length is already higher thatn specified length it is trimmed

```SQL
SELECT * from rpad(emp.job,6,'X') from emp;

-- MANAGE
-- ANALYS
-- ANALYS
-- CLERKX -> X is appended
SELECT * from lpad(emp.job,6,'X') from emp;
-- MANAGE
-- ANALYS
-- ANALYS
-- XCLERK -> x is appended from the left
```


##### GREATEST / LEAST

- Greatest function returns the greatest value in a list
- The least function returns the lowest value in a list of expressions
- First expression used to determine data type

``` SQL
greatest(expression1,expression2,expression3)
SELECT emp.* greatest(least(sal,3000),1000) from emp;
-- this would give me a salary between 1000 and 3000

```

##### PIVOT

- Pivot allows you to rotate rows into columns in a table
- Here you can't have a subquery inside in condition you have to provide specfic values
- Here aggregate function is on population and the pivot component is region_id


``` SQL
SELECT * from 
(SELECT population,region_id,region_sub_id from eba_countries)
pivot (sum(population) for region_id in (10,20,30,40,50));
```

- To explain above we are actually considering all the values of subregion_id and some values of region_id(as columns)

  - We basically make region_id as column and the aggregate function is sum 
  - All the columns that we select apart from aggregate and pivot column will appear in the query
  - Here we are selection region_sub_id, columns (10,20,30,40,50) so total 6 columns 
  - The values for columns region_sub_id would be the orignal values

  - Also think on what would happen if it were a group by clause

    - If we have three rows and 4(3 fields + 1) column(aggr) in group by output , then pivot would have 5 colums and 1 row

    
    ``` SQL
    Col1 Col2 Col3  Aggr
    A     B    C1   10 
    A     B    C2   12
    A     B    C3   13

    -- post pivot would be 
    Col1  Col2   C1  C2  C3
    A     B     10  12  13
    ```

- Anothe example

```SQL
SELECT * from 
(SELECT sal,job,deptno from emp)
pivot (sum(sal) for job in ('PRESIDENT','MAANGER','ANALYST','CLERK','SALESMAN') )
```

- Output of above will have 6 columns one with deptno and other 5 will be values in job present in the condition
- The value of column will be sum(sal) and null if no such records exist

##### UNPIVOT

- Unpivot transforms columns to rows

```SQL

SELECT * FROM TABLE
UNPIVOT(MEASURE_COL FOR NEW_COL_NAME IN (PIVOT_COL_LIST))

SELECT * from avg_test_scores
unpivot(avg_score for subject in (MATHS,SCIENCE,ENGLISH))

```

- This would basically convert the columns into rows and would do reverse of what is shown in the pivot example above