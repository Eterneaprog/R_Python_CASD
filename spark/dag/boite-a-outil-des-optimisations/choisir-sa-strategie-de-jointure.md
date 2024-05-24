# ⏱️ Choisir sa stratégie de jointure

Selon la taille des tables à joindre par rapport à la mémoire, on peut indiquer à Spark une certaine technique de jointure plus ou moins adaptée :&#x20;

1 - Broadcast Hash Join  : si une des tables est petite et l'autre grande, c'est un bon choix. Attention : elle ne supporte que le critère d'égalité pour la jointure.

2 - Sort Merge Join : cette stratégie est efficace en toute circonstances de taille : elle est prévue pour déborder sur le disque car elle n'utilise pas de table de hashache. \
Attention : elle ne supporte que le critère d'égalité pour la jointure.

3 - Shuffle Hash Join : si les deux tables sont grandes, cette stratégie est envisageable car elle mélange le hashage et le shuffling. \
Attention : elle ne supporte que le critère d'égalité pour la jointure et peut ne pas fonctionner si la taille dépasse la mémoire allouée au traitement.

4 - Broadcast Nested Loop Join : cette stratégie est intéressante car elle offre la possibilité de joindre avec un critère < ou >. Ce n'est pas possible avec les algorithmes précédents. \
Attention : Il s'agit de la stratégie la moins rapide, même dans un cas d'égalité. Elle fait une comparaison totale dans tous les cas afin de supporter des critères de jointures particuliers.

5 - Cartesian Product Join : Il s'agit de la jointure naïve. Elle est presque systématiquement à éviter. Elle résulte souvent dans des erreurs mémoires, même avec des tables de taille moyenne. &#x20;

Spark choisit lui-même une stratégie 'adaptée' en fonction de paramètres par défauts, mais on peut forcer la stratégie pour gagner du temps si celle choisie ne nous correspond pas à ce que l'on souhaite faire.

La documentation officielle mentionnant les [stratégies de jointure](https://spark.apache.org/docs/latest/sql-performance-tuning.html#join-strategy-hints-for-sql-queries).
