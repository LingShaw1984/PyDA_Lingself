# hackerrank_sql - Basic Select 

##  Revising the Select Query I 

Query all columns for all American cities in **CITY** with populations larger than `100000`. The *CountryCode* for America is `USA`.  

```mysql
SELECT *
FROM CITY
WHERE (POPULATION > 100000)
AND COUNTRYCODE = 'USA';
```

##  Revising the Select Query II

Query the names of all American cities in **CITY** with populations larger than `120000`. The *CountryCode* for America is `USA`.  

```mysql
SELECT NAME
FROM CITY
WHERE (POPULATION > 120000)
AND COUNTRYCODE = 'USA';
```

## Select All

Query all columns (attributes) for every row in the **CITY** table.

```mysql
SELECT *
FROM CITY;
```

## Select By ID

Query all columns for a city in **CITY** with the *ID* `1661`.

```mysql
SELECT *
FROM CITY
WHERE ID = 1661;
```

## Japanese Cities’ Attributes

Query all attributes of every Japanese city in the **CITY** table. The *COUNTRYCODE* for Japan is `JPN`.

```mysql
SELECT *
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```

## Japanese Cities’ Names

Query the names of all the Japanese cities in the **CITY** table. The *COUNTRYCODE* for Japan is `JPN`. 

```mysql
SELECT NAME
FROM CITY
WHERE COUNTRYCODE = 'JPN';
```

## Weather Observation Station 1

Query a list of *CITY* and *STATE* from the **STATION** table.

```mysql
/*
Enter your query here.
*/

SELECT CITY, STATE
FROM STATION;
```

## Weather Observation Station 3

Query a list of *CITY* names from **STATION** with even *ID* numbers only. You may print the results in any order, but must exclude duplicates from your answer.

```mysql
/*
Enter your query here.
*/

SELECT DISTINCT CITY
FROM STATION
WHERE (ID % 2 = 0);
```

## Weather Observation Station 4

Let  be the number of *CITY* entries in **STATION**, and let  be the number of distinct *CITY* names in **STATION**; query the value of  from **STATION**. In other words, find the difference between the total number of *CITY* entries in the table and the number of distinct *CITY* entries in the table. ![1571132080592](1571132080592.png)

```mysql
/*
Enter your query here.
*/

SELECT COUNT(CITY)- COUNT(DISTINCT CITY)
FROM STATION;
```

## Weather Observation Station 5

Query the two cities in **STATION** with the shortest and longest *CITY* names, as well as their respective lengths (i.e.: number of characters  in the name). If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

```mysql
/*
Enter your query here.
*/

SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) ASC, CITY
LIMIT 1;

SELECT CITY, LENGTH(CITY)
FROM STATION
ORDER BY LENGTH(CITY) DESC, CITY
LIMIT 1;
```

## Weather Observation Station 6

Query the list of *CITY* names starting with vowels (i.e., `a`, `e`, `i`, `o`, or `u`) from **STATION**. Your result *cannot* contain duplicates. 

```mysql
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE 'a%'
OR CITY LIKE 'e%'
OR CITY LIKE 'i%'
OR CITY LIKE 'o%'
OR CITY LIKE 'u%';
```

## Weather Observation Station 7

Query the list of *CITY* names ending with vowels (a, e, i, o, u) from **STATION**. Your result *cannot* contain duplicates. 

```mysql
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE CITY LIKE '%a'
OR CITY LIKE '%e'
OR CITY LIKE '%i'
OR CITY LIKE '%o'
OR CITY LIKE '%u';
```

## Weather Observation Station 8

Query the list of *CITY* names from **STATION** which have vowels (i.e., *a*, *e*, *i*, *o*, and *u*) as both their first *and* last characters. Your result cannot contain duplicates.

```mysql
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE (CITY LIKE 'a%' 
       OR CITY LIKE 'e%'
       OR CITY LIKE 'i%' 
       OR CITY LIKE 'o%' 
       OR CITY LIKE 'u%') 
AND (CITY LIKE '%a' 
     OR CITY LIKE '%e' 
     OR CITY LIKE '%i' 
     OR CITY LIKE '%o' 
     OR CITY LIKE '%u');      
     
-- I don't know why can't use 'REGEXP'
```

## Weather Observation Station 9

Query the list of *CITY* names from **STATION** that *do not start* with vowels. Your result cannot contain duplicates.

```mysql
-- The First Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE 'A%'
AND CITY NOT LIKE 'E%'
AND CITY NOT LIKE 'I%'
AND CITY NOT LIKE 'O%'
AND CITY NOT LIKE 'U%';
```

```mysql
-- The Second Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(SUBSTR(CITY, 1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
AND LOWER(SUBSTR(CITY, 1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
```

## Weather Observation Station 10

Query the list of *CITY* names from **STATION** that *do not end* with vowels. Your result cannot contain duplicates.

```mysql
The Frist Way
/*
Enter your query here.
*/
-- The Second Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE UPPER(SUBSTR(CITY, -1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
AND LOWER(SUBSTR(CITY, -1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
```

```mysql
-- The Second Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE CITY NOT LIKE '%A'
AND CITY NOT LIKE '%E'
AND CITY NOT LIKE '%I'
AND CITY NOT LIKE '%O'
AND CITY NOT LIKE '%U';
```

## Weather Observation Station 11

Query the list of *CITY* names from **STATION** that either do not start with vowels or do not end with vowels. Your result cannot contain duplicates.

```mysql
/*
Enter your query here.
*/
-- The Second Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE (
        UPPER(SUBSTR(CITY, -1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
    AND LOWER(SUBSTR(CITY, -1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
    )
OR (
        UPPER(SUBSTR(CITY, 1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
    AND LOWER(SUBSTR(CITY, 1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
    )
```

## Weather Observation Station 12

Query the list of *CITY* names from **STATION** that *do not start* with vowels and *do not end* with vowels. Your result cannot contain duplicates.

```mysql
/*
Enter your query here.
*/
-- The Second Way
/*
Enter your query here.
*/
SELECT DISTINCT CITY
FROM STATION
WHERE (
        UPPER(SUBSTR(CITY, -1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
    AND LOWER(SUBSTR(CITY, -1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
    )
AND (
        UPPER(SUBSTR(CITY, 1, 1)) NOT IN ('A', 'E', 'O', 'U', 'I')
    AND LOWER(SUBSTR(CITY, 1, 1)) NOT IN ('a', 'e', 'o', 'u', 'i')
    )
```

## Higher Than 75 Marks

Query the *Name* of any student in **STUDENTS** who scored higher than  *Marks*. Order your output by the *last three characters* of each name. If two or more students both have names ending in the  same last three characters (i.e.: Bobby, Robby, etc.), secondary sort  them by ascending *ID*. ![1571137274487](1571137274487.png)

```mysql
/*
Enter your query here.
*/
SELECT Name
FROM STUDENTS 
WHERE Marks > 75 
ORDER BY SUBSTR(Name, LENGTH(Name)-2, 3), ID;
```

## Employee Names

Write a query that prints a list of employee names (i.e.: the *name* attribute) from the **Employee** table in alphabetical order.

**Input Format**

The **Employee** table containing employee data for a company is described as follows: 

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where *employee_id* is an employee's ID number, *name* is their name, *months* is the total number of months they've been working for the company, and *salary* is their monthly salary.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458558202-9a8721e44b-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**

```
Angela
Bonnie
Frank
Joe
Kimberly
Lisa
Michael
Patrick
Rose
Todd
```

Solution:

```mysql
/*
Enter your query here.
*/
SELECT name
FROM EMPLOYEE
ORDER BY name;   
```

## Emplovee Salaries

Write a query that prints a list of employee names (i.e.: the *name***Employee**

**Input Format**

The **Employee** table containing employee data for a company is described as follows: 

![img](https://s3.amazonaws.com/hr-challenge-images/19629/1458557872-4396838885-ScreenShot2016-03-21at4.27.13PM.png)

where *employee_id* is an employee's ID number, *name* is their name, *months* is the total number of months they've been working for the company, and *salary* is the their monthly salary.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/19630/1458558612-af3da3ceb7-ScreenShot2016-03-21at4.32.59PM.png)

**Sample Output**

```
Angela
Michael
Todd
Joe
```

**Explanation**

*Angela* has been an employee for 

 month and earns 

*Michael* has been an employee for 

 months and earns 

*Todd* has been an employee for 

 months and earns 

*Joe* has been an employee for 

 months and earns 

We order our output by ascending *employee_id*.

Solution:

```mysql
/*
Enter your query here.
*/
SELECT NAME
FROM EMPLOYEE
WHERE SALARY > 2000 
AND MONTHS < 10
ORDER BY EMPLOYEE_ID;  
```

