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

# 🚧 Installer Spark

## Installer Spark

Pour simplifier l'installation de Spark, nous avons conçu un script qui effectue cette installation de façon automatisée. Il est situé dans le dossier Python du dossier Raccourcis de votre bureau. Que vous souhaitiez adresser le logiciel Spark avec une syntaxe proche de R ou de Python, cette étape est nécessaire.

Cliquez sur AutoInstallSpark.bat afin d'effectuer l'installation.

Vous devrez d'abord choisir une version de Spark parmi la liste de celle disponible en saisissant son numéro. Je vous conseille la plus récente.&#x20;

{% hint style="warning" %}
Vous devez attendre la fin du script et qu'il demande d'appuyer sur entrée pour terminer. Il ne faut pas fermer la fenêtre du terminal ouvert pendant le script, cette opération n'est pas très longue. Il suffit d'attendre la copie de l'ensemble des fichiers.
{% endhint %}

Ce script décompresse l'archive contenant Spark, copie les fichiers nécessaires à son utilisation sous Windows, et paramètres les variables d'environnement.

Vous pouvez tester l'installation avec la commande suivante dans un environnement anaconda par exemple (Miniconda Prompt) :

```bash
spark-shell
```

### Installer les autres dépendances de Spark

Les fichiers Jar additionnels dont vous pouvez avoir besoin pour installer des librairies Spark peuvent être obtenus dans le même dossier que pour l'installation de SparklyR : dans S:\Spark\jar\_files. Vous trouverez ici les binaires à copier, par exemple, celui qui permet d'ouvrir un fichier SAS avec Spark : spark-sas7bdat, dans différentes versions. De même, vous pourrez installer parso avec la manœuvre qui suit :

* Copiez le Jar de votre choix dans le dossier : "C:\Users\projet\_0\_p\_nom0000\AppData\Local\spark\spark-X.X.X-bin-hadoopX\jars"

## Accès via R

### Utiliser SparkR

SparkR ne nécessite pas d'installation supplémentaire à proprement parler. Il suffit d'insérer les deux lignes suivantes au début de votre script, qui précisent où se situe la librairie SparkR et démarrent la session.

```r
library(SparkR, lib.loc = c(file.path(Sys.getenv("SPARK_HOME"), "R", "lib")))
sparkR.session(master = "local[*]", sparkConfig = list(spark.driver.memory = "2g"))
```

N'hésitez pas à modifier ou ajouter des éléments à la configuration dans la seconde ligne, afin de choisir des ressources adaptées à votre traitement.

### Installer le package SparklyR

Si vous souhaitez utiliser Spark via une interface R pour soumettre vos instructions au cluster, vous pouvez utiliser la librairie SparklyR. Voici la marche à suivre une fois que l'installation de Spark a été effectuée :

Procédez d'abord à l'installation du package SparklyR à l'aide du dépôt, comme dans les chapitres précédents, puis chargez-le :

```r
install.packages("sparklyr")
library("sparklyr")
```

Ensuite, connectez-vous au cluster :

```r
sc <- spark_connect(master="local")
```

Vous possédez un serveur Spark adressable avec R pour votre application !

## Accès via Python

### Installer PySpark et les Notebook Jupyter

{% hint style="info" %}
Il est nécessaire de posséder un environnement anaconda dans une version compatible avec la version de Spark installée. Par exemple, **pour Spark 3.3.2, Python 3.9 est adapté, mais pas 3.11.** La matrice contenant les versions supportées de [Python pour Spark est disponible ici.](https://community.cloudera.com/t5/Community-Articles/Spark-Python-Supportability-Matrix/ta-p/379144) L'extrait qui nous intéresse est celui-ci :&#x20;
{% endhint %}

| Spark | Python minimum | Python maximum |
| :---: | :------------: | :------------: |
| 3.0.x |       3.4      |       3.8      |
| 3.1.x |       3.6      |       3.9      |
| 3.2.x |       3.6      |       3.9      |
| 3.3.x |       3.7      |      3.10      |
| 3.4.x |       3.7      |      3.11      |
| 3.5.x |       3.8      |      3.11      |

PySpark peut être appelé en choisissant un kernel adapté pour exécuter votre notebook. Ouvrez un miniconda prompt dans la version de votre choix.&#x20;

<pre class="language-python"><code class="lang-python"><strong>conda create --name nom_env python --offline
</strong></code></pre>

Lancez et gardez ouvert le script pip-install-package et saissisez, dans votre miniconda prompt :

```python
pip install pyspark==3.3.2
pip install ipykernel --user
```

La version de votre paquet python Pyspark doit être identique à la version de Spark installée sur votre espace ! Puisqu'il s'agit d'un nouvel environnement dédié aux notebook, ipykernel est également nécéssaire.

Vous pouvez maintenant choisir le kernel adapté dans Visual Studio Code. Attention à choisir le bon kernel, et que l'environnement en question possède le package ipykernel qui permet d'exécuter des notebooks.

En cas d'erreur avec py4j, vous pouvez ajouter deux cellules en entrée de script (avant la création de l'environnement Spark !) :&#x20;

```python
import os 
import sys

os.environ['PYTHON_SPARK'] = sys.executable
os.environ['PYTHON_DRIVER_SPARK'] = sys.executable
```

