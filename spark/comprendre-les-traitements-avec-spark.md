# 👩🏫 Comprendre les traitements avec Spark

## Mode local contre mode distribué

Spark est un logiciel capable d'effectuer des tâches de façon parallèles. C'est-à-dire : effectuer plusieurs morceaux de calculs en même temps, puis rassembler les résultats obtenus en un seul morceau. \
Par exemple : si on souhaite appliquer un traitement à chaque ligne d'une table contenant un grand nombre d'observations : il est intéressant d'utiliser cette technique, car on va diviser le temps total de l'opération par le nombre de tâches que l'on peut effectuer de manière parallèle.&#x20;

Le mode local est le fait d'utiliser Spark sur sa propre machine. Il n'y a donc qu'une machine (virtuelle ici) qui travaille, c'est votre bulle. Spark utilise les capacités de cette machine pour lui faire effectuer des tâches de manière parallèle. Ce mode permet d'effectuer des gains algorithmiques. En effet, si la machine possède plusieurs cœurs, on peut effectuer plusieurs tâches à la fois plutôt que de les faire les unes à la suite des autres.

Le mode cluster est le fait d'utiliser un parc de machines distantes sur lequel Spark est installé. On se connecte alors au nœud principal (c'est le master), et on donne des instructions à ce master qui fait travailler des workers. En pratique, cela veut dire faire exécuter les différents morceaux du traitement sur plusieurs machines distinctes, plutôt que sur la même. Cela possède l'intérêt de cumuler les puissances de calculs de plusieurs machines. Cependant, cela génère aussi un trafic réseau important, car il faut faire communiquer les machines. Cette organisation des machines est nommée cluster. La maintenir et la déployer est à la charge de votre fournisseur d'accès en général (le CASD propose ce service). Cependant, [la comprendre permet de l'utiliser de façon optimisée](../gestion-des-clusters/).

## Les ressources avec Spark

Spark utilise massivement [la mémoire ](../5\_performance/notions-autour-des-ressources.md#la-memoire)afin d'accélérer de façon drastique vos calculs. Il s'agit du gain principal de cette technologie par rapport aux plus anciennes comme Hadoop. En effet, en chargeant les données dans la mémoire, cela permet de les lire plusieurs fois de manière quasi instantanée. Cependant, il faut être attentif à la consommation mémoire et ne pas charger à plusieurs reprises les mêmes données. Il s'agit du même problème qu'en R. Cela peut créer des saturations mémoires et consommer énormément de places pour des résultats peu probants.

Pour cette raison, il est très important de bien déterminer les ressources que vous souhaitez allouer à votre session. Une fois allouée, et tant que cette session ne sera pas achevée, elles seront réservées. Indépendamment du mode choisi, une bonne gestion ressources est essentielle pour le travail collaboratif.
