# 🐘 Gestion des données avec HDFS

Le système de fichier distribué distribué HDFS peut être manipulé en ligne de commandes ou en interface graphique, comme l'explorateur de fichiers. Le nombre de commandes à connaître est très limité et elles sont simples. Ces commandes peuvent être utilisées depuis n'importe quel invité de commande (cmd dans la barre de recherche).&#x20;

L'organisation du système dans votre bulle est la suivante :&#x20;

<figure><img src="../.gitbook/assets/HDFS (1).png" alt=""><figcaption><p>Dans la bulle équipée d'un cluster, on peut persister ses données avec le système de fichier local ou HDFS !</p></figcaption></figure>

On voit que l'on peut d'abord monter des données du système de fichier local vers HDFS avec l'instruction -put. Puis, utiliser ces données avec la commande spark\_read\_csv qui permet de lire depuis un système de fichier distribué. \
\
Une fois le calcul achevé, on peut persister notre résultat avec spark\_write\_csv sur HDFS. Enfin, s'il est nécessaire de persister ces données sur le système de fichier local, on peut les télécharger avec l'interface graphique, ou avec hdfs dfs -get !

## Ajouter des données à HDFS depuis le système de fichier local

Il suffit d'utiliser l'instruction -put et de préciser les chemins de fichiers :

```bash
hdfs dfs -put /chemin/vers/le/fichier_source.csv /nom_destination.csv)
```

## Ajouter des données sur le système local depuis HDFS&#x20;

Il s'agit de la même commande avec l'instruction -get :

```bash
hdfs dfs -get /chemin-sur-hdfs/fichier.csv /chemin-systeme-local.csv
```

## Ajouter un fichier à la RAM du cluster depuis HDFS&#x20;

Lire un CSV ou un fichier parquet peut être fait avec les commandes suivantes (il faut avoir défini un [spark\_connect](pyspark.md) au préalable) :&#x20;

```r
spark_read_csv(sc, name = "nom_table", path = "hdfs://chemin/fichier.csv")
```

```r
spark_read_parquet(sc, name = "nom_table", path = "hdfs://chemin/fichier.parquet")
```

## Ajouter des données dans HDFS depuis la RAM du cluster

Écrire un CSV ou un fichier parquet peut être fait avec les commandes suivantes (il faut avoir défini un [spark\_connect](pyspark.md) au préalable) :&#x20;

```r
spark_write_csv(sc, spark_dataframe, path = "hdfs://chemin/fichier.csv")
```

```r
spark_write_parquet(sc, spark_dataframe, path = "hdfs://chemin/fichier.parquet")
```
