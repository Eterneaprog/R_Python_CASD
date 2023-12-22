# 🐍 Gérer les bases SQL avec Python

## Travailler avec SQLite

Pour réaliser ce tutoriel, vous aurez besoin de la librairie sqlite3 qui est intégrée à python (il n'est pas nécessaire d'effectuer d'installation avec pip) :&#x20;

```r
import sqlite3
```

Créez un fichier .db vide à l'endroit où vous souhaitez créer la base (avec VSCode par exemple). Ensuite, nous pouvons créer notre table dans la base de données SQLite :

```python
import sqlite3

# Créer une connexion à la base de données SQLite
conn = sqlite3.connect('chemin/vers/votre/base_de_donnees.db')

# Créer un curseur pour exécuter des commandes SQL
cursor = conn.cursor()

# Création d'une table "utilisateurs" et insertion de données
cursor.execute('''CREATE TABLE utilisateurs (id INTEGER PRIMARY KEY, nom TEXT, age INTEGER)''')
cursor.execute('''INSERT INTO utilisateurs (nom, age) VALUES (?, ?)''', ('Alice', 30))
cursor.execute('''INSERT INTO utilisateurs (nom, age) VALUES (?, ?)''', ('Bob', 25))
cursor.execute('''INSERT INTO utilisateurs (nom, age) VALUES (?, ?)''', ('Charlie', 35))

# Valider les modifications et fermer la connexion
conn.commit()
conn.close()
```

Enfin, interrogeons notre base :&#x20;

```python
conn = sqlite3.connect('chemin/vers/votre/base_de_donnees.db')

# Créer un curseur pour exécuter des commandes SQL
cursor = conn.cursor()

# Exécution d'une requête SELECT pour récupérer des données depuis la table "utilisateurs"
cursor.execute('''SELECT * FROM utilisateurs''')

# Récupérer les résultats de la requête SELECT
result = cursor.fetchall()

# Afficher les résultats
for row in result:
    print(row)

conn.close()
```

## Travailler avec MariaDB / MySQL

A venir.
