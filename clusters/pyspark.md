# 🌠 Spark en mode cluster

## Adapter la configuration

Pour effectuer des traitements avec Spark en mode cluster, il n'y a pas beaucoup de différences avec les traitements en mode local :&#x20;

{% hint style="danger" %}
Notez l'utilisation de l'instruction spark.yarn.queue qui permet de choisir sur quelle file il faut effectuer le traitement. Il peut ne pas exister de file par défaut. Par conséquent, ne pas préciser la file peut amener l'instruction SparkSession.builder() à échouer.
{% endhint %}

{% tabs %}
{% tab title="PySpark" %}
```python
from pyspark.sql import SparkSession

# Configuration des ressources pour le cluster
spark = SparkSession.builder \
    .appName("MonApplication") \  # Nom de l'application Spark
    .config("spark.executor.memory", "8g") \  # Mémoire allouée par exécuteur
    .config("spark.executor.cores", 4) \  # Coeurs par exécuteur
    .config("spark.driver.memory", "4g") \  # Mémoire allouée au driver
    .config("spark.driver.cores", 2) \  # Coeurs alloués au driver
    .config("spark.yarn.queue", "prod") \ #Selection de la file d'exécution
    .config("spark.master", "yarn") \
    .getOrCreate()
```
{% endtab %}

{% tab title="SparkR" %}
{% code overflow="wrap" %}
```r
# Chargement de la bibliothèque SparkR
library(SparkR)

# Configuration des ressources pour le cluster
sparkR.session(
  master = "yarn",
  appName = "MonApplication",         # Nom de l'application Spark
  sparkConfig = list(
    "spark.executor.memory" = "8g",   # Mémoire allouée par exécuteur
    "spark.executor.cores" = 4,       # Coeurs par exécuteur
    "spark.driver.memory" = "4g",     # Mémoire allouée au driver
    "spark.driver.cores" = 2,         # Coeurs alloués au driver
    "spark.yarn.queue" = "prod"       # Sélection de la file d'exécution
  )
)
```
{% endcode %}
{% endtab %}

{% tab title="Sparklyr" %}
```r
library(sparklyr)
library(dplyr)

# Insérer ici vos configurations personelles pour votre session
conf <- spark_config() 
conf["spark.driver.memory"] <- "16g"
conf["spark.executor.memory"] <- "8g"
conf["spark.executor.core"] <- 4
conf["spark.executor.instances"] <- 2
conf["spark.yarn.queue"] <- "prod"

# Création de la connexion Sparklyr en mode cluster
sc <- spark_connect(master = "yarn", config = conf)
```

Une fois cette configuration effectuée, il faut effectuer vos traitements comme vous le feriez en mode local.

Attention à l'instruction collect : elle ramène le dataset vers la machine depuis laquelle vous accédez votre session R ! Si le dataset est de taille très importante, cela peut causer une erreur mémoire, car R chargera ce dataset dans la mémoire de la machine et non sur disque. Cette instruction n'est à réserver qu'aux résultats finaux, avec très peu d'unités. Tant qu'il est possible de l'éviter, il faut le faire.&#x20;

## Modifier les chemins d'accès aux fichiers

Par défaut, si vous possédez une installation pour les clusters, HDFS est votre système de fichier par défaut. Par conséquent, au passage sur le cluster, il est nécessaire de préciser sur quel lecteur se situe votre fichier :

```
spark_read_parquet(sc, "file:///chemin.parquet")
```

C'est ce que l'on peut voir avec l'instruction file:/// qui précise que le système de fichier local doit être utilisé.
{% endtab %}
{% endtabs %}
