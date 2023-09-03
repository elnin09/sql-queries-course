#### REGEX MATCHING


##### PATTERN MATCHING
- PATTERN MATCHING

  - `.` matches any single charecter
    
    - eg a , b ,5 ' ' all of these match above single charecter

  - `.ab+`  
    -  '+' means any occurence of previous string
    - 2ab 2abb 3abb 4abb 5ab all of these match

  - `1a?b`

    - '?' means 0 or 1 occurence of a charecter 
    - it means that it shoud start with 1 and then followed by 0 or 1 charecter of a
    - 1ab 1b 1abb 

  -  `\d` matches any digit
  -  `\w` matches any alphanumeric and both case (lower and upper)

  - `a\w\d`

    - ab2 , aA2 , aB3, aD5 are match
    - Ab2 not a match as A is in caps
  
  - `\d+\w?`
  
    - This means 1 or more occurences of digit followed by 0 or 1 occurence of a word/upper case/digit
    - asc no match
    - 2 is a match
    - 234 is a match
    - abb no match doesn't have 1 digit 
    - 1d is a match

   - ` \d\d\w* `

     - This needs two digits followed by any number of alphanumeric charecter
     - 22 match
     - 1a not a match
     - 222 a match
     - aa not a match

    - `2+\w?\d*`

      - This translates to starting with one or more occurence of 2 followed by 0 or 1 alphanumeric charecter followed by any number of digits

      - 22a1 valid
      - 21 valid
      - 2aaab1 not valid
      - 1a not valid
      - aa not valid

    - `{m}` `{m,}` `{m,n}` intervals matching
    
      - Above means exactly m occurence
      - Between m and infinity 
      - Third means between m and n occurence
    
    - `\d{2}\w{3}`

      - 234sf matches above
      - 11abc is a match
      - 34Dwc is a match
      - Ad4 is not a match
      - 24d e doesn't count because ' ' doesn't match \w

    -  ` \d{1,}\w? `
      
       - This means one ore more digit followed by 0 or 1 alphanumeric charecter
       -  Matches 2 2a 34523e

    - `\d{1,3}-\d{2}`

       - THis means 1-3 digits followed by - and then exactly 2 digits after that


    - Matching charecter list and groups
     
     - Syntax `[...]` match charecter list
     - Sybtax `[^...]` non matching charecter list
     - `(...)` subexpression or grouping
     - You can also specify a range using - eg a-z means a-z

    - `[a-z][a-z][a-b]`

      - zza match zzb match zzd not a match

    -  `[ade][^erf]`

       - Means two charecters first can be a,d or e and second anything other than e,r,f  

    -  `[abcde][^a-z](end)`

       - It means starts with any of abcde then contains any char other than a-z (lower case) and then last three charecters are end

       - a9end a1end and so on

    <br>
    
    - Pattern Matching OR pipe operator

      - (abc|def) means either abc or def
      - (a|b|c|d){4}
      - Means any of a,b,c,d any 4 times

    - Pattern matching back reference
      
      - `\n` this means nth sub pattern
      - `(aa)(bb)\2`  aabbbb
      - `[abc](aa)(bb)\2` aaabbbb baabbbb caabbbb


    - Pattern matching `\`

     - ` (aa)(bb)\* `

      -  aabb* matches so basically \ is used for special charecters


    - `^`` and `$` 
    
     - ^ matches start of string
     - $ matches end of string
     - `^(abe)[a-z]` matches abea abeb abec  .... abez
     - `col[123]$`  matches col1 col2 col3 

<br> <br>

##### REGEXP FUNCTIONS IN SQL

  - REGEXP_LIKE
   
    - Used in where clause
    - Doesn't need to match the entire string
    - REGEXP_LIKE(expression,pattern [,match parameter])
    - `SELECT * from stores where regexp_like(physical_address,'[A-Z]{2} \d{5}$')`
    - `SELECT * from stores where regexp_like(physical_address,'[A-Z]{2} \d{5}')`
    - `SELECT * from customers where regexp_like(full_name,'^Ste(ph|v)en')`

<br><br>

  - REGEXP_INSTR

    - Returns an int stating the location of a regex expression in a string
    - If regex not present then return 0
    - `REGEXP_INSTR(string,pattern[,start_position][,nth_appearance])`
    - First two params are mandatory and other two params are optional and 
    - By default start_position is start of string and nth_apperance is
    the first appearance of the string 

    - `SELECT * from eba_countries where regexp_instr(name,'n') = 7`
    Query where 7th charecer in name is n
    - `SELECT * from eba_countries where regexp_instr(name,'\(.*\)') > 0`
    Query where name has open and close parenthesis

<br> <br>

- REGEXP_SUBSTR

  - Extracts a substring from a string that specifies a pattern

  - `REGEXP_SUBSTR(string,pattern[,start_position][,nth_appearance])`

  -  `SELECT * from eba_countries where regexp_substr(name,'^A.*a$') = name1`
  Finding all countries where name starts and ends with an A

  - `SELECT regexp_substr(name,'^\w+ ')  from eba_countries `
    Finding first word of country which contain multiple words


- REGEXP_REPLACE

   - Replace a sequence of charecters with another sequence of charecters
   - `REGEXP_REPLACE(string,pattern,replacement_string[,start_position][,nth_appearance])`

   - `SELECT FULL_NAME, regexp_replace(email_address,'@\w$','@internalmail.com') from customers;`
   - `SELECT FULL_NAME, regexp_replace(email_address,'\.','-') from customers; --replace . with - in email` 

   - `SELECT FULL_NAME, concat('intermail@',regexp_replace(email_address,'@.*','')) from customers;`

   - `SELECT FULL_NAME, regexp_replace(email_address,'(.*)(@)(.*)','\3\2\1') from customers;`

   - Above example shows usage of back reference and can be very useful in case of regexp_replace . 

<br><br>

- Class Meta Charecter 

  - `[[:alnum]]`
  - `[[:alpha]]`
  - `[[:digit]]`
  - `[[:punct]]`

  - for `\d` we can use `[[:digit]]`


     


   

