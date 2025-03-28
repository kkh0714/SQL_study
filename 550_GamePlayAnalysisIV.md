SELECT ROUND(COUNT(player_id)/(SELECT COUNT(DISTINCT player_id) FROM Activity), 2) AS fraction
FROM Activity
WHERE (player_id, DATE_SUB(event_date, INTERVAL 1 DAY)) IN (
    SELECT player_id, MIN(event_date)
    FROM Activity
    GROUP BY player_id
)

1. `DATE_SUB(event_date, INTERVAL 1 DAY)` creates the previous day's date from the current `event_date` (we are looking backwards)
2. The inner subquery `SELECT player_id, MIN(event_date) FROM Activity GROUP BY player_id` finds each player's *first login date*

3. The `IN` clause checks if the current `event_date` matches the player's *first login date*

