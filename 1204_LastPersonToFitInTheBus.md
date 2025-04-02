```SQL
SELECT q1.person_name
FROM Queue AS q1
JOIN Queue AS q2
ON q1.turn >= q2.turn
GROUP BY q1.turn
HAVING SUM(q2.weight) <= 1000
ORDER BY q1.turn DESC
LIMIT 1
```

- `ON q1.turn >= q2.turn` means:
  - When `q1.turn` = 1, then `q2.turn` = (1) 
  - When `q1.turn` = 2, then `q2.turn` =  (1, 2)
  - When `q1.turn` = 3, then `q2.turn` = (1, 2, 3) 
  - When `q1.turn` = 4, then `q2.turn` = (1, 2, 3, 4)
  - When `q1.turn` = 5, then `q2.turn` = (1, 2, 3, 4, 5)
  - When `q1.turn` = 6, then `q2.turn` = (1, 2, 3, 4, 5, 6)
  - There are 21 rows in total before grouping

- `GROUP BY q1.turn` returns the same thing as `ON q1.turn >= q2.turn`, but reduces to only 6 rows
- `HAVING SUM(q2.weight) <= 1000` sums up all the weight in each `q2.turn` per `q1.turn`

