# hackerrank_sql - Basic Join

##  Asian Population 

Given the **CITY** and **COUNTRY** tables, query the sum of the populations of all cities where the *CONTINENT* is *'Asia'*.

**Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

**Input Format**

The **CITY** and **COUNTRY** tables are described as follows:

 ![CITY.jpg](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![Country.jpg](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

Solution:

```mysql
SELECT SUM(CI.POPULATION)
FROM CITY AS CI
JOIN COUNTRY CO
ON CI.CountryCode = CO.Code
WHERE CONTINENT = 'Asia';
```



##  African Cities 

Given the **CITY** and **COUNTRY** tables, query the names of all cities where the *CONTINENT* is *'Africa'*.   

**Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

**Input Format**

The **CITY** and **COUNTRY** tables are described as follows: 

![CITY.jpg](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![Country.jpg](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

Solution:

```mysql
SELECT CI.NAME
FROM CITY AS CI
JOIN COUNTRY CO
ON CI.CountryCode = CO.Code
WHERE CONTINENT = 'Africa';
```



##  Average Population of Each Continent 

Given the **CITY** and **COUNTRY** tables, query the names of all the continents (*COUNTRY.Continent*) and their respective average city populations (*CITY.Population*) rounded *down* to the nearest integer.

**Note:** *CITY.CountryCode* and *COUNTRY.Code* are matching key columns.

**Input Format**

The **CITY** and **COUNTRY** tables are described as follows:

 ![CITY.jpg](https://s3.amazonaws.com/hr-challenge-images/8137/1449729804-f21d187d0f-CITY.jpg)

![Country.jpg](https://s3.amazonaws.com/hr-challenge-images/8342/1449769013-e54ce90480-Country.jpg)

Solution:

```
SELECT CO.Continent, FLOOR(AVG(CI.Population))
FROM CITY AS CI
INNER JOIN COUNTRY CO
ON CI.CountryCode = CO.Code
GROUP BY CO.Continent;
```



##  The Report 

You are given two tables: *Students* and *Grades*. *Students* contains three columns *ID*, *Name* and *Marks*.

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818166-a5c852caa0-1.png)

*Grades* contains the following data:

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818137-69b76d805c-2.png)

*Ketty* gives *Eve* a task to generate a report containing three columns: *Name*, *Grade* and *Mark*. *Ketty* doesn't want the NAMES of those students who received a grade lower than *8*. The report must be in descending order by grade -- i.e.  higher grades  are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name  alphabetically. Finally, if the grade is lower than 8, use "NULL" as  their name and list them by their grades in descending order. If there  is more than one student with the same grade (1-7) assigned to them,  order those particular students by their marks in ascending order.

Write a query to help Eve.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818093-b79f376ec1-3.png)

**Sample Output**

```
Maria 10 99
Jane 9 81
Julia 9 88 
Scarlet 8 78
NULL 7 63
NULL 7 68
```


 **Note**

Print "NULL" as the name if the grade is less than 8.

**Explanation**

Consider the following table with the grades assigned to the students:

![img](https://s3.amazonaws.com/hr-challenge-images/12891/1443818026-0b3af8db30-4.png)

So, the following students got *8*, *9* or *10* grades:

- *Maria (grade 10)*
- *Jane (grade 9)*
- *Julia (grade 9)*
- *Scarlet (grade 8)*

Solution:

```
SELECT IF(g.Grade<8, NULL, s.Name), g.Grade, s.Marks
FROM Students AS s
JOIN Grades AS g
ON s.Marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY g.Grade DESC, s.Name ASC, s.Marks ASC;
```

```
SELECT IF(g.Grade<8, NULL, s.Name), g.Grade, s.Marks
FROM Students AS s
JOIN Grades AS g
WHERE s.Marks BETWEEN g.Min_Mark AND g.Max_Mark
ORDER BY g.Grade DESC, s.Name ASC, s.Marks ASC;
```



##  Top Competitors 

Julia just finished conducting a coding contest, and she needs your help  assembling the leaderboard! Write a query to print the respective *hacker_id* and *name* of hackers who achieved full scores for *more than one* challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one  hacker received full scores in same number of challenges, then sort them by ascending *hacker_id*.

------

**Input Format**

The following tables contain contest data:

- *Hackers:* The *hacker_id* is the id of the hacker, and *name* is the name of the hacker. ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526776-67667350b4-ScreenShot2016-03-21at7.45.59AM.png)
- *Difficulty:* The *difficult_level* is the level of difficulty of the challenge,  and *score* is the score of the challenge for the difficulty level. ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458526915-57eb75d9a2-ScreenShot2016-03-21at7.46.09AM.png)
- *Challenges:* The *challenge_id* is the id of the challenge, the *hacker_id* is the id of the hacker who created the challenge, and *difficulty_level* is the level of difficulty of the challenge. ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527032-f9ca650442-ScreenShot2016-03-21at7.46.17AM.png)
- *Submissions:* The *submission_id* is the id of the submission, *hacker_id* is the id of the hacker who made the submission, *challenge_id* is the id of the challenge that the submission belongs to, and *score* is the score of the submission. ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527077-298f8e922a-ScreenShot2016-03-21at7.46.29AM.png)

------

**Sample Input**

*Hackers* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527241-6922b4ad87-ScreenShot2016-03-21at7.47.02AM.png) *Difficulty* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527265-7ad6852a13-ScreenShot2016-03-21at7.46.50AM.png) *Challenges* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527285-01e95eb6ec-ScreenShot2016-03-21at7.46.40AM.png) *Submissions* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19504/1458527812-479a74b99f-ScreenShot2016-03-21at8.06.05AM.png)

**Sample Output**

```
90411 Joe
```

**Explanation**

Hacker *86870* got a score of *30* for challenge *71055* with a difficulty level of *2*, so *86870* earned a full score for this challenge.

Hacker *90411* got a score of *30* for challenge *71055* with a difficulty level of  *2*, so *90411* earned a full score for this challenge.

Hacker *90411* got a score of *100* for challenge *66730* with a difficulty level of *6*, so *90411* earned a full score for this challenge.

Only hacker *90411* managed to earn a full score for more than one challenge, so we print the their *hacker_id* and *name* as 2 space-separated values.

Solution：

```mysql
/*
Enter your query here.
*/
SELECT h.hacker_id, h.name
FROM Submissions AS s 
JOIN Hackers AS h ON s.hacker_id = h.hacker_id
JOIN Challenges AS c ON s.challenge_id = c.challenge_id
JOIN Difficulty AS d ON c.difficulty_level = d.difficulty_level
WHERE s.score = d.score
GROUP BY h.hacker_id, h.name
HAVING COUNT(*)>1
ORDER BY COUNT(*) DESC, h.hacker_id;
```



##  Ollivander's Inventory 

Harry Potter and his friends are at Ollivander’s with Ron, finally replacing Charlie’s old broken wand.

Hermione decides the best way to choose is by determining the minimum number of gold galleons needed to buy each non-evil wand of high power  and age. Write a query to print the *id*, *age*, *coins_needed*, and *power* of the wands that Ron’s interested in, sorted in order of descending *power*. If more than one wand has same power, sort the result in order of descending *age*.

**Input Format**

The following tables contain data on the wands in Ollivander’s inventory:

- *Wands*: The *id* is the id of the wand, *code* is the code of the wand, *coins_needed* is the total number of gold galleons needed to buy the wand, and *power* denotes the quality of the wand (the higher the *power*, the better the wand is).

![wands_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/wands_0.png)

- *Wands_Property*: The *code* is the code of the wand, *age* is the age of the wand, and *is_evil* denotes whether the wand is good for the dark arts. If the value of *is_evil* is 0, it means that the wand is not evil. The mapping between *code* and *age* is one-one, meaning that if there are two pairs, (code1, age1) and (code2, age2), then code1 ≠ code2 and age1 ≠ age2.

![wands_property_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/wands_property_0.png)

------

**Sample Input**

*Wands* Table:

![wands_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/wands_1.png)

*Wands_Property* Table:

![wands_property_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/wands_property_1.png)

**Sample Output**

> 9 45 1647 10
>  12 17 9897 10
>  1 20 3688 8
>  15 40 6018 7
>  19 20 7651 6
>  11 40 7587 5
>  10 20 504 5
>  18 40 3312 3
>  20 17 5689 3
>  5 45 6020 2
>  14 40 5408 1

**Explanation**

The data for wands of age 45 (code 1):

![explanation_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/explanation_1.png)

- The minimum number of galleons needed for wand(age=45, power=2) = 6020
- The minimum number of galleons needed for wand(age=45, power=10) = 1647

The data for wands of age 40 (code 2):

![explanation_2](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/explanation_2.png)

- The minimum number of galleons needed for wand(age=40, power=1) = 5408
- The minimum number of galleons needed for wand(age=40, power=3) = 3312
- The minimum number of galleons needed for wand(age=40, power=5) = 7587
- The minimum number of galleons needed for wand(age=40, power=7) = 6018

The data for wands of age 20 (code 4):

![explanation_4](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/explanation_4.png)

- The minimum number of galleons needed for wand(age=20, power=5) = 504
- The minimum number of galleons needed for wand(age=20, power=6) = 7651
- The minimum number of galleons needed for wand(age=20, power=8) = 3688

The data for wands of age 17 (code 5):

![explanation_5](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Ollivander-s-Inventory/explanation_5.png)

- The minimum number of galleons needed for wand(age=17, power=3) = 5689
- The minimum number of galleons needed for wand(age=17, power=10) = 9897

Solution:

```mysql
SELECT id, age, m.coins_needed, m.power 
FROM (SELECT code, power, MIN(coins_needed) AS coins_needed 
      FROM Wands 
      GROUP BY code, power) AS m
JOIN Wands AS w ON m.code = w.code AND m.power = w.power AND m.coins_needed = w.coins_needed
JOIN Wands_Property AS p ON m.code = p.code
WHERE p.is_evil = 0
ORDER BY m.power DESC, age DESC;
```



##  Challenges 

Julia asked her students to create some coding challenges.  Write a query to print the *hacker_id*, *name*, and the  total number of challenges created by each student. Sort your results by the total number of challenges in descending order. If more than one  student created the same number of challenges, then sort the result by *hacker_id*. If more than one student created the same number of challenges and the  count is less than the maximum number of challenges created, then  exclude those students from the result.

**Input Format**

The following tables contain challenge data:

- *Hackers:* The *hacker_id* is the id of the hacker, and *name* is the name of the hacker. ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521004-cb4c077dd3-ScreenShot2016-03-21at6.06.54AM.png)
- *Challenges:* The *challenge_id* is the id of the challenge, and *hacker_id* is the id of the student who created the challenge. ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521079-549341d9ec-ScreenShot2016-03-21at6.07.03AM.png)

------

**Sample Input 0**      

*Hackers* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521384-34c6866dae-ScreenShot2016-03-21at6.07.15AM.png) *Challenges* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521410-befa8e1cd9-ScreenShot2016-03-21at6.07.25AM.png)

**Sample Output 0**     

```
21283 Angela 6
88255 Patrick 5
96196 Lisa 1
```

**Sample Input 1**

*Hackers* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521469-87036deea3-ScreenShot2016-03-21at6.07.48AM.png) *Challenges* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521490-358215cf0b-ScreenShot2016-03-21at6.07.58AM.png)

**Sample Output 1**

```
12299 Rose 6
34856 Angela 6
79345 Frank 4
80491 Patrick 3
81041 Lisa 1
```

**Explanation**

For *Sample Case 0*, we can get the following details: 
 ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521677-fd04c384c0-ScreenShot2016-03-21at6.07.38AM.png) 
 Students 5077 and 62743 both created 4 challenges, but the maximum number of challenges created is 6  so these students are excluded from the result. 

 For *Sample Case 1*, we can get the following details: 
 ![img](https://s3.amazonaws.com/hr-challenge-images/19506/1458521836-24039e7523-ScreenShot2016-03-21at6.08.08AM.png) 
 Students  12299 and 34856 both created 6 challenges. Because 6 is the maximum number of challenges created, these students are included in the result. 

Solution:

```mysql
SELECT c.hacker_id, h.name, COUNT(c.challenge_id) AS counts 
FROM Hackers AS h 
JOIN Challenges AS c ON h.hacker_id = c.hacker_id
GROUP BY c.hacker_id, h.name
HAVING counts = (SELECT COUNT(c1.challenge_id)
                 FROM Challenges AS c1
                 GROUP BY c1.hacker_id
                 ORDER BY COUNT(*) DESC
                 LIMIT 1)
OR counts NOT IN (SELECT COUNT(c2.challenge_id)
                  FROM Challenges AS c2
                  GROUP BY c2.hacker_id
                  HAVING c2.hacker_id <> c.hacker_id)
ORDER BY counts DESC, c.hacker_id;
```



##  Contest Leaderboard 

You did such a great job helping Julia with her last coding contest challenge that she wants you to work on this one, too!

The total score of a hacker is the sum of their maximum scores for all of the challenges. Write a query to print the *hacker_id*, *name*, and total score of the hackers ordered by the descending score. If more than one hacker achieved the same total score, then sort the result by  ascending *hacker_id*. Exclude all hackers with a total score of 0 from your result.

**Input Format**

The following tables contain contest data:

- *Hackers*: The *hacker_id* is the id of the hacker, and *name* is the name of the hacker.

![hackers_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Contest-Leaderboard/hackers_0.png)

- *Submissions*: The *submission_id* is the id of the submission, *hacker_id* is the id of the hacker who made the submission, *challenge_id* is the id of the challenge for which the submission belongs to, and *score* is the score of the submission.

![submissions_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Contest-Leaderboard/submissions_0.png)

**Sample Input**

*Hackers* Table:

![hackers_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Contest-Leaderboard/hackers_1.png)

*Submissions* Table:

![submissions_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Contest-Leaderboard/submissions_1.png)

**Sample Output**

> 4071 Rose 191
>  74842 Lisa 174
>  84072 Bonnie 100
>  4806 Angela 89
>  26071 Frank 85
>  80305 Kimberly 67
>  49438 Patrick 43

**Explanation**

Hacker *4071* submitted solutions for challenges *19797* and *49593*, so the total score = 95 + max(43,96) = 191.

Hacker *74842* submitted solutions for challenges *19797* and *63132*, so the total score = max(98,5) + 76 = 174.

Hacker *84072* submitted solutions for challenges *49593* and *63132*, so the total score = 100 + 0 = 100.

The total scores for hackers *4806*, *26071*, *80305*, and *49438* can be similarly calculated.

Solution:

```mysql
SELECT s.hacker_id, h.name, SUM(s.maxScore) AS totalScore
FROM Hackers AS h
JOIN (SELECT hacker_id, challenge_id, MAX(score) AS maxScore
      FROM Submissions
      GROUP BY hacker_id, challenge_id) AS s ON h.hacker_id = s.hacker_id
GROUP BY s.hacker_id, h.name
HAVING totalScore > 0
ORDER BY totalScore DESC, s.hacker_id;
```

