# ✨ Comprendre les notions autour des ressources

## Comprendre la gestion des ressources

> _Qu'est ce que les ressources?_

> Il s'agit de la configuration matérielle associée à votre projet. C'est-à-dire, le niveau de puissance du matériel fourni. Il doit être adapté aux traitements que vous allez effectuer. Par exemple, une régression linéaire sur 30 000 individus peut tout à fait être réalisé avec une configuration minimale. Mais ce n'est pas le cas de l'entrainement d'un modèle d'intelligence artificielle sur des centaines de milliers de lignes. Par ressources, au CASD, on entend le processeur et ses cœurs, la mémoire vive (RAM) ainsi que la mémoire sur disque (HDD/SSD).

Le processeur possède deux caractéristiques qui nous intéressent particulièrement pour le calcul :

* Sa fréquence : elle peut grossièrement être considérée comme proportionnelle au nombre d'opérations par secondes. Une fréquence plus élevée est en général synonyme de temps de traitements plus courts.
* Son nombre de cœurs : C'est le nombre de traitements que le processeur peut effectuer en même temps. Il s'agit d'un élément fondamental pour le multitâche ainsi que les calculs parallèles.

Il est très important de bien comprendre le comportement de votre logiciel et son utilisation des cœurs. En effet, si un processus est monocœur, peu importe le reste de la configuration (mémoire en particulier), une augmentation forte du nombre d'observations augmentera très fortement le temps de calcul ! Nous verrons dans la section suivante comment optimiser le code par le parallélisme.

Le deuxième élément clé qui détermine la performance d'un calcul (hormis le processeur) est la mémoire vive (aussi appelée RAM). Cette mémoire est un stockage de taille modérée, mais très performante. Elle permet de stocker des résultats de calculs intermédiaires, mais aussi certaines données utiles au calcul que le processeur réutilisera par la suite. On peut donc s'en servir pour accélérer nos calculs, car écrire chaque résultat intermédiaire sur disque est très long. C'est une opération qui est dite 'couteuse'. Écrire et lire les informations stockées dans la RAM est bien moins couteux. Cependant, la place est plus limitée.

En effet, en chargeant des données lues à de multiples reprises dans la mémoire RAM, on économise ainsi le temps de lecture sur disque. Cela peut représenter un gain de temps très important selon les applications. Cette utilisation n'est pas la même selon les logiciels. Par exemple, R utilise massivement la mémoire, ce qui peut causer des erreurs puisque celui-ci n'inclue pas de mécanisme de nettoyage nativement. À la différence de Python, qui vide automatiquement la mémoire, R impose de faire attention aux chargements que l'on effectue et de vider manuellement la mémoire. Nous verrons également ceci dans la section suivante.
