# Utiliser Spark pour faire des calculs

Dans les précédents chapitres, nous avons appris comment installer un client pour utiliser Spark, en mode Local ou en mode Cluster. Nous avons également appris comment demander des ressources, et fermer notre session. Voyons maintenant comment utiliser ces outils afin d'effectuer des calculs. Il existe de nombreuses ressources, en particulier la [documentation officielle de Spark](https://spark.apache.org/docs/latest/quick-start.html). Nous allons ici voir des exemples fondamentaux :

- Comment exécuter une requête SQL
- Comment joindre deux tables avec Spark

Ces deux exemples seront traités en SparklyR et PySpark.

Je ne présenterai pas dans ce guide les utilisations avancées de Spark (Gestion des graph avec GraphX, machine Learning avec MLlib ou encore le mode streaming). Ces utilisations sont très spécifiques, mais font également l'objet de documentation en ligne. Nous faisons mention de leur existence car ces librairies sont très puissantes. Elles permettent des applications sur des volumes de données qui ne sont pas comparables avec les autres librairies disponibles sur le marché.

## Exécuter une requête SQL

Si vous démarrez un processus de conversion de code vers Spark, il est possible de ne pas immédiatement convertir l'ensemble du code. En effet, Spark est tout à fait capable d'exécuter du code SQL. Son moteur de calcul est moins optimisé que lorsqu'il exécute du code Spark. Cependant, cela reste une option intéressante en raison de son faible coût de code, et de ses performances tout à fait raisonnables.

### SparklyR

Une fois l'environnement configuré comme expliqué dans le chapitre précédent, exécuter une requête SQL s'effectue de la manière suivante :

```r
# Charger une table au format parquet
spark_read_table(sc, "nom_table", source = "parquet", path = "/chemin/vers/le/fichier.parquet")

# Exécuter une requête SQL
result <- sparklyr::spark_session(sc) %>%
  sparklyr::invoke("sql", "SELECT * FROM nom_table WHERE colonne = 'valeur'")

# Afficher le résultat
show(result)
spark_disconnect(sc)
```

Ici, j'ai choisi de faire une requête SQL très simple, composée d'un SELECT, un FROM et un WHERE. Je vais donc récupérer tout les colonnes de la table, mais en filtrant les lignes selon une colonne particulière.
J'ai affiché le résultat, et j'ai fermé la session Spark afin de libérer les ressources.

### PySpark

On suppose ici aussi que l'environnement est initialisé, cette fois, faisons une agrégation :

```python
# Charger une table Spark temporaire depuis un fichier Parquet :
df = spark.read.parquet("/chemin/vers/France.parquet")
df.createOrReplaceTempView("France")

# Exécuter une requête SQL
result = spark.sql("SELECT region, count(departement) FROM France GROUP BY region")

# Afficher le résultat
result.show()
spark.stop()
```

J'ai ici imaginé une table France, contenant les départements et leur région d'appartenance. J'ai compté le nombre de départements par région en utilisant un group by. De plus, il faut toujours fermer sa session avec spark.stop().

## Effectuer une jointure simple

Dans cette exemple, deux tables seront créés, mais on pourrait les charger depuis des fichiers dans des Spark DataFrames directement.

| id | valeur1 |   | id | valeur2 |
|:--:|:-------:|:-:|:--:|:-------:|
|  1 |    A    |   |  2 |    X    |
|  2 |    B    |   |  3 |    Y    |
|  3 |    C    |   |  1 |    Z    |

On transforme les dataframes créés en Spark DataFrames avec les noms de colonnes appropriés. Enfin, on performe une jointure sur les deux tables.

| id | valeur1 | valeur2 |
|:--:|:-------:|:-------:|
|  1 |    A    |    Z    |
|  2 |    B    |    X    |
|  3 |    C    |    Y    |

Voyons comment effectuer cette manipulation en SparklyR et en PySpark.

### SparklyR

```R
# Créer deux data frames
df1 <- data.frame(id = c(1, 2, 3), value1 = c("A", "B", "C"))
df2 <- data.frame(id = c(1, 2, 3), value2 = c("Z", "X", "Y"))

# Convertir les data frames en DataFrames Spark
sdf1 <- sdf_copy_to(sc, df1, "df1")
sdf2 <- sdf_copy_to(sc, df2, "df2")

# Effectuer la jointure
result <- inner_join(sdf1, sdf2, by = "id")

# Afficher le résultat
show(result)
spark_disconnect(sc)
```

### PySpark

```python

# Créer deux DataFrames
data1 = [(1, "A"), (2, "B"), (3, "C")]
data2 = [(1, "Z"), (2, "X"), (3, "Y")]

columns1 = ["id", "valeur1"]
columns2 = ["id", "valeur2"]

df1 = spark.createDataFrame(data1, columns1)
df2 = spark.createDataFrame(data2, columns2)

# Effectuer la jointure
result = df1.join(df2, "id", "inner")

# Afficher le résultat
result.show()
spark.stop()
```

Dans les deux exemples, on charge d'abord les données, puis ont effectue la jointure entre les deux dataframes créés. Enfin, on affiche les résultats avant de fermer la session. Même s'il s'agit du mode local, la fermeture de la session est une bonne pratique qu'il faut appliquer systématiquement à la fin d'un code Spark pour libérer les ressources.