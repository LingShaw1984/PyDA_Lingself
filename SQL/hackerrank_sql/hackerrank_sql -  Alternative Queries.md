# hackerrank_sql -  Alternative Queries 

##  Draw The Triangle 1 

*P(R)* represents a pattern drawn by Julia in *R* rows. The following pattern represents *P(5)*:

```
* * * * * 
* * * * 
* * * 
* * 
*
```

Write a query to print the pattern *P(20)*.

Solution:

```MYSQL
SET @number = 21;
SELECT REPEAT('* ', @number := @number-1)
FROM information_schema.tables;
```



## Draw The Triangle 2 

*P(R)* represents a pattern drawn by Julia in *R* rows. The following pattern represents *P(5)*:

```
* 
* * 
* * * 
* * * * 
* * * * *
```

Write a query to print the pattern *P(20)*.

Solution:

```mysql
SET @number = 0;
SELECT REPEAT('* ', @number := @number+1)
FROM information_schema.tables
LIMIT 20;
```



##  Print Prime Numbers 

 Write a query to print all *prime numbers* less than or equal to 1000. Print your result on a single line, and use the ampersand (&) character as your separator (instead of a space). 

 For example, the output for all prime numbers ≤ 10 would be: 

```
2&3&5&7
```

Solution:

```mysql
SET @potential_prime = 1;
SET @divisor = 1;

SELECT GROUP_CONCAT(POTENTIAL_PRIME SEPARATOR '&') FROM
    (SELECT @potential_prime := @potential_prime + 1 AS POTENTIAL_PRIME FROM
    information_schema.tables t1,
    information_schema.tables t2
    LIMIT 1000) list_of_potential_primes
WHERE NOT EXISTS(
	SELECT * FROM
        (SELECT @divisor := @divisor + 1 AS DIVISOR FROM
	    information_schema.tables t4,
        information_schema.tables t5
	    LIMIT 1000) list_of_divisors
	WHERE MOD(POTENTIAL_PRIME, DIVISOR) = 0 AND POTENTIAL_PRIME <> DIVISOR);
```

