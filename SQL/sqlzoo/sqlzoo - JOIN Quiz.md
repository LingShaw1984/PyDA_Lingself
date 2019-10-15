# sqlzoo - JOIN Quiz

1. You want to find the stadium where player 'Dimitris Salpingidis' scored. Select the JOIN condition to use:

   ```sql
   game  JOIN goal ON (id=matchid)
   ```

   

2. You JOIN the tables **goal** and **eteam** in an SQL statement. Indicate the list of column names that may be used in the SELECT line:

   ```sql
    matchid, teamid, player, gtime, id, teamname, coach
   ```

   

3. Select the code which shows players, their team and the amount of goals they scored against Greece(GRE).

   ```sql
   SELECT player, teamid, COUNT(*)
     FROM game JOIN goal ON matchid = id
    WHERE (team1 = "GRE" OR team2 = "GRE")
      AND teamid != 'GRE'
    GROUP BY player, teamid
   ```

   

4. Select the result that would be obtained from this code: 

```sql
SELECT DISTINCT teamid, mdate
  FROM goal JOIN game on (matchid=id)
 WHERE mdate = '9 June 2012'
```

![1570558187882](C:\Users\凌\AppData\Roaming\Typora\typora-user-images\1570558187882.png)

5. Select the code which would show the player and their team for those who have scored against Poland(POL) in National Stadium, Warsaw.

  ```sql
   SELECT DISTINCT player, teamid 
     FROM game JOIN goal ON matchid = id 
    WHERE stadium = 'National Stadium, Warsaw' 
   AND (team1 = 'POL' OR team2 = 'POL')
     AND teamid != 'POL'
  ```

  

6. Select the code which shows the player, their team and the time they scored, for players who have played in Stadion Miejski (Wroclaw) but not against Italy(ITA).

  ```sql
  SELECT DISTINCT player, teamid, gtime
    FROM game JOIN goal ON matchid = id
   WHERE stadium = 'Stadion Miejski (Wroclaw)'
     AND (( teamid = team2 AND team1 != 'ITA') OR ( teamid = team1 AND team2 != 'ITA'))
  ```

7. Select the result that would be obtained from this code: 

```sql
SELECT teamname, COUNT(*)
  FROM eteam JOIN goal ON teamid = id
 GROUP BY teamname
HAVING COUNT(*) < 3
```

![1570558280963](C:\Users\凌\AppData\Roaming\Typora\typora-user-images\1570558280963.png)