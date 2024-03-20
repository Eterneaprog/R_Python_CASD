# 📊 DuckDB avec R

Avant toute chose, installer le package DuckDB est obligatoire pour les manipulations qui vont suivre :

<pre><code><strong>install.packages("duckdb")
</strong></code></pre>

## Interroger un fichier parquet :

Exécuter une [requête SQL](../sql/bases.md#la-syntaxe-sql-pour-effectuer-des-requetes) sur un fichier parquet avec duckDB ne prend que 4 lignes !

```r
library("duckdb")

con <- dbConnect(duckdb())

con.execute("SELECT * FROM 'exemple.parquet';")

print(con)

```

## [Créer, remplir](../sql/bases.md#creer-des-tables-et-inserer-des-donnees) et interroger sa propre base

Ce n'est pas beaucoup plus compliqué puisqu'il suffit d'utiliser la syntaxe SQL classique :

```r
library("DBI")

# Connexion à la base de données en mémoire
con <- dbConnect(duckdb::duckdb(), dbdir=":memory:")

# Création d'une table
dbExecute(con, "CREATE TABLE users (id INTEGER, name VARCHAR)")
# Insertion de données dans la table
dbExecute(con, "INSERT INTO users VALUES (1, 'Alice')")

# Exécution d'une requête
result <- dbGetQuery(con, "SELECT * FROM users")
print(res)

# Fermeture de la connexion
dbDisconnect()
```

