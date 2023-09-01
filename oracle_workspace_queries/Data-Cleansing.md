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

