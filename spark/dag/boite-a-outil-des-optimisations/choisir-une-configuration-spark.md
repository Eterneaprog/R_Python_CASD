# 🔧 Choisir une configuration Spark

Dans certains cas, les données dépassent la taille de la mémoire allouée au traitement. S'il est possible de le faire, on peut envisager l'augmentation de la mémoire pour que l'ensemble des données soient chargées en mémoire. Sinon, cela provoque la montée et descente intempestive de données entre disque et mémoire pour que les données puissent être lues par Spark. Ce n'est pas optimal.

Si vous avez détecté une configuration insuffisante, vous pouvez apporter des modifications à la configuration de Spark pour votre programme :

* [Modifier sa configuration Spark](../../r.md#configurer-spark-en-mode-local)

Voici les paramètres qui vont particulièrement nous intéresser dans le cas d'une telle optimisation en cluster :

<table><thead><tr><th width="236.33333333333331" align="center">Paramètre</th><th width="98" align="center">Défaut</th><th align="center">Description</th></tr></thead><tbody><tr><td align="center"><strong>spark.executor.instances</strong></td><td align="center">2</td><td align="center">Le nombre d'instances de Spark utilisées</td></tr><tr><td align="center"><strong>spark.executor.cores</strong></td><td align="center">1</td><td align="center">Le nombre de cœurs par instances</td></tr><tr><td align="center"><strong>spark.executor.memory</strong></td><td align="center">1g</td><td align="center">La quantité de mémoire par instance</td></tr></tbody></table>

