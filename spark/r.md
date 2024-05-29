# 🌠 Utiliser Spark

Trois façons d'accéder à Spark via R sont supportées au CASD. Il est possible d'utiliser la librairie officiellement supportée par Spark pour R : SparkR

Une alternative à la syntaxe très proche de dplyr est également disponible : Sparklyr.

Enfin, il est possible d'utiliser PySpark !

SparkR et PySpark sont les options les plus performantes et proposent une meilleure explication de ces traitements grâce à [des DAG détaillés](dag/les-plans-dexecutions-et-catalyst.md).

Dans cet article, vous pouvez passer d'une syntaxe à l'autre avec les onglets !

## Configurer Spark en mode local

Dans le précédent chapitre, nous avons appris comment [installer un client pour utiliser Spark](installer.md). Nous allons maintenant réserver des ressources afin de préparer Spark pour notre traitement. Voici la marche à suivre pour se connecter en mode local :&#x20;

{% tabs %}
{% tab title="PySpark" %}
{% code overflow="wrap" %}
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
{% endcode %}
{% endtab %}

{% tab title="SparkR" %}
<pre class="language-r" data-overflow="wrap"><code class="lang-r"><strong>library(SparkR)
</strong>
# Initialisation d'une session Spark en mode local
sparkR.session(master = "local[*]", appName = "SparkR-Example")

# Vérification de la session
sparkSession &#x3C;- sparkR.session()
</code></pre>
{% endtab %}

{% tab title="Sparklyr" %}
{% code overflow="wrap" %}
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
{% endcode %}
{% endtab %}
{% endtabs %}

Voici un exemple simple de configuration Spark. Les ressources doivent être proportionnelles à la tâche effectuée et aux données traitées par votre application.

## Effectuer des traitements

Voyons désormais comment utiliser ces outils pour effectuer des calculs. Il existe de nombreuses ressources, en particulier la [documentation officielle de Spark](https://spark.apache.org/docs/latest/quick-start.html). Nous allons ici voir des exemples fondamentaux :

* Comment exécuter une requête SQL
* Comment joindre deux tables avec Spark

Ces deux exemples seront traités en SparklyR, car ce package présente la même syntaxe que deeplyr. Les deux librairies SparkR et SparklyR permettent d'interagir avec Spark, avec des fonctionnalités similaires. SparklyR est indépendant tandis que SparkR est une librairie officielle de Spark (comme PySpark).

Je ne présenterai pas dans ce guide les utilisations avancées de Spark (Gestion des graphs avec GraphX, Machine Learning avec MLlib ou encore le mode streaming). Ces utilisations sont très spécifiques, mais font par ailleurs l'objet de documentation en ligne. Je fais mention de leur existence, car ces librairies sont très puissantes. Elles permettent des applications sur des volumes de données qui ne sont pas comparables avec les autres librairies disponibles sur le marché.

### Faire une requête SQL

Si vous démarrez un processus de conversion de code vers Spark, il est possible de ne pas immédiatement convertir l'ensemble du code. En effet, Spark est tout à fait capable d'exécuter [du code SQL](../stockage/sql/bases.md). Son moteur de calcul est moins optimisé que lorsqu'il exécute du code Spark. Cependant, cela reste une option intéressante en raison de son faible coût de code, et de ses performances tout à fait raisonnables.

Une fois l'environnement configuré comme expliqué dans le chapitre précédent, exécuter une requête SQL s'effectue de la manière suivante :

{% tabs %}
{% tab title="PySpark" %}
<pre class="language-python" data-overflow="wrap"><code class="lang-python"><strong># Charger une table Spark depuis un fichier Parquet :
</strong>df = spark.read.parquet("/chemin/vers/France.parquet")
df.createOrReplaceTempView("France")

# Exécution d'une requête SQL sur la table
result = spark.sql("SELECT region, count(departement) FROM France GROUP BY region")

# Afficher le résultat
result.show()
</code></pre>
{% endtab %}

{% tab title="SparkR" %}
```r
# Charger une table Spark depuis un fichier Parquet :
df <- read.parquet("/chemin/vers/France.parquet")
createOrReplaceTempView(df, "parquet_table")

# Exécution d'une requête SQL sur la table
result <- sql("SELECT region, count(departement) FROM France GROUP BY region")

# Affichage des résultats
showDF(result)
```
{% endtab %}

{% tab title="Sparklyr" %}
{% code overflow="wrap" %}
```r
# Charger une table Spark depuis un fichier Parquet :
spark_read_table(sc, "France", source = "parquet", path = "/chemin/vers/France.parquet")

# Exécution d'une requête SQL sur la table
result <- sparklyr::spark_session(sc) %>%
  sparklyr::invoke("sql", "SELECT region, count(departement) FROM France GROUP BY region")

# Affichage des résultats
show(result)
```
{% endcode %}
{% endtab %}
{% endtabs %}

J'ai ici imaginé une table France, contenant les départements et leur région d'appartenance. J'ai compté le nombre de départements par région en utilisant un group by. De plus, il faut toujours fermer sa session avec spark.stop().

### Effectuer une jointure simple

Dans cet exemple, deux tables seront créées, mais on pourrait les charger depuis des fichiers dans des Spark DataFrames directement.

<table><thead><tr><th width="76" align="center">id</th><th width="261" align="center">valeur1</th><th width="67" align="center">id</th><th align="center">valeur2</th><th data-hidden></th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">2</td><td align="center">X</td><td></td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">3</td><td align="center">Y</td><td></td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">1</td><td align="center">Z</td><td></td></tr></tbody></table>

On transforme les DataFrames créés en Spark DataFrames avec les noms de colonnes appropriés. Enfin, on performe une jointure sur les deux tables.

<table><thead><tr><th width="73" align="center">id</th><th width="324" align="center">valeur1</th><th align="center">valeur2</th></tr></thead><tbody><tr><td align="center">1</td><td align="center">A</td><td align="center">Z</td></tr><tr><td align="center">2</td><td align="center">B</td><td align="center">X</td></tr><tr><td align="center">3</td><td align="center">C</td><td align="center">Y</td></tr></tbody></table>

Voyons comment effectuer cette manipulation :

{% tabs %}
{% tab title="PySpark" %}
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
{% endtab %}

{% tab title="SparkR" %}
```r
# Créer deux DataFrames
data1 <- list(list(1, "A"), list(2, "B"), list(3, "C"))
data2 <- list(list(1, "Z"), list(2, "X"), list(3, "Y"))

columns1 <- c("id", "valeur1")
columns2 <- c("id", "valeur2")

df1 <- createDataFrame(data1, schema = columns1)
df2 <- createDataFrame(data2, schema = columns2)

# Effectuer la jointure
result <- join(df1, df2, df1$id == df2$id, "inner")

# Afficher le résultat
showDF(result)
sparkR.session.stop()
```
{% endtab %}

{% tab title="Sparklyr" %}
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
{% endtab %}
{% endtabs %}
