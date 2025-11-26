# SQL Query Examples

## 1. ORDER BY Two or More Columns
This query shows all Huntington University players, ordered first by position and then by last name. This is useful when you want to display data in a structured, readable order based on multiple criteria.

```sql
SELECT player_id, first_name, last_name, position, jersey_number
FROM players
ORDER BY position, last_name;
```

## 2. Using DIFFERENCE
This query gives the point difference between games during the 2024-25 season. We could also add the team ids and be able to tell how much the team lost or won by. 

```sql
SELECT game_id, home_score, away_score,
       (home_score - away_score) AS point_diff
FROM games
WHERE season_id = 2;
```

## 3. USING MONTHNAME
This query can get the months of every game played during the 2024-2025 season. We can later apply this and find the months that had the most wins.  

```sql
SELECT game_id, game_date, MONTHNAME(game_date) AS month_name
FROM games
WHERE season_id = 2;
```

## 4. HAVING & GROUP BY:
This query shows the teams having players greater than or equal to 15. This is the typical average number of players you want on a NAIA basketball team.
```sql
SELECT t.team_id, t.school_name, COUNT(p.player_id) AS total_players
FROM teams t
LEFT JOIN players p ON t.team_id = p.team_id
GROUP BY t.team_id, t.school_name
HAVING COUNT(p.player_id) >= 15;
```

## 5. INNER JOIN:
This query joins tables players, teams, and season_stats showing important data about the player and their team focusing on the last season.

```sql
SELECT p.player_id, p.first_name, p.last_name,
       ss.games_played, ss.field_goal_pct, ss.points_per_game,
       t.school_name AS team_name
FROM players p
INNER JOIN season_stats ss ON p.player_id = ss.player_id
INNER JOIN teams t ON t.team_id = ss.team_id
WHERE ss.season_id = 2;
```

## 6. LEFT OR RIGHT JOIN:
This query shows who had the highest three pointer percentage in descending order. Using minutes per game > 20 we see typically the starting players. 

```sql
SELECT p.first_name, p.last_name, s.three_pt_pct
FROM players p
LEFT JOIN season_stats s ON p.player_id = s.player_id
WHERE s.season_id = 2
  AND minutes_per_game > 20
ORDER BY s.three_pt_pct DESC;
```

## 7. UPDATE QUERY: 
We can use this when players transfer out to different schools.

```sql
UPDATE players
SET team_id = 7
WHERE player_id = 5;
```

## 8. DELETE QUERY: 
If a player left or transferred, we can get rid of that  player from our database

 ```sql
DELETE FROM players
WHERE player_id = 5;
```

## 9.  VIEW:
This view shows each player's name with their points per game.

 ```sql
CREATE VIEW player_points AS
SELECT p.first_name, p.last_name, ss.points_per_game
FROM players p
JOIN season_stats ss ON p.player_id = ss.player_id
WHERE ss.season_id = 2;

SELECT * FROM player_points;
 ```

## 10. ROLLBACK
This shows accidentally deleting all our players, but rollback before any of the changes are committed.

 ```sql
START TRANSACTION;
DELETE FROM players;
ROLLBACK;
 ```

