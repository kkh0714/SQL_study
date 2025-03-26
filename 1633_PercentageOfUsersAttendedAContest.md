SELECT contest_id, ROUND(COUNT(r.user_id)/(SELECT COUNT(user_id) FROM Users)*100, 2) AS percentage
FROM Register AS r
GROUP BY r.contest_id
ORDER BY percentage DESC, contest_id ASC