---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 🐍 Utiliser Spark avec Python

## Configurer Spark en mode local

Dans le précédent chapitre, nous avons appris comment [installer un client pour utiliser Spark](6\_spark\_install.md). Nous allons maintenant réserver des ressources afin de préparer Spark pour notre traitement. Voici la marche à suivre pour se connecter en mode local :

```python
from pyspark.sql import SparkSession

# Configuration des ressources
spark = SparkSession.builder \
    .appName("ExempleJointureSimple") \  # Nom de l'application Spark
    .config("spark.executor.memory", "8g") \  # Mémoire allouée par exécuteur
    .config("spark.executor.cores", 4) \  # Coeurs par exécuteur
    .config("spark.driver.memory", "4g") \  # Mémoire allouée au driver (processus principal)
    .config("spark.driver.cores", 2) \  # Coeurs alloués au driver
    .getOrCreate()
```

Voici un exemple simple de configuration Spark. Les ressources doivent être proportionnelles à la tâche effectuée et aux données traitées par votre application.

## Effectuer des traitements

Voyons désormais comment utiliser ces outils pour effectuer des calculs. Il existe de nombreuses ressources, en particulier la [documentation officielle de Spark](https://spark.apache.org/docs/latest/quick-start.html). Nous allons ici voir des exemples fondamentaux :

* Comment exécuter une requête SQL
* Comment joindre deux tables avec Spark

Ces deux exemples seront traités en PySpark.

Je ne présenterai pas dans ce guide les utilisations avancées de Spark (Gestion des graphs avec GraphX, Machine Learning avec MLlib ou encore le mode streaming). Ces utilisations sont très spécifiques, mais font par ailleurs l'objet de documentation en ligne. Je fais mention de leur existence, car ces librairies sont très puissantes. Elles permettent des applications sur des volumes de données qui ne sont pas comparables avec les autres librairies disponibles sur le marché.

### Faire une requête SQL

Si vous démarrez un processus de conversion de code vers Spark, il est possible de ne pas immédiatement convertir l'ensemble du code. En effet, Spark est tout à fait capable d'exécuter du code SQL. Son moteur de calcul est moins optimisé que lorsqu'il exécute du code Spark. Cependant, cela reste une option intéressante en raison de son faible coût de code, et de ses performances tout à fait raisonnables.

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

### Faire une jointure

Dans cet exemple, deux tables seront créées, mais on pourrait les charger depuis des fichiers dans des Spark DataFrames directement.

<table><thead><tr><th width="76" align="center">id</th><th width="261" align="center">valeur1</th><th width="67" align="center">id</th><th align="center">valeur2</th><th data-hidden></th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">2</td><td align="center">X</td><td></td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">3</td><td align="center">Y</td><td></td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">1</td><td align="center">Z</td><td></td></tr></tbody></table>

On transforme les DataFrames créés en Spark DataFrames avec les noms de colonnes appropriés. Enfin, on performe une jointure sur les deux tables.

<table><thead><tr><th width="73" align="center">id</th><th width="324" align="center">valeur1</th><th align="center">valeur2</th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">Z</td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">X</td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">Y</td></tr></tbody></table>

Voyons comment effectuer cette manipulation en PySpark :

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

Dans les deux exemples, on charge d'abord les données, puis on effectue la jointure entre les deux DataFrames créés. Enfin, on affiche les résultats avant de fermer la session. Même s'il s'agit du mode local, la fermeture de la session est une bonne pratique qu'il faut appliquer systématiquement à la fin d'un code Spark pour libérer les ressources.
