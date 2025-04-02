SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs AS l1
JOIN Logs AS l2
ON l2.id-1 = l1.id
JOIN Logs AS l3
ON l3.id-1 = l2.id
WHERE l1.num = l2.num AND l1.num = l3.num

- The condition l1.id = l2.id - 1 doesn't mean l2 has one less row
- It is establishing a relationship between the rows in the two table aliases based on their ID values
For exampel:
l1 row with id=1 joins with l2 row with id=2 (because 1 = 2-1)
l1 row with id=2 joins with l2 row with id=3 (because 2 = 3-1)
l1 row with id=3 joins with l2 row with id=4 (because 3 = 4-1)
l1 row with id=4 joins with l2 row with id=5 (because 4 = 5-1)