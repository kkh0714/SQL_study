```SQL
(SELECT u.name AS results
FROM Users AS u
LEFT JOIN MovieRating AS m
USING(user_id)
GROUP BY u.user_id
ORDER BY COUNT(m.movie_id) DESC, u.name ASC
LIMIT 1)

UNION ALL

(SELECT m1.title AS results
FROM Movies AS m1
LEFT JOIN MovieRating AS m2
ON m1.movie_id = m2.movie_id
WHERE m2.created_at BETWEEN "2020-02-01" AND "2020-02-28"
GROUP BY m1.title
ORDER BY AVG(m2.rating) DESC, m1.title ASC
LIMIT 1)
```

The brackets around each `SELECT` query in your `UNION ALL` statement are necessary for two main reasons:

1. **Order of operations**: The brackets ensure that each individual query is fully executed (including its own `ORDER BY` and `LIMIT` clauses) before the `UNION ALL` combines them. Without brackets, SQL might interpret the `ORDER BY` and `LIMIT` clauses as applying to the entire combined result rather than to each subquery separately.
2. **Subquery requirement**: When using `UNION`, `UNION ALL`, `INTERSECT`, or `EXCEPT` operations with queries that have `ORDER BY` and `LIMIT` clauses, SQL requires that these queries be enclosed in parentheses to treat them as subqueries.