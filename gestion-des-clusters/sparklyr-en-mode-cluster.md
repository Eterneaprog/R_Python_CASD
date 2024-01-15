# 📊 Sparklyr en mode cluster

## Adapter la configuration

Pour effectuer des traitements avec Sparklyr en mode cluster, il n'y a pas beaucoup de différences avec les traitements en mode local :

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

Notez la présence du paramètre spark.yarn.queue. Il n'existe pas de file par défaut pour forcer le choix vers une des files adaptées. Ne pas préciser ce paramètre amènera le traitement à échouer !

Une fois cette configuration effectuée, il faut effectuer vos traitements comme vous le feriez en mode local.

Attention à l'instruction collect : elle ramène le dataset vers la machine depuis laquelle vous accédez votre session R ! Si le dataset est de taille très importante, cela peut causer une erreur mémoire, car R chargera ce dataset dans la mémoire de la machine et non sur disque. Cette instruction n'est à réserver qu'aux résultats finaux, avec très peu d'unités. Tant qu'il est possible de l'éviter, il faut le faire.&#x20;

## Modifier les chemins d'accès aux fichiers

Par défaut, si vous possédez une installation pour les clusters, HDFS est votre système de fichier par défaut. Par conséquent, au passage sur le cluster, il est nécessaire de préciser sur quel lecteur se situe votre fichier :

```
spark_read_parquet(sc, "file:///chemin.parquet")
```

C'est ce que l'on peut voir avec l'instruction file:/// qui précise que le système de fichier local doit être utilisé.
