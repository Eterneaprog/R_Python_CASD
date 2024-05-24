# 🔬 Une méthode pour tester son optimisation

Nous avons vu les techniques avancées que Catalyst met en place pour optimiser les temps de calculs dans l'article précédent.  Voyons maintenant comment nous pouvons en tirer profit par un code optimal en tenant compte du comportement de ce module.&#x20;

### Étape 1 : Détecter les engorgements via l'interface graphique

L'interface graphique Spark contient beaucoup d'informations que l'on peut utiliser afin de choisir son optimisation.

Par exemple, on peut regarder l'adéquation de la configuration au code utilisé (les ressources mémoires sont-elles suffisantes/insuffisantes ou surdimensionnées ?)

\[Image ressources]

On peut regarder également s'il y a beaucoup de mouvements de données et des engorgements. Nous avons appris où lire un diagramme DAG dans l'article précédent. Ce que l'on recherche dans ce diagramme est les engorgements. C'est-à-dire, les étapes qui provoquent un ralentissement en bloquant l'ensemble du code. Cela se matérialise souvent par la présence d'un shuffle, qui sont souvent la conséquence d'une instruction de nature Wide :

<figure><img src="../../.gitbook/assets/example partition.png" alt=""><figcaption></figcaption></figure>

Ici, on voit que l'engorgement se fait au moment où l'on passe de l'étape 8 à 9, car il y a lecture et écriture de 58 Giga de données entre les deux étapes. C'est-à-dire, transfert de données.&#x20;

On peut aussi regarder quelles sont les étapes qui consomment le plus de temps (de CPU et de RAM dans le tableau en dessous également). Cet exemple d'Apache Spark montre les étapes du calcul de Pi :

<figure><img src="../../.gitbook/assets/summary.PNG" alt=""><figcaption></figcaption></figure>

On peut alors déterminer dans notre code ce qui est responsable de la durée du traitement. On peut ensuite prendre une décision adaptée en apportant des modifications.\
Il ne faut pas hésiter à explorer cette interface afin de trouver les problèmes.

### Étape 2 : Utiliser une technique pour optimiser

Il existe différentes techniques afin d'optimiser son code, à adapter selon la cause de l'engorgement détectée à l'étape 1. Parmi celles-ci, on trouve, entre autres :&#x20;

* [L'adaptation de la configuration](boite-a-outil-des-optimisations/choisir-une-configuration-spark.md) (efficace lors des saturations mémoires)
* [Éliminer certaines instructions](boite-a-outil-des-optimisations/forcer-les-calculs.md) de son code pour laisser Catalyst optimiser mieux (efficace lorsque le code utilise des collect/compute et est donc très haché)
* [Le choix d'une stratégie de jointure alternative](boite-a-outil-des-optimisations/choisir-sa-strategie-de-jointure.md) (efficace lors d'une jointure)
* [L'utilisation d'un cache](boite-a-outil-des-optimisations/utiliser-le-cache-pour-ameliorer-ses-calculs.md) (efficace lors de la réutilisation d'une table)
* [Le partitionnement d'une table](boite-a-outil-des-optimisations/partitionner-une-table-selon-une-variable.md) selon une variable bien choisie (efficace lorsque l'on va utiliser une table par une variable précise par la suite).

### Étape 3 : Comparer avec ou sans l'optimisation

Une fois votre stratégie d'optimisation définie, vous pouvez effectuer un benchmark pour comparer si la stratégie d'optimisation a permis de réduire le temps de calcul. En utilisant le Spark UI, vous pouvez obtenir la durée de traitement ou alors définir dans votre code des balises de temps pour mesurer la durée d'une fonction :&#x20;

En pyspark :

```python
from pyspark.sql import SparkSession
import time

def my_spark_function():
    spark = SparkSession.builder.appName("mon_application").getOrCreate()
    
    # Transformations
    df = spark.read.csv("chemin/vers/votre/fichier.csv", header=True, inferSchema=True)
    result_df = df.groupBy("colonne").count()
    
    # Action
    result_df.show()

start_time = time.time()
my_spark_function()
end_time = time.time()
duration = end_time - start_time

# Affichez la durée
print(f"La fonction Spark a mis {duration} secondes pour s'exécuter.")
```

En SparklyR :&#x20;

```r
library(sparklyr)
library(dplyr)
library(SparkR)
library(SparkR::sparklyr)

my_spark_function <- function() {
  spark <- spark_connect(master = "local", version = "3.0.2")
  
  # Traitement
  df <- spark_read_csv(spark, "chemin/vers/votre/fichier.csv", header = TRUE, infer_schema = TRUE)
  result_df <- df %>% group_by(colonne) %>% summarize(count = n())

  # Action
  spark_print(result_df)
}

start_time <- Sys.time()
my_spark_function()
end_time <- Sys.time()

duration <- end_time - start_time

cat(paste("La fonction Spark a mis", as.numeric(duration), "secondes pour s'exécuter.\n"))
```
