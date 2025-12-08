
## SQL Create Table Blocks

# Coaches Table
```sql
CREATE TABLE coaches (
    coach_id INT AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    team_id INT,
    hire_date DATE,
    FOREIGN KEY (team_id) REFERENCES teams(team_id)
);
```

# Games Table
```sql
CREATE TABLE games (
    game_id INT AUTO_INCREMENT PRIMARY KEY,
    game_date DATE,
    
    home_team_id INT,
    away_team_id INT,
    
    home_score INT,
    away_score INT,
    
    location VARCHAR(100),
    game_type VARCHAR(50),
    
    FOREIGN KEY (home_team_id) REFERENCES teams(team_id),
    FOREIGN KEY (away_team_id) REFERENCES teams(team_id)
);
```
# Players Table

```sql
 CREATE TABLE players (
    player_id INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    date_of_birth DATE NOT NULL,
    height VARCHAR(10) NOT NULL,
    position ENUM('G','F','C','G/F','F/C') NOT NULL,
    jersey_number INT(11) DEFAULT NULL,
    hometown VARCHAR(100) DEFAULT NULL,
    team_id INT(11) DEFAULT NULL,
    height_inches INT(11) DEFAULT NULL,
    
    FOREIGN KEY (team_id) REFERENCES teams(team_id)
);  
```
# Seasons Table
```sql
CREATE TABLE seasons (
    season_id INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    season_year VARCHAR(20) UNIQUE DEFAULT NULL
);
```

# Season stats Table 
```sql
CREATE TABLE season_stats (
    stats_id INT(11) NOT NULL AUTO_INCREMENT PRIMARY KEY,
    player_id INT(11) NOT NULL,
    team_id INT(11) NOT NULL,
    season_id INT(11) NOT NULL,
    games_played INT(11) DEFAULT NULL,
    games_started INT(11) DEFAULT NULL,
    minutes_per_game DECIMAL(4,1) DEFAULT NULL,
    field_goal_pct DECIMAL(5,2) DEFAULT NULL,
    three_pt_pct DECIMAL(5,2) DEFAULT NULL,
    free_throw_pct DECIMAL(5,2) DEFAULT NULL,
    points_per_game DECIMAL(4,1) DEFAULT NULL,
    FOREIGN KEY (player_id) REFERENCES players(player_id),
    FOREIGN KEY (team_id) REFERENCES teams(team_id),
    FOREIGN KEY (season_id) REFERENCES seasons(season_id)
);
```
# Teams table 
```sql
CREATE TABLE teams (
    team_id INT(11) NOT NULL PRIMARY KEY,
    school_name VARCHAR(255) DEFAULT NULL,
    city VARCHAR(255) DEFAULT NULL,
    state VARCHAR(255) DEFAULT NULL,
    league VARCHAR(255) DEFAULT NULL
);
```
