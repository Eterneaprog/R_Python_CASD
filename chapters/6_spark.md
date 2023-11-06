# Utiliser un cluster spark

## Principes généraux

> _Qu'est ce qu'un cluster Spark ?_
> 
> Un cluster est un regroupement de machines de travail (les workers), sous la direction d'une machine maître (le master). Le master se charge de distribuer le travail sur les différents machines de travail et de collecter les résultats. Cela permet de travailler de façon parallèle, et donc de gagner du temps. Spark est le logiciel avec lequel vous allez échanger pour faire fonctionner ce cluster. Vous pouvez écrire vos instructions dans une syntaxe plus proche du R : c'est SparkR, ou bien avec une syntaxe proche du Python : c'est PySpark !

Voici un aperçu simplifié du fonctionnement de votre cluster :

<img src="/assets/images/spark.png" alt="Git"/>

Un cluster spark est un outil puissant qui permet d'accélérer grandement la vitesse d'éxecution de vos calculs. De plus, la puissance du cluster et sa taille sont plus modulables qu'une machine seule à laquelle on ajoute des ressources : il suffit d'ajouter des workers. Cependant, l'utilisation de cet outil n'est pas toujours aussi aisé que lorsque l'on s'adresse une machine seule avec R. Voyons d'abord comment installer les paquets nécessaires pour pouvoir s'adresser au cluster en R, puis en python. Ensuite, nous verrons comment réserver des ressources (il s'agit du la notion de Spark Context sur le schéma) et enfin comment utiliser notre cluster pour effectuer des calculs simples.

## Effectuer les installations nécéssaires

### Installer le package sparklyr pour travailler avec SparkR dans Rstudio server

Si vous souhaitez utiliser sparkR pour soumettre vos instructions au cluster, vous aurez besoin de la librairie sparklyR. Voici la marche à suivre pour faire les installations qui vous permettent de vous adresser à un cluster spark avec R : 

Procédez d'abord à l'installation du package sparklyr à l'aide du dépôt, comme dans les chapitres précédents, puis chargez le:

```r
install.packages("sparklyr")
library("sparklyr")
```

Dans un contexte avec internet, la commande correcte serait:

```r
spark_install(version = "3.3.2", hadoop_version = "2")
```

Cependant, cette tentative se soldera par un échec puisque cette commande tente de récupérer le binaire correspondant sur les serveurs Apache. Les archives nécessaires à cette installation sont tout de même disponibles dans votre espace de travail dans le dossier S:\spark. Exécutons donc la commande suivante:

```r
spark_install_tar("/chemin/vers/votre/binaire.tar")
```

Enfin, puisque nous travaillons sous environnement Windows, une installation complémentaire est nécessaire. Essayez d'abord d'exécuter la commande:

```r
sc <- spark_connect(master="local")
```

Cette commande doit échouer en indiquant une erreur de type : "Copy winutils.exe to C:\Users\projet_0_p_nom0000\AppData\Local\spark\spark-3.3.2-bin-hadoop2\tmp\hadoop\bin"

Le chemin indiqué par l'erreur est l'adresse à laquelle nous devons copier les fichiers contenus dans S:\Spark\Binaires. Une fois les fichiers copiés, exécutez de nouveau:

```r
sc <- spark_connect(master="local")
```

Vous possédez un serveur Spark adressable avec R pour votre application!

### Installer PySpark et adresser le cluster avec un notebook jupyter

## Réserver des ressources avec l'instruction la session spark

> _Comment les ressources sont elles partagées entre les utilisateurs du cluster ?_
> 
> Attention: dans un cluster spark les ressources sont partagées et vous devez en réserver une partie de façon préalable pour effectuer un traitement. C'est ce que nous avons appris à faire dans cette section. Il est fondamental de libérer les ressources après utilisation en fermant votre session spark avec l'instruction spark.close() ! Autrement, vos ressources restent allouées, même après la fin de votre traitement.
> De même, il convient d'être raisonnable en choisissant une allocation mémoire et processeur adaptée à votre traitement afin de laisser des ressources aux autres utilisateurs du cluster.

## Utiliser SparkR et PySpark pour faire des calculs