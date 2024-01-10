# 🐘 Gestion des données avec HDFS

Le système de fichier distribué distribué HDFS doit être manipulé en ligne de commandes contrairement à l'explorateur de fichier. Cependant, le nombre de commandes à connaître est très limité et elles sont simples. Ces commandes peuvent être utilisées depuis n'importe quel invité de commande (cmd dans la barre de recherche).

Pour l'ensemble de ces commandes, il est nécessaire de posséder l'adresse du NameNode de votre cluster puisque c'est ici que HDFS s'attend à recevoir les données. Vous pouvez le trouver dans les documents spécifiques à votre cluster dans l'espace commun.

## Ajouter des données à HDFS

Il suffit d'utiliser l'instruction -put et de préciser les chemins de fichiers :

```bash
hdfs dfs -put /chemin/vers/le/fichier_source.csv /nom_destination.csv)
```

## Récupérer des données depuis HDFS

Il s'agit de la même commande avec l'instruction -get :

```bash
hdfs dfs -get /chemin-sur-hdfs/fichier.csv /chemin-systeme-local.csv
```

## Utiliser un fichier stocké dans HDFS pour un traitement Spark avec Sparklyr

Lire un CSV ou un fichier parquet peut être fait avec les commandes suivantes (il faut avoir défini un [spark\_connect](sparklyr-en-mode-cluster.md#adapter-la-configuration) au préalable) :&#x20;

```r
spark_read_csv(sc, name = "nom_table", path = "hdfs://adresseNameNode:Port/fichier.csv")
```

```r
spark_read_parquet(sc, name = "nom_table", path = "hdfs://adresseNameNode:Port/fichier.parquet")
```
