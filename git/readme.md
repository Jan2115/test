-- Tabela użytkowników
CREATE TABLE Users (
    user_id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    password_hash VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE,
    role VARCHAR(20) -- np. 'admin' lub 'user'
);

-- Tabela zawodników
CREATE TABLE Players (
    player_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    age INT,
    team_id INT REFERENCES Teams(team_id)
);

-- Tabela drużyn
CREATE TABLE Teams (
    team_id SERIAL PRIMARY KEY,
    team_name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT NOW()
);

-- Tabela turniejów
CREATE TABLE Tournaments (
    tournament_id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    start_date DATE,
    end_date DATE,
    tournament_type VARCHAR(50)
);

-- Tabela łącząca turnieje i zawodników
CREATE TABLE Tournament_Players (
    tournament_id INT REFERENCES Tournaments(tournament_id),
    player_id INT REFERENCES Players(player_id),
    PRIMARY KEY (tournament_id, player_id)
);

-- Tabela meczów
CREATE TABLE Matches (
    match_id SERIAL PRIMARY KEY,
    tournament_id INT REFERENCES Tournaments(tournament_id),
    team1_id INT REFERENCES Teams(team_id),
    team2_id INT REFERENCES Teams(team_id),
    match_date TIMESTAMP,
    team1_score INT DEFAULT 0,
    team2_score INT DEFAULT 0
);

-- Tabela wyników meczów
CREATE TABLE Match_Results (
    result_id SERIAL PRIMARY KEY,
    match_id INT REFERENCES Matches(match_id),
    player_id INT REFERENCES Players(player_id),
    points INT
);
