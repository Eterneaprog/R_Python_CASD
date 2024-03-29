# 📊 Utiliser Spark via R

## Configurer Spark en mode local

Dans le précédent chapitre, nous avons appris comment [installer un client pour utiliser Spark](installer.md). Nous allons maintenant réserver des ressources afin de préparer Spark pour notre traitement. Voici la marche à suivre pour se connecter en mode local :

```r
library(sparklyr)

# Configuration des ressources
config <- spark_config()

config$spark.executor.memory <- "8g" # Mémoire allouée par exécuteur
config$spark.executor.cores <- 4 # Coeurs par exécuteur
config$spark.driver.memory <- "4g" # Mémoire allouée au driver
config$spark.driver.cores <- 2 # Coeurs alloués au driver

# Création de la connexion Sparklyr
sc <- spark_connect(master = "local", config = config, version = "3.3.2")
```

## Effectuer des traitements

Voyons désormais comment utiliser ces outils pour effectuer des calculs. Il existe de nombreuses ressources, en particulier la [documentation officielle de Spark](https://spark.apache.org/docs/latest/quick-start.html). Nous allons ici voir des exemples fondamentaux :

* Comment exécuter une requête SQL
* Comment joindre deux tables avec Spark

Ces deux exemples seront traités en SparklyR, car ce package présente la même syntaxe que deeplyr. Les deux librairies SparkR et SparklyR permettent d'interagir avec Spark, avec des fonctionnalités similaires. SparklyR est indépendant tandis que SparkR est une librairie officielle de Spark (comme PySpark).

Je ne présenterai pas dans ce guide les utilisations avancées de Spark (Gestion des graphs avec GraphX, Machine Learning avec MLlib ou encore le mode streaming). Ces utilisations sont très spécifiques, mais font par ailleurs l'objet de documentation en ligne. Je fais mention de leur existence, car ces librairies sont très puissantes. Elles permettent des applications sur des volumes de données qui ne sont pas comparables avec les autres librairies disponibles sur le marché.

### Faire une requête SQL

Si vous démarrez un processus de conversion de code vers Spark, il est possible de ne pas immédiatement convertir l'ensemble du code. En effet, Spark est tout à fait capable d'exécuter [du code SQL](../stockage/sql/bases.md). Son moteur de calcul est moins optimisé que lorsqu'il exécute du code Spark. Cependant, cela reste une option intéressante en raison de son faible coût de code, et de ses performances tout à fait raisonnables.

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

Ici, j'ai choisi de faire une requête SQL très simple, composée d'un SELECT, un FROM et un WHERE. Je vais donc récupérer toutes les colonnes de la table, mais en filtrant les lignes selon une colonne particulière. J'ai affiché le résultat, et j'ai fermé la session Spark afin de libérer les ressources.

### Effectuer une jointure simple

Dans cet exemple, deux tables seront créées, mais on pourrait les charger depuis des fichiers dans des Spark DataFrames directement.

<table><thead><tr><th width="76" align="center">id</th><th width="261" align="center">valeur1</th><th width="67" align="center">id</th><th align="center">valeur2</th><th data-hidden></th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">2</td><td align="center">X</td><td></td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">3</td><td align="center">Y</td><td></td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">1</td><td align="center">Z</td><td></td></tr></tbody></table>

On transforme les DataFrames créés en Spark DataFrames avec les noms de colonnes appropriés. Enfin, on performe une jointure sur les deux tables.

<table><thead><tr><th width="73" align="center">id</th><th width="324" align="center">valeur1</th><th align="center">valeur2</th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">Z</td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">X</td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">Y</td></tr></tbody></table>

Voyons comment effectuer cette manipulation :

```r
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
