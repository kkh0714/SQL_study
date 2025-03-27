SELECT q.query_name, 
ROUND(AVG(q.rating/q.position), 2) AS quality, 
ROUND(AVG(IF(q.rating < 3, 1, 0))*100, 2) AS poor_query_percentage
FROM Queries AS q
GROUP BY q.query_name