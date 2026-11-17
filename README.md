# Worldcup_database
A Bash script that enters information from World Cup games into PostgreSQL, then query the database for useful statistics

D'un simple fichier CSV à une base de données relationnelle interrogeable : tout le Mondial 2014 et 2018 en PostgreSQL, alimenté et analysé en Bash.

Projet réalisé dans le cadre du cursus **Relational Database** de [freeCodeCamp](https://www.freecodecamp.org/).

1) 🎯 L'idée

Un fichier `games.csv` contient les résultats des phases finales des Coupes du monde 2014 et 2018. Le script lit ce fichier ligne par ligne, construit les tables, puis des requêtes SQL répondent à des questions comme :

- Qui a gagné chaque Coupe du monde ?
- Combien de buts ont été marqués en moyenne par match ?
- Quelles équipes se sont affrontées en huitièmes de finale ?
- 
📊 En chiffres

- 2 tournois : 2014 et 2018
- 32 matchs
- 24 équipes
- 2 tables reliées par clés étrangères

🏆 Champions : Allemagne (2014), France (2018)

2) 🗂️ Structure de la base

    TEAMS {
        int team_id PK
        varchar name UK
    }
    
    GAMES {
        int game_id PK
        int year
        varchar round
        int winner_id FK
        int opponent_id FK
        int winner_goals
        int opponent_goals
    }

🧰 Ce que le projet met en pratique

- PostgreSQL : création de tables, clés primaires et étrangères, contrainte d'unicité
- Bash : lecture d'un CSV avec `while read`, variables, conditions
- SQL : `JOIN`, `SUM`, `AVG`, `ROUND`, `COUNT`, `DISTINCT`, `LIKE`, `ORDER BY`
- Sauvegarde : export de la base avec `pg_dump`

 📁 Les fichiers

| Fichier | Rôle |
|---|---|
| `games.csv` | Les données brutes des matchs |
| `insert_data.sh` | Remplit les tables `teams` et `games` à partir du CSV, sans doublons d'équipes |
| `queries.sh` | Lance 13 requêtes d'analyse et affiche les résultats |
| `worldcup.sql` | Sauvegarde complète de la base |

## ▶️ Lancer le projet

Prérequis :PostgreSQL installé `worldcup.sql` commence par `DROP DATABASE worldcup;`. Si tu as déjà une base de ce nom, elle sera supprimée.

bash
 
1. Restaurer la base
psql --username=freecodecamp -f worldcup.sql

2. (Optionnel) Recharger les données depuis le CSV
./insert_data.sh

3. Lancer les requêtes d'analyse
./queries.sh
<img width="656" height="984" alt="RESULTAT" src="https://github.com/user-attachments/assets/3d1b5fdb-ca2c-4b41-aca2-70d8f219bf40" />



## 🔎 Exemple de requête

Les champions de chaque édition :

sql
SELECT year, name
FROM teams
INNER JOIN games ON teams.team_id = games.winner_id
WHERE round = 'Final'
ORDER BY year;



## 👤 Auteur

** AGBO Edem ** · Responsable administratif et financier, développeur Full-Stack junior en formation
📍 Lomé, Togo · [GitHub](https://github.com/EDEMOF3105)
