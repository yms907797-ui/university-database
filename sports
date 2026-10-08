CREATE DATABASE GamesDB;
USE GamesDB;
CREATE TABLE Games (
    game_id INT PRIMARY KEY,
    game_name VARCHAR(50) NOT NULL,
    min_age INT NOT NULL,
    max_age INT NOT NULL
);
CREATE TABLE Players (
    player_id INT PRIMARY KEY,
    player_name VARCHAR(50) NOT NULL,
    age INT NOT NULL,
    gender VARCHAR(10)
);
CREATE TABLE Teams (
    team_id INT PRIMARY KEY,
    team_name VARCHAR(50) NOT NULL,
    game_id INT,
    coach_id INT
);
CREATE TABLE Coaches (
    coach_id INT PRIMARY KEY,
    coach_name VARCHAR(50) NOT NULL,
    experience INT
);
CREATE TABLE Tournaments (
    tournament_id INT PRIMARY KEY,
    tournament_name VARCHAR(100) NOT NULL,
    game_id INT,
    tournament_date DATE
);
CREATE TABLE PlayerParticipation (
    participation_id INT PRIMARY KEY,
    player_id INT,
    game_id INT,
    team_id INT,
    tournament_id INT,
    score INT,

    FOREIGN KEY (player_id) REFERENCES Players(player_id),
    FOREIGN KEY (game_id) REFERENCES Games(game_id),
    FOREIGN KEY (team_id) REFERENCES Teams(team_id),
    FOREIGN KEY (tournament_id) REFERENCES Tournaments(tournament_id)
);
ALTER TABLE Teams
ADD FOREIGN KEY (game_id) REFERENCES Games(game_id);

ALTER TABLE Teams
ADD FOREIGN KEY (coach_id) REFERENCES Coaches(coach_id);
ALTER TABLE Tournaments
ADD FOREIGN KEY (game_id) REFERENCES Games(game_id);
INSERT INTO Games VALUES
(1, 'Football', 16, 35),
(2, 'Basketball', 18, 30),
(3, 'Cricket', 15, 40),
(4, 'Tennis', 14, 35),
(5, 'Badminton', 12, 30);
INSERT INTO Players VALUES
(101, 'Rahul', 20, 'Male'),
(102, 'Arjun', 25, 'Male'),
(103, 'Priya', 19, 'Female'),
(104, 'Sneha', 28, 'Female'),
(105, 'Kiran', 16, 'Male'),
(106, 'Ravi', 32, 'Male'),
(107, 'Anjali', 14, 'Female'),
(108, 'Vikram', 22, 'Male');
INSERT INTO Coaches VALUES
(201, 'Ramesh', 10),
(202, 'Suresh', 8),
(203, 'Mahesh', 12),
(204, 'Kavya', 6),
(205, 'Deepak', 15);
INSERT INTO Teams VALUES
(301, 'Thunder FC', 1, 201),
(302, 'Basket Warriors', 2, 202),
(303, 'Super Strikers', 3, 203),
(304, 'Tennis Stars', 4, 204),
(305, 'Smash Masters', 5, 205);
INSERT INTO Tournaments VALUES
(401, 'National Football Cup', 1, '2026-01-15'),
(402, 'State Basketball League', 2, '2026-02-10'),
(403, 'National Cricket Cup', 3, '2026-03-20'),
(404, 'Tennis Championship', 4, '2026-04-12'),
(405, 'Badminton Open', 5, '2026-05-18');
INSERT INTO PlayerParticipation VALUES
(501, 101, 1, 301, 401, 85),
(502, 102, 1, 301, 401, 92),
(503, 103, 2, 302, 402, 88),
(504, 104, 2, 302, 402, 95),
(505, 105, 1, 301, 401, 70),
(506, 106, 3, 303, 403, 91),
(507, 107, 4, 304, 404, 75),
(508, 108, 3, 303, 403, 98),
(509, 101, 5, 305, 405, 89),
(510, 104, 4, 304, 404, 93);
SELECT 
    p.player_name,
    p.age,
    g.game_name,
    pp.score
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id;
SELECT
    p.player_name,
    t.team_name,
    c.coach_name
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Teams t
    ON pp.team_id = t.team_id
JOIN Coaches c
    ON t.coach_id = c.coach_id;
SELECT
    p.player_name,
    g.game_name,
    tr.tournament_name,
    pp.score
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id
JOIN Tournaments tr
    ON pp.tournament_id = tr.tournament_id;
SELECT
    p.player_name,
    p.age,
    g.game_name,
    t.team_name,
    c.coach_name,
    tr.tournament_name,
    pp.score
FROM PlayerParticipation pp
JOIN Players p
    ON pp.player_id = p.player_id
JOIN Games g
    ON pp.game_id = g.game_id
JOIN Teams t
    ON pp.team_id = t.team_id
JOIN Coaches c
    ON t.coach_id = c.coach_id
JOIN Tournaments tr
    ON pp.tournament_id = tr.tournament_id;
SELECT p.player_name
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id
WHERE g.game_name = 'Football'

UNION

SELECT p.player_name
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id
WHERE g.game_name = 'Cricket';
SELECT p.player_name
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
WHERE pp.game_id = 1

UNION ALL

SELECT p.player_name
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
WHERE pp.game_id = 3;
SELECT player_id
FROM PlayerParticipation
WHERE game_id = 1

INTERSECT

SELECT player_id
FROM PlayerParticipation
WHERE game_id = 5;
SELECT player_name
FROM Players
WHERE player_id IN (
    SELECT player_id
    FROM PlayerParticipation
    WHERE game_id = 1

    INTERSECT

    SELECT player_id
    FROM PlayerParticipation
    WHERE game_id = 5
);
SELECT
    p.player_name,
    p.age,
    g.game_name,
    g.min_age,
    g.max_age,
    CASE
        WHEN p.age BETWEEN g.min_age AND g.max_age
        THEN 'Eligible'
        ELSE 'Not Eligible'
    END AS eligibility
FROM Players p
CROSS JOIN Games g;
SELECT
    p.player_name,
    p.age,
    g.game_name,
    g.min_age,
    g.max_age,
    CASE
        WHEN p.age BETWEEN g.min_age AND g.max_age
        THEN 'Eligible'
        ELSE 'Not Eligible'
    END AS eligibility
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id;
SELECT
    p.player_id,
    p.player_name,
    g.game_name,
    pp.score
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id
ORDER BY pp.score DESC
LIMIT 5;
SELECT
    player_id,
    player_name,
    age,
    gender
FROM Players
ORDER BY age DESC
LIMIT 5;
CREATE VIEW Top5PlayersByScore AS
SELECT
    p.player_id,
    p.player_name,
    g.game_name,
    pp.score
FROM Players p
JOIN PlayerParticipation pp
    ON p.player_id = pp.player_id
JOIN Games g
    ON pp.game_id = g.game_id
ORDER BY pp.score DESC
LIMIT 5;
SELECT * FROM Top5PlayersByScore;
CREATE VIEW Top5PlayersByAge AS
SELECT
    player_id,
    player_name,
    age,
    gender
FROM Players
ORDER BY age DESC
LIMIT 5;
SELECT * FROM Top5PlayersByAge;
