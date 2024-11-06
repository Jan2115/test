Projekt malej bazy danych, odpowiadajacej za:
- logowanie uzytkownikow
- informacje o zawodnikach, polaczonych z druzynami i rozgrywkami
- dane druzyn
- rozgryweki i ich typ
- mecze przyporzadkowane do rozgrywek i ich wynikow
- tabele rozgrywek
  
```
CREATE TABLE uzytkownicy (
    id SERIAL PRIMARY KEY,
    nick VARCHAR(20) NOT NULL,
    haslo VARCHAR(30) NOT NULL,
    email VARCHAR(25) UNIQUE,
    rola VARCHAR(10),
);

CREATE TABLE zawodnicy (
    zawodnik_id SERIAL PRIMARY KEY,
    imie VARCHAR(20) NOT NULL,
    nazwisko VARCHAR(20) NOT NULL,
    wiek INT,
    druzyna_id INT REFERENCES druzyny(druzyna_id),
);

CREATE TABLE druzyny (
    druzyna_id SERIAL PRIMARY KEY,
    druzyna_nazwa VARCHAR(30) NOT NULL,
    utworzono TIMESTAMP DEFAULT NOW(),
);

CREATE TABLE Rozgrywki (
    turniej_id SERIAL PRIMARY KEY,
    nazwa VARCHAR(30) NOT NULL,
    start_data DATE,
    koniec_data DATE,
    turniej_typ VARCHAR(10),
);

CREATE TABLE Rozgrywki_zawodnicy (
    turniej_id INT REFERENCES Rozgrywki(turniej_id),
    zawodnik_id INT REFERENCES zawodnicy(zawodnik_id),
    PRIMARY KEY (turniej_id, zawodnik_id),
);

CREATE TABLE Mecze (
    mecz_id SERIAL PRIMARY KEY,
    turniej_id INT REFERENCES Rozgrywki(turniej_id),
    druzyna1_id INT REFERENCES druzyny(druzyna_id),
    druzyna2_id INT REFERENCES druzyny(druzyna_id),
    mecz_data TIMESTAMP,
    druzyna1_wynik INT DEFAULT 0,
    druzyna2_wynik INT DEFAULT 0,
);

CREATE TABLE Mecz_wyniki (
    wynik_id SERIAL PRIMARY KEY,
    mecz_id INT REFERENCES Mecze(mecz_id),
    zawodnik_id INT REFERENCES zawodnicy(zawodnik_id),
    punkty INT,
);
```
    
