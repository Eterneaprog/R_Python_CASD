# 👩🏫 Clusters et haute performance

Si vous avez accès à un cluster dans votre projet, vous pouvez quitter le mode local et passer en mode cluster afin de disposer d'une plus grande quantité de ressources.

## Qu'est-ce qu'un cluster ?

Un cluster est un regroupement de machines de travail (les workers), sous la direction d'une machine maître (le master). Le master se charge de distribuer le travail sur les différentes machines de travail et de collecter les résultats. Cela permet de travailler de façon parallèle, et donc de gagner du temps. Spark est un logiciel avec lequel vous allez échanger pour faire fonctionner un cluster. Vous pouvez écrire vos instructions dans une syntaxe plus proche du R : c'est SparkR, ou bien avec une syntaxe proche du Python : c'est PySpark ! Il est à noter que l'on peut tout à fait utiliser Spark sans cluster, c'est le [mode local](../spark/). De même, on peut interagir avec un cluster avec d'autres logiciels que Spark. (Votre projet n'est pas nécessairement équipé d'un cluster, vous pouvez vous rapprocher de votre chef de projet pour obtenir cette information.)

Voici un aperçu simplifié du fonctionnement d'un cluster Spark :

<figure><img src="../chapters/images/spark.png" alt=""><figcaption><p>Un exemple de cluster Spark</p></figcaption></figure>

Un cluster Spark est un outil puissant qui permet d'accélérer grandement la vitesse d'exécution de vos calculs. De plus, la puissance du cluster et sa taille sont plus modulables qu'une machine seule à laquelle on ajoute des ressources : il suffit d'ajouter des workers. Cependant, l'utilisation de cet outil n'est pas toujours aussi aisée que lorsque l'on s'adresse à une machine seule. Les différents articles suivants de cette section présentent comment adapter votre code pour effectuer la migration vers un cluster de calcul.&#x20;

De plus, il est important de noter qu'un cluster ajoute une ressource supplémentaire à évaluer par rapport aux ressources traditionnellement prises en comptes pour les calculs ([CPU](../performance-calculs/ressources.md#le-processeur) et [RAM](../performance-calculs/ressources.md#la-memoire)) : le réseau. En effet, puisque les machines du parc doivent communiquer, il faut assurer que ces communications se fassent de façon rapide, car les temps de transferts d'informations sont perdus pour les calculs.

## Notion de files d'exécutions

Dans un cluster Spark, on peut définir des files d'exécutions. L'intérêt de ces files est de posséder des capacités dédiées et des usages bien précis. Ci-dessous, un exemple dans le cadre d'un cluster avec deux files pour cluster de 3 To de mémoire :

<figure><img src="../.gitbook/assets/files_exec (1).png" alt=""><figcaption></figcaption></figure>

Une partie des ressources est dédiée à la production statistique, une autre file dédie des ressources à l'utilisation interactive et aux essais sur des plus petits volumes.&#x20;

L'intérêt est de permettre le lancement de tâches et la récupération de résultats plus tard. On peut donc optimiser l'usage des ressources et les répartir dans le temps.

## Faut-il faire tourner son code sur un cluster plutôt qu'en local ?

Le coût de création du contexte Spark et la sélection des ressources à attribuer est un processus couteux en termes de temps. Ce processus peut être rentabilisé dans le cas d'un long traitement, cette étape devenant négligeable. Cependant, si le traitement est de taille raisonnable en mode local, passer en mode cluster peut représenter une perte de temps en introduisant beaucoup d'étapes intermédiaires, car la gestion ressource et le traitement sont de même ordre de grandeur.&#x20;

Il faut donc réserver l'utilisation du cluster aux traitements lourds, qui ne peuvent pas fonctionner en mode local parce qu'ils sont trop lourds (trop d'unités, traitement couteux comme une jointure, etc). C'est en particulier le cas si votre cluster est équipé d'une file dédiée à la production : elle ne doit pas faire l'objet d'une utilisation à des fins de développement ou de tests, une autre file est prévue pour cela et doit être privilégiée. De façon plus générale, il faut essayer de choisir des outils adaptés au besoin afin d'optimiser la consommation de ressources.

## Comment utiliser correctement un cluster quand un traitement justifie son utilisation ?

Passer en mode cluster n'est pas une formule magique pour gagner du temps. Avant d'effectuer un code très lourd sur un cluster, il faut vérifier plusieurs choses :

* Il fonctionne localement sur une petite quantité de donnée

Un code qui ne fonctionne pas localement n'a **aucune chance** de fonctionner avec un cluster. Cependant, l'effectuer en mode cluster complique considérablement la recherche de l'erreur. En effet, on risque de mélanger les problèmes venant du mode cluster et du code. Ce n'est pas une bonne chose. La bonne pratique est donc de systématiquement effectuer un test local pour assurer le bon fonctionnement du code, sur une base réduite. Ainsi, si un code fonctionne en local, et pas en mode cluster, on est certain que l'erreur provient du passage au cluster, et on peut orienter la recherche de bugs en conséquences (sur les ressources, le réseau, etc.)

* Il utilise des fonctions compatibles avec un traitement distribué&#x20;

Un code qui utilise des fonctions qui ne sont pas distribuées (fonctions R standards par exemple), ne bénéficiera pas d'un passage sur cluster. Il faut donc être sûr que le code est bien distribué avant de le passer sur un cluster de calcul.

* &#x20;Le code est bien optimisé

Cela permet d'assurer que l'utilisation des ressources est optimale. Il est toujours préférable d'optimiser son code pour le faire tourner en local si c'est possible, plutôt que de le faire tourner sur un cluster très puissant. Le cluster ne doit pas être une solution pour faire tourner de façon continue des codes mal optimisés qui prennent trop de temps, car leur conception est défaillante.

Les ressources d'un cluster sont partagées entre les membres d'une même bulle et sont couteuses. Il convient d'être raisonnable en communiquant ses traitements aux autres personnes utilisant le cluster, en utilisant le [spark UI](interfaces.md) pour identifier les ressources disponibles et en réservant des ressources adéquates pour son traitement. En général, les clusters font l'objet d'une organisation interne avec des files d'exécution. Il est important de respecter ces files en se renseignant auprès de la personne métier responsable du cluster.
