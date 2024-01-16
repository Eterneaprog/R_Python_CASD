# 🐍 DuckDB avec Python

Vous aurez besoin du package duckdb qui est disponible sur notre serveur local. Il peut être installé avec la [procédure classique](../../paquets/python.md), n'oubliez pas de lancer le script pip-install-packages et d'activer votre environnement avant d'effectuer la commande `pip install duckdb`.

## Faire des requêtes [SQL](../sql/bases.md) sur un fichier parquet grâce à [DuckDB](comprendre.md)

Interrogeons d'abord un fichier parquet :

```python
import duckdb

duckdb.sql('SELECT * FROM "exemple.parquet";') 
```

On observe que c'est très simple et que la syntaxe utilisée est celle de SQL

## Créer votre propre base et la remplir

Vous aurez de nouveau besoin de la librairie duckDB

Ensuite, il est possible de mettre en place votre base en mémoire, la remplir, l'interroger et d'afficher le résultat !

{% code fullWidth="false" %}
```python
import duckdb

# Connexion à la base de données en mémoire
conn = duckdb.connect(database=':memory:', read_only=False)

# Création d'une table
conn.execute("CREATE TABLE users (id INTEGER, name VARCHAR)")

# Insertion de données dans la table
conn.execute("INSERT INTO users VALUES (1, 'Alice')")

# Exécution d'une requête
result = conn.execute("SELECT * FROM users")
data = result.fetchdf()
print(data)

# Fermeture de la connexion
conn.close()
```
{% endcode %}
