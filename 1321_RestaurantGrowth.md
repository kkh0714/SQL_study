```SQL
SELECT visited_on,
(SELECT SUM(amount)
FROM Customer
WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
) AS amount,
(SELECT ROUND(SUM(amount)/7, 2)
FROM Customer
WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
) AS average_amount

FROM Customer AS c

WHERE visited_on >= (
    SELECT DATE_ADD(MIN(visited_on), INTERVAL 6 DAY)
    FROM customer
)

GROUP BY visited_on
```

Step 1: Find the days we are looking for

```sql
WHERE visited_on >= (
    SELECT DATE_ADD(MIN(visited_on), INTERVAL 6 DAY)
    FROM customer
)
```

Step 2: Given the days we are looking for, we define the calculation for `amount` and `average_amount`

```SQL
WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
) AS amount,
(SELECT ROUND(SUM(amount)/7, 2)
FROM Customer
WHERE visited_on BETWEEN DATE_SUB(c.visited_on, INTERVAL 6 DAY) AND c.visited_on
) AS average_amount
```

- In your query, you use `c.visited_on` in the subqueries because you need to reference the visited_on value from the current row of the outer query.