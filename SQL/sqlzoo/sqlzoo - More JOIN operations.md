# sqlzoo - More JOIN operations

1. List the films where the **yr** is 1962 [Show **id**, **title**]   

   ```sql
   SELECT id, title
    FROM movie
    WHERE yr=1962
   ```

2. Give year of 'Citizen Kane'.    

   ```sql
   SELECT yr
   FROM movie
   WHERE title = 'Citizen Kane';
   ```

3. List all of the Star Trek movies, include the **id**, **title** and **yr** (all of these movies include the words Star Trek in the title). Order results by year. 

   ```sql
   SELECT id, title, yr
   FROM movie
   WHERE title LIKE 'Star Trek%'
   ORDER BY yr;
   ```

4. What **id** number does the actor 'Glenn Close' have?   

   ```sql
   SELECT id
   FROM actor
   WHERE name = 'Glenn Close';
   ```

5. What is the **id** of the film 'Casablanca'    

   ```sql
   SELECT id
   FROM movie
   WHERE title = 'Casablanca';
   ```

6. Obtain the cast list for 'Casablanca'. 

   what is a cast list?

   Use **movieid=11768**, (or whatever value you got from the previous question)   

   ```sql
   SELECT name
   FROM casting JOIN actor ON actorid = id
   WHERE movieid = '11768';
   ```

7. Obtain the cast list for the film 'Alien'  

   ```sql
   SELECT name
   FROM casting JOIN actor ON actorid = id
   WHERE movieid = (SELECT id
                    FROM movie
                    WHERE title = 'Alien');
   ```

8. List the films in which 'Harrison Ford' has appeared    

   ```sql
   SELECT title
   FROM movie JOIN casting ON movie.id = movieid JOIN actor ON actorid = actor.id
   WHERE actor.name = 'Harrison Ford';
   ```

9. List the films where 'Harrison Ford' has appeared - but not in the starring role. 
   [Note: the **ord** field of casting gives the position of the actor. 
   If ord=1 then this actor is in the starring role]     

   ```sql
   SELECT title
   FROM movie JOIN casting ON movie.id = movieid JOIN actor ON actorid = actor.id
   WHERE actor.name = 'Harrison Ford'
   AND casting.ord <> 1;
   ```

10. List the films together with the leading star for all 1962 films.      

    ```sql
    SELECT m.title, a.name
    FROM movie AS m
    JOIN casting AS c ON m.id = c.movieid
    JOIN actor AS a ON c.actorid = a.id
    WHERE c.ord = 1
    AND yr = 1962;
    ```

11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.      

    ```sql
    SELECT yr,COUNT(title)
    FROM movie
    JOIN casting ON movie.id=movieid
    JOIN actor   ON actorid=actor.id
    WHERE name='Rock Hudson'
    GROUP BY yr
    HAVING COUNT(title) > 2;
    ```

12. List the film title and the leading actor for all of the films 'Julie Andrews' played in. 

    Did you get "Little Miss Marker twice"?

    ```sql
    SELECT DISTINCT title, name
    FROM (SELECT m.*
          FROM movie AS m
          JOIN casting AS c ON m.id = c.movieid
          JOIN actor AS a ON a.id = c.actorid
          WHERE a.name = 'Julie Andrews') AS t1
    JOIN
         (SELECT actor.*, casting.movieid
          FROM actor
          JOIN casting ON actor.id = casting.actorid
          WHERE casting.ord = 1) AS t2
    ON t1.id = t2.movieid;
    
    ```

13. Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.        

    ```
    SELECT a.name
    FROM actor AS a
    JOIN casting AS c
    ON a.id = c.actorid
    WHERE c.ord = 1
    GROUP BY a.name
    HAVING COUNT(a.name) >= 30
    ORDER BY a.name;
    ```

14. List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

    ```sql
    SELECT m.title, COUNT(m.title)
    FROM movie AS m
    JOIN casting AS c
    ON m.id = c.movieid
    WHERE yr = 1978
    GROUP BY m.title
    ORDER BY COUNT(m.title) DESC, m.title;
    ```

15. List all the people who have worked with 'Art Garfunkel'.         

    ```sql
    SELECT actor.name
    FROM (SELECT casting.*
          FROM (SELECT m.*
                FROM actor a
                JOIN casting c
                ON a.id = c.actorid
                JOIN movie m
                ON m.id = c.movieid
                WHERE a.name = 'Art Garfunkel') AS t1
          JOIN casting
          ON t1.id = casting.movieid) AS t2
    JOIN actor
    ON actor.id = t2.actorid
    WHERE actor.name <> 'Art Garfunkel';
    ```

    



