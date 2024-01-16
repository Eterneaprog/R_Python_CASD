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

## Les éléments nécessaires

### Installer Spark

Pour simplifier l'installation de Spark, nous avons conçu un script qui effectue cette installation de façon automatisée. Il est situé dans l'espace commun. Que vous souhaitiez adresser le logiciel Spark avec une syntaxe proche de R ou de Python, cette étape est nécessaire.

Cliquez sur AutoInstallSpark.bat afin d'effectuer l'installation.

**Attention :** Vous devez attendre la fin du script et qu'il demande d'appuyer sur entrée pour terminer. Il ne faut pas fermer la fenêtre du terminal ouvert pendant le script, cette opération n'est pas très longue.

Ce script décompresse l'archive contenant Spark, copie les fichiers nécessaires à son utilisation sous Windows, et paramètres les variables d'environnement.

Vous pouvez tester l'installation avec la commande suivante dans un terminal de commande (cmd) :

```bash
spark-shell
```

### Installer le package SparklyR pour travailler avec SparkR dans Rstudio

Si vous souhaitez utiliser SparkR pour soumettre vos instructions au cluster, vous aurez besoin de la librairie SparklyR. Voici la marche à suivre une fois que l'installation de Spark a été effectuée :

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

### Installer PySpark et adresser le cluster avec un Notebook Jupyter

PySpark est inclus nativement avec Spark. Une fois l'installation de Spark effectuée avec le script fourni, vous pouvez accéder à Pyspark dans votre application avec la commande :

```bash
pyspark
```

### Installer les autres dépendances de Spark

Les fichiers Jar additionnels dont vous pouvez avoir besoin pour installer des librairies Spark peuvent être obtenus dans le même dossier que pour l'installation de SparklyR : dans S:\Spark\jar\_files. Vous trouverez ici les binaires à copier, par exemple, celui qui permet d'ouvrir un fichier SAS avec Spark : spark-sas7bdat, dans différentes versions. De même, vous pourrez installer parso avec la manœuvre qui suit :

* Copiez le Jar de votre choix dans le dossier : "C:\Users\projet\_0\_p\_nom0000\AppData\Local\spark\spark-3.3.2-bin-hadoop2\jars"

