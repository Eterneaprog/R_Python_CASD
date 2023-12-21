# 👩🏫 Bonnes pratiques de code Python

Le premier objectif lorsqu'on produit un code informatique est qu'il fonctionne, et réponde à notre besoin. Cependant, on peut atteindre cet objectif avec un code dit de 'bonne qualité' ou non. \
\
Nous allons apprendre dans cette section des premières notions sur la qualité du code, et quels sont les avantages très concrets d'appliquer ces principes. Ensuite, nous verrons comment appliquer ces principes à notre code Python.

## Une notion de qualité du code

La qualité de code est évaluée sur plusieurs critères, voici une liste non exhaustive :&#x20;

* Le code réalise bien le besoin demandé
* Le code est facile à comprendre et à lire
* Le code est documenté de façon régulière
* Le style est cohérent au travers de l'ensemble du programme
* Le code est testable et testé

Nous allons revenir sur chacune de ces notions en détail avec la pratique Python correspondante. Avant cela, puisque développer un code de bonne qualité coute plus cher de façon immédiate qu'un code de mauvaise qualité, voyons quels sont les objectifs :&#x20;

* Avoir un code qui produit des résultats fiables et dont on peut prouver l'origine
* Avoir un code fiable qui s'exécute de façon sereine
* Pouvoir faire évoluer le code façon simple
* Faciliter l'utilisation de notre code par les utilisateurs
* Pouvoir maintenir facilement notre code dans le temps

Avoir un code de bonne qualité coute un tout petit peu plus cher à produire, mais c'est un investissement rentable sur la durée ! Un code qui ne coute presque rien en maintenance, et dont on est sûr qu'il va fonctionner et produire le bon résultat.

Voyons maintenant les techniques pratiques pour produire un code de bonne qualité à moindres frais. En effet, il existe beaucoup d'outils qui peuvent vous aider à changer peu de choses dans votre façon de coder, tout en assurant les propriétés que nous avons citées précédemment.                            &#x20;

## En pratique (avec Python)

### Comment cibler le besoin ?

Pour répondre à cet objectif, il n'y a un qu'un seul leitmotiv : "Réfléchir avant d'agir". Différentes questions peuvent aider à bien cibler le besoin réel :&#x20;

* Quels sont les éléments qui relèvent de l'essentiel et du superflu ? (Savoir prioriser les besoins)
* Suis-je en train de produire un code que d'autres ont déjà fait 10 fois avant moi, en mieux, ou suis-je en train de traiter un besoin très spécifique ?&#x20;
  * **Exemple :** Recoder un système de date en Python, alors que Datetime ou Pendulum sont des librairies totalement fonctionnelles pour cela, n'est pas très pertinent et ne sert probablement pas mon objectif métier de façon directe
* Mes choix technologiques sont-ils bien adaptés à mon objectif ?&#x20;
  * **Exemple :** Utiliser un logiciel de production statistique (SAS / SQL / STATA / SPSS / R) alors que mon objectif est le data management. Ne faut-il pas utiliser une simple base SQL qui est prévue pour cet usage plutôt qu'un outil qui a pour fonction primaire de faire des analyses statistiques sur une base construite.

Une fois que les choix technologiques ont été définis par rapport à notre objectif, on peut concevoir notre code. Il faut alors définir quelles sont les fonctions que l'on veut coder. On cherche dans cette étape à décomposer notre tâche générale en tâches de plus petites tailles qui vont s'enchainer de façon logique et cohérente.&#x20;

### La documentation et la compréhension

#### La documentation

Lorsque vous produisez le code, il est important de le documenter afin de répondre au troisième objectif. Il est important de comprendre pourquoi et pour qui on documente, car ce n'est pas une fin en soi. Documenter une fonction, c'est décrire le 'Quoi'. Cela sert avant tout aux utilisateurs de votre code ainsi qu'aux développeurs. Le but n'est pas de décrire comment est construite la fonction, mais ce qu'elle fait (Quels sont ses paramètres ? Que produit-elle comme résultat ?), afin d'assurer une utilisation simple.&#x20;

La documentation, c'est le manuel d'utilisation de la fonction. Prenons une métaphore : le manuel et l'aide de votre téléphone mobile vous expliquent comment le démarrer, le charger, l'utiliser pour envoyer des messages, etc. Cependant, elles ne vous décrivent pas comment le fabricant construit un écran, assemble la batterie et quelle couche logicielle est utilisée pour envoyer un message. La documentation de votre code doit suivre la même logique. Elle n'est pas là pour expliquer comment la fonction est codée, mais ce qu'elle fait et comment on peut s'en servir.&#x20;

En python, il existe différente façon de faire une documentation. On documente les fonctions sous leur nom, de la façon suivante :&#x20;

```python
def ma_fonction(parametre1 : int):
    """
    Un descriptif concis de ce que fait la fonction
    
    :param parametre1: Un entier quelconque
    :type parametre1: int
    
    :return: L'entier saisi en paramètre avec une unité supplémentaire
    :rtype: int
    """
    return parametre1 + 1
```

La façon de faire l'intérieur de la documentation est libre, il existe plusieurs standards :&#x20;

* Le style Google
* Le style reStructuredText
* Le style Numpy/SciPy
* Le style Epytext

L'exemple que j'ai fourni ci-dessus est dans le style reStructured, mais j'utilise personnellement le style Google, qui est le plus parlant pour moi. Le plus important est la consistance de la documentation dans le code.

Pour aller plus loin sur ce sujet, [l'article de realPython](https://realpython.com/documenting-python-code/#docstring-formats) sur le sujet est très complet et présente les 4 styles possibles.

#### Les commentaires et la lisibilité

La documentation ne doit pas être confondue avec les commentaires et la lisibilité. La capacité d'un autre développeur à comprendre votre code est aussi importante, mais ce n'est pas le rôle de la documentation : c'est le rôle du code et de ses commentaires. C'est pour cela qu'on décrit également le 'Comment' dans les commentaires si c'est nécessaire. C'est ce qui permet à un autre développeur de modifier votre code et d'assurer sa maintenabilité, y compris par vous-même d'ailleurs. Cela peut être fait à l'aide des commentaires dans le code. Cela doit s'accompagner de façon impérative d'un code lisible (nom de variables parlants, conditions claires). Il faut trouver le compromis entre trop de commentaires, et un code sans commentaire qui est illisible.

En règle générale, si le traitement que vous êtes en train d'effectuer est logique et simple, il se passe de commentaires, car en lisant les variables, on peut comprendre aisément ce qui est fait. Il faut commenter les passages les plus techniques. Si vous ressentez le besoin de commenter le code systématiquement parce qu'il n'est pas assez limpide, le problème vient d'abord du code et il faut envisager de le modifier en premier. Si aucune solution ne peut être trouvée pour le simplifier et rendre le code lisible, il faut effectivement utiliser les commentaires de manière plus détaillée.

Pour commenter en Python, on utilise le symbole #&#x20;

```python
# On ajoute trois au nombre de bananes
x + 3
```

Lorsqu'il est nécessaire de commenter, je trouve plus clair d'utiliser un commentaire sur toute une ligne au-dessus de la ligne de code que de commenter en bout de ligne. Mais c'est un choix personnel. Pour un court commentaire, cela peut suffire

```python
x + 3 # On ajoute trois au nombre de bananes
```

Cependant, la meilleure solution serait bien sûr :&#x20;

```
nb_bananes + 3
```

### Le style

Tant que possible, il faut essayer d'appliquer les principes recommandés par le standard [PEP8](https://peps.python.org/pep-0008/) (Python Enhancement Proposals) qui définit le style de code applicable au code Python. Cela permet un code plus lisible.

Cependant, appliquer la PEP8 à son code de façon manuelle est très long et fastidieux. Il existe donc des extensions qui permettent de formater le code de manière automatisée. En particulier avec Visual Studio Code comme nous l'avons [vu précédemment.](../3\_code/vscode.md)

S'il fallait résumer rapidement la PEP8 :&#x20;

* Utiliser des docstrings
* Utiliser 4 espaces et pas de tabulations
* Les noms de variables sont Snakecase : `ma_variable = 0`
* Les classes sont en CamelCase : `MaClasse`
* Limiter la taille des lignes (79 caractères maximum)
* Mettre des espaces avant et après les opérateurs : `a == b` et non `a==b`

À mon sens, la PEP8 n'est à suivre strictement, mais doit être vue comme un guide de bonnes pratiques. Le plus important est de loin la cohérence du code. Il resterait préférable d'avoir un code consistant qui utilise le mixedCase : `maClasse` pour les classes qu'un code qui utiliserait un mélange de Snakecase et de CamelCase par exemple.

### Les tests

Les tests sont le fait d'exécuter une fonction afin de vérifier qu'elle répond bien à son cas d'usage. Cela permet de corriger les bugs et de les détecter lorsqu'on effectue des modifications. Une fonction utilisant une sous fonction, si on modifie la sous-fonction, on peut casser une partie du programme que l'on n'avait pas prévue. Le seul moyen de le détecter est de tester de façon systématique les fonctions réalisées.&#x20;

Cependant, il n'est nul besoin de tester manuellement le programme à chaque modification. La force des éditeurs de code nous permet d'écrire un test une fois, et de le faire exécuter de manière systématique. On va donc construire une base de tests lorsqu'on conçoit le programme, et elle restera valable de façon permanente. De nouveau, il s'agit d'un investissement un peu couteux, mais qui est extrêmement rentable par la suite.

En Python, il existe globalement deux paradigmes de tests :&#x20;

* Pytest
* Unittest

Unittest est la librairie officielle de test de Python. Cependant, elle est de plus en plus délaissée au profit de Pytest (pour des raisons de simplicité, de fonctionnalité offertes ...). La dynamique est historique va vers l'utilisation de Pytest, car la communauté y est plus active et que la syntaxe et la compréhension est plus simple.

C'est personnellement le framework que j'utilise pour développer mes programmes, mais unittest reste fonctionnel. C'est essentiellement un choix qui revient au développeur.

Les tests suivent généralement la conception suivante :&#x20;

1. **Mise en place** des conditions du test (création des objets)
2. **Action** en appelant la fonction
3. **Vérification** que la condition est vérifiée

L'article de [RealPython au sujet des tests](https://realpython.com/pytest-python-testing/) est très complet et présente la syntaxe pour rédiger les tests. &#x20;
