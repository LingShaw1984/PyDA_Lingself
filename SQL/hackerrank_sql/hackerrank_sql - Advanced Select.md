# hackerrank_sql -  Advanced Select 

##  The PADS 

Generate the following two result sets:

1. Query an *alphabetically ordered* list of all names in **OCCUPATIONS**, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: `AnActorName(A)`, `ADoctorName(D)`, `AProfessorName(P)`, and `ASingerName(S)`.  

2. Query the number of ocurrences of each occupation in **OCCUPATIONS**. Sort the occurrences in *ascending order*, and output them in the following format:    

   ```
   There are a total of [occupation_count] [occupation]s.
   ```

   where `[occupation_count]` is the number of occurrences of an occupation in **OCCUPATIONS** and `[occupation]` is the *lowercase* occupation name. If more than one *Occupation* has the same `[occupation_count]`, they should be ordered alphabetically.

**Note:** There will be at least two entries in the table for each type of occupation.

**Input Format**

The **OCCUPATIONS** table is described as follows: ![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png) *Occupation* will only contain one of the following values: **Doctor**, **Professor**, **Singer** or **Actor**.

**Sample Input**

An **OCCUPATIONS** table that contains the following records:

![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816608-0b4d01d157-2.png)

**Sample Output**

```
Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.
```

**Explanation**

The results of the first query are formatted to the problem description's specifications. 
 The results of the second query are ascendingly ordered first by number of names corresponding to each profession ( ). 

**Solution：**

```mysql
/*
Enter your query here.
*/
SELECT CONCAT(Name, CASE 
    WHEN Occupation = 'Doctor' THEN '(D)'
    WHEN Occupation = 'Professor' THEN '(P)'
    WHEN Occupation = 'Singer' THEN '(S)'
    ELSE '(A)'
END)
FROM OCCUPATIONS
ORDER BY Name;

SELECT CONCAT('There are a total of ', COUNT(occupation), ' ', LOWER(SUBSTR(occupation, 1, 1)), SUBSTR(occupation,2,LENGTH(occupation)), 's.')
FROM OCCUPATIONS
GROUP BY occupation
ORDER BY COUNT(occupation) ASC, occupation;
```



##  Occupations 

[Pivot](https://en.wikipedia.org/wiki/Pivot_table) the *Occupation* column in **OCCUPATIONS** so that each *Name* is sorted alphabetically and displayed underneath its corresponding *Occupation*. The output column headers should be *Doctor*, *Professor*, *Singer*, and *Actor*, respectively.

**Note:** Print **NULL** when there are no more names corresponding to an occupation.

**Input Format**

The **OCCUPATIONS** table is described as follows:

![img](https://s3.amazonaws.com/hr-challenge-images/12889/1443816414-2a465532e7-1.png)

*Occupation* will only contain one of the following values: **Doctor**, **Professor**, **Singer** or **Actor**.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12890/1443817648-1b2b8add45-2.png)

**Sample Output**

```
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria
```

**Explanation**

The first column is an alphabetically ordered list of Doctor names. 
 The second column is an alphabetically ordered list of Professor names. 
 The third column is an alphabetically ordered list of Singer names. 
 The fourth column is an alphabetically ordered list of Actor names. 
 The empty cell data for columns with less than the maximum number of  names per occupation (in this case, the Professor and Actor columns) are filled with **NULL** values.

**Solution**

```mysql
SET @r1=0, @r2=0, @r3=0, @r4=0;
SELECT MIN(Doctor), MIN(Professor), MIN(Singer), MIN(Actor)
FROM(
  SELECT CASE WHEN Occupation='Doctor' THEN (@r1:=@r1+1)
              WHEN Occupation='Professor' THEN (@r2:=@r2+1)
              WHEN Occupation='Singer' THEN (@r3:=@r3+1)
              WHEN Occupation='Actor' THEN (@r4:=@r4+1) END AS RowNumber,
         CASE WHEN Occupation='Doctor' THEN Name END AS Doctor,
         CASE WHEN Occupation='Professor' THEN Name END AS Professor,
         CASE WHEN Occupation='Singer' THEN Name END AS Singer,
         CASE WHEN Occupation='Actor' THEN Name END AS Actor
  FROM OCCUPATIONS
  ORDER BY Name
) TEMP
GROUP BY RowNumber;
```

PS: The solution come from: https://github.com/RamAlapure/SQL/blob/master/Advanced-Select/OCCUPATIONS.sql



##  Binary Tree Nodes 

You are given a table, *BST*, containing two columns: *N* and *P,* where *N* represents the value of a node in *Binary Tree*, and *P* is the parent of *N*.

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818507-5095ab9853-1.png)

Write a query to find the node type of *Binary Tree* ordered by the value of the node. Output one of the following for each node:

- *Root*: If node is root node.
- *Leaf*: If node is leaf node.
- *Inner*: If node is neither root nor leaf node.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443818467-30644673f6-2.png)

**Sample Output**

```
1 Leaf
2 Inner
3 Leaf
5 Root
6 Leaf
8 Inner
9 Leaf
```


 **Explanation**

The *Binary Tree* below illustrates the sample:

![img](https://s3.amazonaws.com/hr-challenge-images/12888/1443773633-f9e6fd314e-simply_sql_bst.png)

**Solution:**

```mysql
/*
Enter your query here.
*/
SELECT N, IF(P IS NULL, 'Root', IF((SELECT COUNT(*)
                                    FROM BST
                                    WHERE P = B.N)>0, 'Inner', 'Leaf'))
FROM BST AS B
ORDER BY N;
```



##  New Companies 

Amber's conglomerate corporation just acquired some new companies. Each of the companies follows this hierarchy: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458531031-249df3ae87-ScreenShot2016-03-21at8.59.56AM.png)

Given the table schemas below, write a query to print the *company_code*, *founder* name, total number of *lead* managers, total number of *senior* managers, total number of *managers*, and total number of *employees*. Order your output by ascending *company_code*.

**Note:**

- The tables may contain duplicate records.
- The *company_code* is string, so the sorting should not be **numeric**. For example, if the *company_codes* are *C_1*, *C_2*, and *C_10*, then the ascending *company_codes* will be *C_1*, *C_10*, and *C_2*.

------

**Input Format**

The following tables contain company data:

- *Company:* The *company_code* is the code of the company and *founder* is the founder of the company. ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458531125-deb0a57ae1-ScreenShot2016-03-21at8.50.04AM.png)
- *Lead_Manager:* The *lead_manager_code* is the code of the lead manager, and the *company_code* is the code of the working company. ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534960-2c6d764e3c-ScreenShot2016-03-21at8.50.12AM.png)
- *Senior_Manager:* The *senior_manager_code* is the code of the senior manager, the *lead_manager_code* is the code of its lead manager, and the *company_code* is the code of the working company. ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534973-6548194998-ScreenShot2016-03-21at8.50.21AM.png)
- *Manager:* The *manager_code* is the code of the manager, the *senior_manager_code* is the code of its senior manager, the *lead_manager_code* is the code of its lead manager, and the *company_code* is the code of the working company. ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458534988-7fc0af46ce-ScreenShot2016-03-21at8.50.29AM.png)
- *Employee:* The *employee_code* is the code of the employee, the *manager_code* is the code of its manager, the *senior_manager_code* is the code of its senior manager, the *lead_manager_code* is the code of its lead manager, and the *company_code* is the code of the working company. ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535002-d47f63cbb4-ScreenShot2016-03-21at8.50.41AM.png)

------

**Sample Input**

*Company* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535049-2a207c44b3-ScreenShot2016-03-21at8.50.52AM.png) *Lead_Manager* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535073-919107f639-ScreenShot2016-03-21at8.51.03AM.png) *Senior_Manager* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535111-b1c48335b3-ScreenShot2016-03-21at8.51.15AM.png) *Manager* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535122-888f4bf340-ScreenShot2016-03-21at8.51.26AM.png) *Employee* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19505/1458535134-878767e0d9-ScreenShot2016-03-21at8.51.52AM.png)

**Sample Output**

```
C1 Monika 1 2 1 2
C2 Samantha 1 1 2 2
```

**Explanation**

In company *C1*, the only lead manager is *LM1*. There are two senior managers, *SM1* and *SM2*, under *LM1*. There is one manager, *M1*, under senior manager *SM1*. There are two employees, *E1* and *E2*, under manager *M1*.

In company *C2*, the only lead manager is *LM2*. There is one senior manager, *SM3*, under *LM2*. There are two managers, *M2* and *M3*, under senior manager *SM3*. There is one employee, *E3*, under manager *M2*, and another employee, *E4*, under manager, *M3*.

**Solution**:

```mysql
/*
Enter your query here.
*/
SELECT c.company_code, c.founder, 
       COUNT(DISTINCT l.lead_manager_code), COUNT(DISTINCT s.senior_manager_code),
       COUNT(DISTINCT m.manager_code), COUNT(DISTINCT e.employee_code)
FROM Company c 
JOIN Lead_Manager l ON c.company_code = l.company_code 
JOIN Senior_Manager s ON l.lead_manager_code = s.lead_manager_code
JOIN Manager m ON s.senior_manager_code = m.senior_manager_code
JOIN Employee e ON m.manager_code = e.manager_code   
GROUP BY c.company_code, c.founder
ORDER BY c.company_code;
```

##  Type of Triangle 

Write a query identifying the type of each record in the **TRIANGLES** table using its three side lengths. Output one of the following statements for each record in the table:

- **Equilateral**: It’s a triangle with 3 sides of equal length.
- **Isosceles**: It’s a triangle with 2 sides of equal length.
- **Scalene**: It’s a triangle with 3 sides of differing lengths.
- **Not a Triangle**: The given values of A, B, and C don’t form a triangle.

**Input Format**
 The **TRIANGLES** table is described as follows:

| Column | Type    |
| ------ | ------- |
| A      | Integer |
| B      | Integer |
| C      | Integer |

Each row in the table denotes the lengths of each of a triangle’s three sides.

**Sample Input**

| A    | B    | C    |
| ---- | ---- | ---- |
| 20   | 20   | 23   |
| 20   | 20   | 20   |
| 20   | 21   | 22   |
| 13   | 14   | 30   |

**Sample Output**

> Isosceles
>  Equilateral
>  Scalene
>  Not A Triangle

**Explanation**
 Values in the tuple (20,20,23) form an Isosceles triangle, because A=B.
 Values in the tuple (20,20,20) form an Equilateral triangle, because A=B=C.
 Values in the tuple (20,21,22) form a Scalene triangle, because A≠B≠C.
 Values in the tuple (13,14,30) cannot form a triangle because the  combined value of sides A and B is not larger than that of side C.

Solution:

```mysql
SELECT IF(A+B>C AND A+C>B AND B+C>A, IF(A=B AND A=C, 'Equilateral', IF(A=B OR B=C OR C=A, "Isosceles", 'Scalene')), "Not A Triangle")
FROM TRIANGLES;
```

