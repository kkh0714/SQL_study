SELECT customer_id
FROM Customer AS c
GROUP BY customer_id
HAVING COUNT(DISTINCT c.product_key) = (SELECT COUNT(product_key) FROM Product)



- `LEFT JOIN` is unnecessary here. In this problem, we're only interested in actual purchases which would be in the Customer table already
- `DISTINCT` is important here because the question specifies "This table may contain duplicates rows."
