# 📊 Gérer les ressources avec R

### Vider la mémoire avec R

R effectue une utilisation intensive des ressources mémoires. En particulier, toute instruction de type

```r
read.csv()
```

charge les données du fichier dans la mémoire. Faire plusieurs chargements identiques ou avoir plusieurs tables intermédiaires chargées dans la mémoire de R peut amener à une saturation. Par conséquent, nous devons vider cette mémoire des objets inutiles. Dans Rstudio, l'onglet qui permet de voir ce qui est chargé dans la mémoire se situe en haut à droite, dans la fenêtre "Environnement". On y retrouve tous les objets chargés dans la mémoire, et qui sont accessibles par un appel dans la console par exemple.

On peut vider un objet spécifiquement avec la commande :

```r
rm(nom_objet)
```

Aussi, il est possible de vider l'ensemble des éléments avec la commande :

```r
rm(list=ls())
```

C'est ce qu'il est recommandé de faire lorsque vous souhaitez recommencer l'exécution d'un programme à 0.&#x20;

### Chargement de la session précédente au démarrage de Rstudio

RStudio charge la dernière session via le fichier Rdata si une telle instruction est donnée dans les paramètres. Cette instruction se situe dans :

Outils -> Options globales -> Restaurer .Rdata dans l'espace de travail au démarrage

Cela signifie que la fermeture de R avec Rstudio paramétré de façon incorrecte peut amener au chargement de données au démarrage qui ne sont pas prévues. Il n'est donc également pas recommandé de sortir un fichier Rdata puisqu'il peut contenir des données intermédiaires. Il est recommandé de désactiver cette option.
