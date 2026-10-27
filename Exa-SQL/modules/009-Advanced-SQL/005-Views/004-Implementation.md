<br>

In this example we will work with two tables. The `players` table will focus on the player information and the `games_played` table, which stores data about each game played and has a foreign key (`player_id`) referencing the players table to establish a relationship between players and the games they've played.

Table 1: players

|player_id|player_name|player_email             |
|---------|-----------|-------------------------|
|        1|Tanisi     |cantstopmenow@example.com|
|        2|Zelda      |mamamia@example.com      |
|        3|ImmaWinner |zeldafan@example.com     |





Table 2: games_played

|game_id|player_id|game_title                             |game_score|
|-------|---------|--------------------------------------|----------|
|    101|        1|The Legend of Zelda: Ocarina of Time   |        95|
|    102|        1|The Legend of Zelda: Breath of the Wild|        98|
|    103|        2|The Legend of Zelda: Twilight Princess |        92|
|    104|        2|The Legend of Zelda: Skyward Sword     |        88|
|    105|        3|The Legend of Zelda: Wind Waker        |        90|
|    106|        3|The Legend of Zelda: A Link to the Past|        94|



Let's consider a scenario where you were tasked with retrieving detailed information about each player along with the games they have played. Assuming we want a view that includes detailed information about each player and the games they have played, we can create a view named `player_games_view`:

**Syntax for Creating a View**:
```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

**Creating a view named player_games_view**:
```sql
-- Create a view to show detailed information about each player and the games they played
CREATE VIEW player_games_view
AS
SELECT p.player_id, p.player_name, p.player_email, g.game_id,g.game_title, g.game_score
FROM players p
JOIN games_played g 
ON p.player_id = g.player_id;
```


This view encapsulates the logic of joining the `players` and `games_played` tables, providing a simplified way to retrieve detailed information about each player and the games they have played.

To see the view we can do a basic SELECT all statement
```sql
SELECT * FROM player_games_view;
```
OUTPUT:

|player_id|player_name|player_email             |game_id|game_title                             |game_score|
|---------|-----------|-------------------------|-------|---------------------------------------|----------|
|        1|Tanisi     |cantstopmenow@example.com|    101|The Legend of Zelda: Ocarina of Time   |        95|
|        1|Tanisi     |cantstopmenow@example.com|    102|The Legend of Zelda: Breath of the Wild|        98|
|        2|Zelda      |mamamia@example.com      |    103|The Legend of Zelda: Twilight Princess |        92|
|        2|Zelda      |mamamia@example.com      |    104|The Legend of Zelda: Skyward Sword     |        88|
|        3|ImmaWinner |zeldafan@example.com     |    105|The Legend of Zelda: Wind Waker        |        90|
|        3|ImmaWinner |zeldafan@example.com     |    106|The Legend of Zelda: A Link to the Past|        94|

