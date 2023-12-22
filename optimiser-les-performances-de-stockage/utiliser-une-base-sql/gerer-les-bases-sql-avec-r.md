# 📊 Gérer les bases SQL avec R

## Travailler avec SQLite

Pour réaliser ce tutoriel, vous aurez besoin de la librairie RSQLite :&#x20;

```r
install.packages("RSQLite")
```

Ensuite, nous pouvons commencer par créer notre base de données SQLite :

```r
library(RSQLite)

db_path <- "chemin/vers/votre/base_de_donnees.db"

# Créer une connexion à la base de données
con <- dbConnect(SQLite(), dbname = db_path)

# Création d'une table "utilisateurs"
dbExecute(con, "CREATE TABLE utilisateurs (id INTEGER PRIMARY KEY, nom TEXT, age INTEGER)")

# Insertion de données dans la table "utilisateurs"
dbExecute(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Alice', 30)")
dbExecute(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Bob', 25)")
dbExecute(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Charlie', 35)")
```

Enfin, interrogeons notre base et déconnectons-nous :&#x20;

```r
result <- dbGetQuery(con, "SELECT * FROM utilisateurs")

# Afficher les résultats
print(result)

dbDisconnect(con)
```

Si vous êtes familier avec le langage SQL, ou que vous avez suivi le cours express sur [les bases SQL](les-bases-sql.md), vous pouvez constater que les éléments supplémentaires liés à la manipulation en R sont minimalistes. Il est possible d'avoir une base fonctionnelle de façon très rapide.

## Travailler avec MariaDB ou MySQL :

Pour réaliser ce tutoriel, vous aurez besoin de la librairie RMySQL :&#x20;

```r
install.packages("RMySQL")
```

Nous allons devoir créer notre base hors de R avant de pouvoir nous y connecter.

```sql
CREATE DATABASE nom_de_la_base;
```

Ensuite, nous pouvons nous connecter pour créer une table et la remplir :

```r
library(RMySQL)

con <- dbConnect(
  MySQL(),
  user = "votre_nom_utilisateur",
  password = "votre_mot_de_passe",
  dbname = "nom_de_votre_base_de_donnees",
  host = "adresse_ip_ou_nom_hote",
  port = numéro_de_port
)

dbSendQuery(con, "CREATE TABLE utilisateurs (id INT AUTO_INCREMENT PRIMARY KEY, nom VARCHAR(50), age INT)")

# Insertion de données dans la table "utilisateurs"
dbSendQuery(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Alice', 30)")
dbSendQuery(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Bob', 25)")
dbSendQuery(con, "INSERT INTO utilisateurs (nom, age) VALUES ('Charlie', 35)")
```

Enfin, interrogeons notre base et déconnectons-nous :

```r
result <- dbGetQuery(con, "SELECT * FROM utilisateurs")

# Afficher les résultats
print(result)

dbDisconnect(con)
```
