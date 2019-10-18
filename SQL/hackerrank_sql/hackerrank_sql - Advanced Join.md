# hackerrank_sql - Advanced Join

##  SQL Project Planning 

You are given a table, *Projects*, containing three columns: *Task_ID*, *Start_Date* and *End_Date*. It is guaranteed that the difference between the *End_Date* and the *Start_Date* is equal to *1* day for each row in the table.

![img](https://s3.amazonaws.com/hr-challenge-images/12894/1443819551-639948acc0-1.png)

If the *End_Date* of the tasks are consecutive, then they are  part of the same project. Samantha is interested in finding the total  number of different projects completed.

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order.  If there is more than one project that have the same number of  completion days, then order by the start date of the project.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12894/1443819440-1c40e943a1-2.png)

**Sample Output**

```
2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04
```


 **Explanation**

The example describes following *four* projects:

- *Project 1*: Tasks *1*, *2* and *3* are completed on consecutive days, so these are part of the project. Thus start date of project is *2015-10-01* and end date is *2015-10-04*, so it took *3 days* to complete the project.
- *Project 2*: Tasks *4* and *5* are completed on consecutive days, so these are part of the project. Thus, the start date of project is *2015-10-13* and end date is *2015-10-15*, so it took *2 days* to complete the project.
- *Project 3*: Only task *6* is part of the project. Thus, the start date of project is *2015-10-28* and end date is *2015-10-29*, so it took *1 day* to complete the project.
- *Project 4*: Only task *7* is part of the project. Thus, the start date of project is *2015-10-30* and end date is *2015-10-31*, so it took *1 day* to complete the project.

Solution:

```
SELECT Start_Date, MIN(End_Date)
FROM (SELECT Start_Date
      FROM Projects
      WHERE Start_Date NOT IN (SELECT End_Date FROM Projects)) AS s,
     (SELECT End_Date
      FROM Projects
      WHERE End_Date NOT IN (SELECT Start_Date FROM Projects)) AS e
WHERE Start_Date < End_Date
GROUP BY Start_Date
ORDER BY DATEDIFF(MIN(End_Date), Start_Date), Start_Date;
```



##  Placements 

You are given three tables: *Students*, *Friends* and *Packages.* *Students* contains two columns: *ID* and *Name*. *Friends* contains two columns: *ID* and *Friend_ID* (*ID* of the ONLY best friend). *Packages* contains two columns: *ID* and *Salary* (offered salary in $ thousands per month).

![img](https://s3.amazonaws.com/hr-challenge-images/12895/1443820186-2a9b4939a8-1.png)

Write a query to output the names of those students whose best  friends got offered a higher salary than them. Names must be ordered by  the salary amount offered to the best friends. It is guaranteed that no  two students got same salary offer.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12895/1443820079-9bd1e231b1-2_1.png) ![img](https://s3.amazonaws.com/hr-challenge-images/12895/1443820100-adb691b2f5-2_2.png)

**Sample Output**

```
Samantha
Julia
Scarlet
```


 **Explanation**

See the following table:

![img](https://s3.amazonaws.com/hr-challenge-images/12895/1443819966-c37c146d27-3.png)

Now,

- *Samantha's* best friend got offered a higher salary than her at 11.55
- *Julia's* best friend got offered a higher salary than her at 12.12
- *Scarlet's* best friend got offered a higher salary than her at 15.2
- *Ashley's* best friend did NOT get offered a higher salary than her

The name output, when ordered by the salary offered to their friends, will be:

- *Samantha*
- *Julia*
- *Scarlet*

Solution:

```
SELECT s.Name FROM Students AS s 
JOIN Packages AS p1 ON s.ID = p1.ID 
JOIN Friends AS f ON s.ID = f.ID
JOIN Packages AS p2 ON f.Friend_ID = p2.ID
WHERE p1.Salary < p2.Salary
ORDER BY p2.Salary;
```



##  Symmetric Pairs 

You are given a table, *Functions*, containing two columns: *X* and *Y*.

![img](https://s3.amazonaws.com/hr-challenge-images/12892/1443818798-51909e977d-1.png)

Two pairs *(X1, Y1)* and *(X2, Y2)* are said to be *symmetric* *pairs* if *X1 = Y2* and *X2 = Y1*.

Write a query to output all such *symmetric* *pairs* in ascending order by the value of *X*.

**Sample Input**

![img](https://s3.amazonaws.com/hr-challenge-images/12892/1443818693-b384c24e35-2.png)

**Sample Output**

```
20 20
20 21
22 23
```

Solution:

```
SELECT f1.X, f1.Y
FROM Functions AS f1 
WHERE f1.X = f1.Y AND (SELECT COUNT(*)
                       FROM Functions
                       WHERE X = f1.X AND Y = f1.X) > 1
UNION
SELECT f1.X, f1.Y
FROM Functions AS f1, Functions AS f2
WHERE f1.X <> f1.Y AND f1.X = f2.Y AND f1.Y = f2.X AND f1.X < f2.X
ORDER BY X;
```



##  Interviews 

Samantha interviews many candidates from different colleges using coding challenges and contests. Write a query to print the *contest_id*, *hacker_id*, *name*, and the sums of *total_submissions*, *total_accepted_submissions*, *total_views*, and *total_unique_views* for each contest sorted by *contest_id*. Exclude the contest from the result if all four sums are 0.

**Note:** A specific contest can be used to screen candidates at more than one college, but each college only holds 1 screening contest.

------

**Input Format**

The following tables hold interview data:

- *Contests*: The *contest_id* is the id of the contest, *hacker_id* is the id of the hacker who created the contest, and *name* is the name of the hacker.

![contests_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/contests_0.png)

- *Colleges*: The *college_id* is the id of the college, and *contest_id*is the id of the contest that Samantha used to screen the candidates.

![colleges_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/colleges_0.png)

- *Challenges*: The *challenge_id* is the id of the challenge that belongs to one of the contests whose contest_id Samantha forgot, and *college_id* is the id of the college where the challenge was given to candidates.

![challenges_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/challenges_0.png)

- *View_Stats*: The *challenge_id* is the id of the challenge, *total_views* is the number of times the challenge was viewed by candidates, and *total_unique_views* is the number of times the challenge was viewed by unique candidates.

![view_stats_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/view_stats_0.png)

- *Submission_Stats*: The *challenge_id* is the id of the challenge, *total_submissions* is the number of submissions for the challenge, and *total_accepted_submission* is the number of submissions that achieved full scores.

![submission_stats_0](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/submission_stats_0.png)

------

**Sample Input**

Contests Table:

![contests_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/contests_1.png)

Colleges Table:

![colleges_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/colleges_1.png)

Challenges Table:

![challenges_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/challenges_1.png)

View_Stats Table:

![view_stats_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/view_stats_1.png)

Submission_Stats Table:

![submission_stats_1](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/submission_stats_1.png)

**Sample Output**

> 66406 17973 Rose 111 39 156 56
>  66556 79153 Angela 0 0 11 10
>  94828 80275 Frank 150 38 41 15

**Explanation**

The contest 66406 is used in the college 11219. In this college  11219, challenges 18765 and 47127 are asked, so from the view and  submission stats:

- Sum of total submissions = 27 + 56 + 28 = 111
- Sum of total accepted submissions = 10 + 18 + 11 = 39
- Sum of total views = 43 + 72 + 26 + 15 = 156
- Sum of total unique views = 10 + 13 + 19 + 14 = 56

Similarly, we can find the sums for contests 66556 and 94828.

Solution:

```
SELECT con.contest_id, con.hacker_id, con.name, 
SUM(sg.total_submissions), SUM(sg.total_accepted_submissions), 
SUM(vg.total_views), SUM(vg.total_unique_views)
FROM Contests AS con
JOIN Colleges AS col ON con.contest_id = col.contest_id
JOIN Challenges AS cha ON cha.college_id = col.college_id
LEFT JOIN
(SELECT ss.challenge_id, SUM(ss.total_submissions) AS total_submissions, SUM(ss.total_accepted_submissions) AS total_accepted_submissions FROM Submission_Stats AS ss GROUP BY ss.challenge_id) AS sg
ON cha.challenge_id = sg.challenge_id
LEFT JOIN
(SELECT vs.challenge_id, SUM(vs.total_views) AS total_views, SUM(vs.total_unique_views) AS total_unique_views
FROM View_Stats AS vs GROUP BY vs.challenge_id) AS vg
ON cha.challenge_id = vg.challenge_id
GROUP BY con.contest_id, con.hacker_id, con.name
HAVING SUM(sg.total_submissions) +
       SUM(sg.total_accepted_submissions) +
       SUM(vg.total_views) +
       SUM(vg.total_unique_views) > 0
ORDER BY con.contest_id;
```

PS: The Solution com from: [SQL Notes: Hackerrank Interviews - Memogrocery](https://nifannn.github.io/2017/10/24/SQL-Notes-Hackerrank-Interviews/)



##  15 Days of Learning SQL

 Julia conducted a 15 days of learning SQL contest. The start date of the contest was *March 01, 2016* and the end date was *March 15, 2016*.  

 Write a query to print total number of unique hackers who made at least 1 submission each day (starting on the first day of the contest), and find the *hacker_id* and *name* of the hacker who made maximum number of submissions each day. If more  than one such hacker has a maximum number of submissions, print the  lowest *hacker_id*. The query should print this information for each day of the contest, sorted by the date. 

------

**Input Format**

The following tables hold contest data:

- *Hackers:* The *hacker_id* is the id of the hacker, and *name* is the name of the hacker.![img](https://s3.amazonaws.com/hr-challenge-images/19597/1458511164-12adec3b8b-ScreenShot2016-03-21at3.26.47AM.png)
- *Submissions:* The *submission_date* is the date of the submission, *submission_id* is the id of the submission, *hacker_id* is the id of the hacker who made the submission, and *score* is the score of the submission. ![img](https://s3.amazonaws.com/hr-challenge-images/19597/1458511251-0b534030b9-ScreenShot2016-03-21at3.26.56AM.png)

**Sample Input**

For the following sample input, assume that the end date of the contest was *March 06, 2016*.

*Hackers* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19597/1458511957-814a2c7bf2-ScreenShot2016-03-21at3.27.06AM.png) *Submissions* Table: ![img](https://s3.amazonaws.com/hr-challenge-images/19597/1458512015-ff6a708164-ScreenShot2016-03-21at3.27.21AM.png)

**Sample Output**

```
2016-03-01 4 20703 Angela
2016-03-02 2 79722 Michael
2016-03-03 2 20703 Angela
2016-03-04 2 20703 Angela
2016-03-05 1 36396 Frank
2016-03-06 1 20703 Angela
```

**Explanation**

On *March 01, 2016* hackers 20703, 36396, 53473, and 79722 made submissions. There are  unique hackers who made at least one submission each day. As each hacker made one submission, 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is *Angela*. 

On *March 02, 2016* hackers 15758, 20703, and 79722 made submissions. Now 20703 and 79722 were the only ones to submit every day, so there are 2 unique hackers who made at least one submission each day. 79722 made 2 submissions, and name of the hacker is *Michael*. 

 On *March 03, 2016* hackers 20703, 36396, and 79722 made submissions. Now 20703 and 79722 were the only ones, so there are  unique hackers who made at least one submission each day. As each hacker made one submission so 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is *Angela*. 

 On *March 04, 2016* hackers 20703, 44065, 53473, and 79722 made submissions. Now 20703 and 79722 only submitted each day, so there are 2 unique hackers who made at least one submission each day. As each hacker made one submission so 20703 is considered to be the hacker who made maximum number of submissions on this day. The name of the hacker is *Angela*. 

 On *March 05, 2016* hackers 20703, 36396, 38289 and 62529 made submissions. Now 20703 only submitted each day, so there is only 1 unique hacker who made at least one submission each day. 36396 made 2 submissions and name of the hacker is *Frank*. 

 On *March 06, 2016* only 20703 made submission, so there is only 1 unique hacker who made at least one submission each day. 20703 made 1 submission and name of the hacker is *Angela*. 

Solution:

```mysql
SELECT SUBMISSION_DATE,
	   (SELECT COUNT(DISTINCT HACKER_ID)
	   FROM SUBMISSIONS S2
	   WHERE S2.SUBMISSION_DATE = S1.SUBMISSION_DATE
	   AND (SELECT COUNT(DISTINCT S3.SUBMISSION_DATE)
			FROM SUBMISSIONS S3
			WHERE S3.HACKER_ID = S2.HACKER_ID AND S3.SUBMISSION_DATE < S1.SUBMISSION_DATE) = DATEDIFF(S1.SUBMISSION_DATE , '2016-03-01')),
	   (SELECT HACKER_ID
	   FROM SUBMISSIONS S2
	   WHERE S2.SUBMISSION_DATE = S1.SUBMISSION_DATE
	   GROUP BY HACKER_ID
	   ORDER BY COUNT(SUBMISSION_ID) DESC, HACKER_ID LIMIT 1) AS TMP,
	   (SELECT NAME
	   FROM HACKERS
	   WHERE HACKER_ID = TMP)
FROM (SELECT DISTINCT SUBMISSION_DATE
	 FROM SUBMISSIONS) S1
GROUP BY SUBMISSION_DATE;
```

PS：The Answear come form:[HackerRank-Solutions/15 Days of Learning SQL.mysql at master · BlakeBrown/HackerRank-Solutions](https://github.com/BlakeBrown/HackerRank-Solutions/blob/master/SQL/5_Advanced%20Join/5_15%20Days%20of%20Learning%20SQL/15%20Days%20of%20Learning%20SQL.mysql)

PPS: 最后两个也太难了。突然就上天了，兼职不是人类可以解决的问题。