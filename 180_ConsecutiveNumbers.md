SELECT DISTINCT l1.num AS ConsecutiveNums
FROM Logs AS l1
JOIN Logs AS l2
ON l2.id-1 = l1.id
JOIN Logs AS l3
ON l3.id-1 = l2.id
WHERE l1.num = l2.num AND l1.num = l3.num