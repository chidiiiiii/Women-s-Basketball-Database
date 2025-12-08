## Fully normalized database
- [RELATIONSHIP DIAGRAM](relationships.png)
  
The database is fully normalized to Third Normal Form (3NF). Each table stores one clear category of information with no repeating groups or unnecessary duplication. For example, players, teams, seasons, and games are all separated so that each entity has a single, reliable place where its information is kept. 
This prevents problems like update anomalies—if a team changes conferences or a player changes teams, the update only happens in one table.

Relationships between tables are handled using foreign keys, which allows the database to remain normalized while still linking all the necessary information. Instead of storing team names repeatedly in the players, games, and season stats tables, each table stores only the team’s ID. Similarly, game records reference teams and seasons by ID rather than repeating text. 
This ensures data consistency and reduces storage waste.

One design choice was to separate season statistics from game statistics. Season averages belong in the season_stats table, while individual games belong in the games table.
This separation prevents denormalization and avoids mixing two different grain levels of data. I had also broken down the seasons table to be seasons and then season_stats. The original design had all the stats in a season table but it led to dupicate date, hence why I had to break it down.

# Description of each table 

## Teams
Stores basic information about each college or university in the league, including its name, city, state, and league.
Other tables use the team_id to link players, coaches, games, and statistics to the correct school.
This keeps team data consistent and prevents repeating school names everywhere.

## Players

Stores personal and athletic information about each player, including name, position, height, and hometown.
Each player is linked to a single team through team_id.
This table allows coaches and statisticians to track rosters accurately.

## Coaches

Contains information about coaching staff members, including their names, hire year, and the team they coach.
It connects each coach to their team through team_id.
This helps maintain accurate records of staff throughout different seasons.

## Seasons

Stores the academic or athletic year (e.g., “2023–24”).
Season IDs link to statistics and games so the database can differentiate performance across different years.
This allows reporting and comparisons over time.

## Season_stats

Contains statistical averages for players for a specific season, such as minutes played, field goal percentages, and points per game. 
Links the player, their team, and the season using foreign keys.
This structure keeps all season performance data organized, accurate, and free of duplication.

## Games

Stores every game played, including date, home team, away team, scores, location, and game type.
Uses foreign keys to connect teams and seasons without repeating information.
This table forms the core of game schedule and results reporting.
