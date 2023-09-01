#### REGEX MATCHING

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
  
  - `\d+\w?
  
    - This means 1 or more occurences of digit followed by 0 or 1 occurence of a word/upper case/digit
    - asc no match
    - 2 is a match
    - 234 is a match
    - abb no match doesn't have 1 digit 
    - 1d is a match

   - `\d\d\w*`

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


   

