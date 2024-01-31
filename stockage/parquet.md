# 🗄 Utiliser Parquet

## Qu'est-ce que le parquet ?

Le parquet est un format de stockage de données en colonnes, optimisé pour la lecture. Il utilise par défaut une compression snappy, qui tient compte du contenu afin de maximiser le gain de place. Cette compression est cependant transparente à l'utilisation.

### Les avantages de ce format par rapport aux autres (CSV / SAS7BDAT / Excel)

* Un taux de compression très élevé, qui peut diminuer par 10 la taille par rapport à un autre format n'utilisant pas de compression.
* Une vitesse de lecture accrue qui peut accélérer vos traitements par 3 s'ils utilisent massivement la lecture
* Un format neutre et agnostique des logiciels

### Les défauts de ce format

* Il ne permet pas d'éditer le contenu du fichier, une modification passe par la régénération du fichier
* Il n'est pas lisible aussi facilement qu'un fichier CSV non compressé

## Quand faut-il utiliser le parquet ?

Parquet est très efficace pour effectuer de l'analyse. Cependant, il est inefficace pour les opérations transactionnelles.&#x20;

Par exemple, l'entrainement d'un modèle ou la réalisation d'une régression sur des grands nombres d'individus sont des cas d'usages très adaptés pour Parquet. À l'inverse, Parquet est inefficace s'il doit être utilisé comme une base de données dans laquelle on doit écrire des données de manière fréquente. Le critère déterminant est : combien d'opérations d'écritures et de lecture mon application va-t-elle utiliser ?\
Si la réponse est plusieurs opérations de lecture, écriture, modification, il faut se tourner vers [une base de données SQL](sql/). Si la réponse est une seule opération d'écriture que l'on va utiliser pour lire à de nombreuses reprises, alors Parquet est très adapté. Ce sera typiquement le cas si on fige la base de données d'une application pour y faire de l'analyse statistique.

## Les outils avec lesquels utiliser Parquet

Il existe des outils pour chaque cas d'usage :&#x20;

* Pour lire du parquet et l'afficher, vous pouvez utiliser [TADviewer](https://www.tadviewer.com/) ou [ParquetViewer](https://github.com/mukunku/ParquetViewer)
* Pour l'interroger et l'utiliser comme une base de données en lecture : [DuckDB](duckdb/) est un très bon candidat (très efficace avec R et Python).
* Pour le créer et interagir avec de façon directe : [Arrow ](https://arrow.apache.org/docs/python/parquet.html)est une librairie efficace qui permet presque de tout faire avec parquet en Python ou R.

## Partitionnement ou non ?

Un fichier parquet peut être partitionné. Cela se reconnait au fait que le fichier parquet est dans ce cas un dossier qui contient plusieurs fichiers parquets de petite taille. Cela signifie qu'il est découpé afin de pouvoir le requêter de manière plus efficace.

On peut le partitionner par colonne par exemple : si je possède un fichier contenant des véhicules, je peux le partitionner par marque. Ainsi, si je ne travaille que sur les véhicules d'une certaine marque, je n'utiliserai que ce fichier parquet et le traitement sera donc très rapide.

Le partitionnement peut donc être une solution intelligente s'il est effectué de sorte à avoir du sens par rapport aux futurs traitements métiers. L'objectif est partitionnant les données est de les regrouper de telle sorte que les traitements soient appliqués sur un minimum de fichier, et ainsi gagner du temps de traitement.&#x20;
