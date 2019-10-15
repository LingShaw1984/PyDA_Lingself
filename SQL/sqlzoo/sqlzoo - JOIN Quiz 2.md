# sqlzoo - JOIN Quiz 2

1. Select the statement which lists the unfortunate directors of the movies which have caused financial loses (gross <  budget)

   ```sql
   SELECT name
     FROM actor INNER JOIN movie ON actor.id = director
    WHERE gross < budget
   ```

2. Select the correct example of JOINing three tables

   ```sql
   SELECT *
     FROM actor JOIN casting ON actor.id = actorid
     JOIN movie ON movie.id = movieid
   ```

3. Select the statement that shows the list of actors called 'John' by order of number of movies in which they acted

   ```
   SELECT name, COUNT(movieid)
     FROM casting JOIN actor ON actorid=actor.id
    WHERE name LIKE 'John %'
   GROUP BY name ORDER BY 2 DESC
   ```

4. Select the result that would be obtained from the following code:  

```sql
 SELECT title 
   FROM movie JOIN casting ON (movieid=movie.id)
              JOIN actor   ON (actorid=actor.id)
  WHERE name='Paul Hogan' AND ord = 1
```

![1570610169097](C:\Users\凌\AppData\Roaming\Typora\typora-user-images\1570610169097.png)

5. Select the statement that lists all the actors that starred in movies directed by Ridley Scott who has id 351

   ```
   SELECT name
     FROM movie JOIN casting ON movie.id = movieid
     JOIN actor ON actor.id = actorid
   WHERE ord = 1 AND director = 351
   ```

6. There are two sensible ways to connect movie and actor. They are:![1570610203327](C:\Users\凌\AppData\Roaming\Typora\typora-user-images\1570610203327.png)

7. Select the result that would be obtained from the following code:  

```sql
 SELECT title, yr 
   FROM movie, casting, actor 
  WHERE name='Robert De Niro' AND movieid=movie.id AND actorid=actor.id AND ord = 3
```

![1570610221547](C:\Users\凌\AppData\Roaming\Typora\typora-user-images\1570610221547.png)