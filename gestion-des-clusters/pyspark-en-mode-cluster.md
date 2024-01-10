# 🐍 Pyspark en mode cluster

## Adapter la configuration

Pour effectuer des traitements avec Sparklyr en mode cluster, il n'y a pas beaucoup de différences avec les traitements en mode local :

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

Notez l'utilisation de l'instruction spark.yarn.queue qui permet de choisir sur quelle file il faut effectuer le traitement. Il peut ne pas exister de file par défaut. Par conséquent, ne pas préciser la file peut amener l'instruction SparkSession.builder() à échouer.
