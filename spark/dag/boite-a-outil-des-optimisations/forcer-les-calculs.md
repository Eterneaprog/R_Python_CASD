# ⏳ Forcer les calculs ?

## Comportement de Spark

Nous avons vu dans [actions ou transformations ](../actions-ou-transformations.md)et dans [Catalyst](../les-plans-dexecutions-et-catalyst.md) que le phénomène de Lazy evaluation est responsable du fait que Spark exécute parfois du code plus tard que ce à quoi on pourrait s'y attendre. Gardez en tête ce principe :&#x20;

{% hint style="warning" %}
En Spark, tant qu'aucune action n'est appelée (count, show, ...), les transformations demandées sont mises en file d'attente. Quand une action est demandée, les transformations sont toutes exécutées dans le meilleur ordre afin de minimiser le temps de calcul.
{% endhint %}

Par conséquent, la question de l'exécution du code forcée, en ajoutant une instruction `.show(5)` ou `.count()`  peut se poser. En effet, avec l'une de ces instructions présente dans le code, on force Spark à exécuter l'ensemble des codes qui permettent de produire la table dont on va afficher les premières lignes ou compter le nombre de lignes. Cela va aussi provoquer le chargement des tables.&#x20;

## Interactif ou production

En mode interactif, il peut être intéressant de forcer les calculs de temps en temps, afin de voir les résultats apparaitre au fur et à mesure. Dans un notebook Jupyter, on peut utiliser `.show()` afin de vérifier que les tables ont la forme attendue. De plus, en mode interactif, la performance n'est pas l'objectif recherché. Ce mode est plutôt réservé au développement de nouveaux codes et à l'exploration de données.&#x20;

En mode production, lorsque l'on met en route un script qui a pour but de produire un résultat numérique ou une table, il est préférable de retirer les actions intermédiaires qui provoquent un déclenchement de calcul inutile. Cela permettra à Catalyst d'effectuer de fortes optimisations avant l'exécution des calculs, en trouvant un plan logique et physique optimal.

### Utilisation de `collect`&#x20;

`Collect` est une instruction présente en PySpark comme en SparkR/Sparklyr. Bien qu'elle ne soit pas exactement le même résultat dans les deux langages, le comportement de la commande est le même. Elle retourne l'ensemble des lignes du tableau Spark en un tableau R ou une liste de lignes dans le cas de PySpark. Par conséquent, il s'agit d'une action puisque l'on part d'un tableau Spark vers un autre format.

L'instruction collect sur une trop grande quantité de données provoque de grands déplacements de données. Ce n'est pas souvent efficace. Par conséquent, si on souhaite vraiment visualiser le résultat, il est préférable d'afficher les 5 premières lignes de la table, ce qui est nettement moins consommateur de ressources et de temps.

De plus, effectuer un collect pour récupérer le tableau et le persister ensuite avec les fonctions natives de R ou Python n'a pas beaucoup de sens, il est presque systématiquement préférable de persister son tableau en le stockant en Parquet ou en CSV directement depuis Spark. On chargera ensuite ce tableau en tant que dataframe R ou Python dans une autre session par la suite.&#x20;

Le cas d'usage où l'instruction collect est intéressante est celui ou les résultats d'une table produite par Spark sont de petites tailles (après un group by par exemple) et où l'on souhaite continuer à traiter ces données avec Python ou R. Cependant, même dans ce cas, il peut être préférable de marquer une séparation en stockant les données produites dans un fichier. Cela marque la fin de la préparation / prétraitement des données avec Spark, et le début de la phase d'analyse/visualisation avec Python ou R. Les deux parties du code poursuivent de très différents objectifs, on peut donc séparer les fichiers de code et passer de l'un à l'autre avec le stockage d'une table à la fin de la première phase.
