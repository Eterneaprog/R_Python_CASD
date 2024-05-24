# 👩‍🏫 Optimiser Spark

Avant de s'intéresser aux optimisations, il est très important de bien maitriser les notions de transformations et d'actions en Spark. Elles ont des implications fortes sur le code et son exécution à cause du phénomène "Lazy evaluation". Un rappel sur ces notions est disponible ici :&#x20;

[Rappel sur la différence entre actions et transformations](actions-ou-transformations.md#difference-entre-les-deux-notions)

De plus, les transformations sont réparties en deux types, celles qui mobilisent un sous-ensemble des données (narrrow), ou celles qui ont besoin de l'ensemble des données (wide). Il est important de pouvoir identifier de quel type est une transformation avant de l'ajouter à son code. Un rappel sur la différence entre ces deux types de transformations, ainsi que des exemples sont disponibles ici :&#x20;

[Rappel sur les types de transformations Spark](actions-ou-transformations.md#transformations-narrow-contre-wide)

Spark embarque un module chargé d'optimiser votre code et qui rend ce langage très performant : Catalyst. Comprendre le fonctionnement de Catalyst et des plans d'exécutions aide grandement à comprendre pourquoi les optimisations que nous allons appliquer par la suite sont, ou ne sont pas efficaces. Cependant, il est possible d'appliquer les bonnes pratiques sans saisir les détails de ces notions.&#x20;

[Le fonctionnement de Catalyst et des DAG en Spark](les-plans-dexecutions-et-catalyst.md)

On peut appliquer une méthode afin d'optimiser son code et tester que ces optimisations sont efficaces :&#x20;

[Une méthodologie de l'optimisation](une-methode-pour-tester-son-optimisation.md)

Dans cette méthodologie, vous verrez comment détecter ce qui rend le code lent, quelles sont les optimisations disponibles, et comment les appliquer. Entre autres : la configuration adaptée, le partitionnement, le cache.
