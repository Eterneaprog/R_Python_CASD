# 🐍 Utiliser un ORM avec Python



## Qu'est-ce qu'un ORM ?

ORM signifie Object Relational Model. C'est le fait de mettre en commun le schéma de la base de données SQL d'une application, et le modèle de gestion de données d'une application. Concrètement, cela signifie que chaque table dans la base de données (le RM de Relational Model), correspond à une classe d'objets dans l'application (le O de object).

On va donc stocker nos objets métiers directement dans la base de données de l'application, et on pourra ainsi les récupérer plus tard.

## Pourquoi en utiliser un avec Python ?&#x20;

Utiliser un ORM facilite considérablement la gestion des données associées à une application Python. En effet, pas besoin d'écrire de longues requêtes SQL pour stocker ou récupérer des données dans la base : la librairie qui réalise l'ORM permet, lorsqu'on lui transmet un objet, de l'écrire de façon automatisée dans la base, et inversement.&#x20;

Pour la partie de la gestion des données qui concerne [les opérations CRUD](bases.md#notion-des-operations-crud) (écriture, lecture, modification et suppression),  elles sont directement implémentées pour chaque objet !

De même, lorsque l'on effectue des jointures, la librairie sait automatiquement joindre deux objets qui possèdent une clé en commun, car les clés sont définies dans le modèle de relationnel. \
\
Enfin, la création des tables et des contraintes dans la base SQL peut être effectué directement depuis le modèle relationnel ! Il n'est donc même pas nécessaire d'effectuer la mise en place de la base qui est traditionnellement couteuse.

## Comment mettre en place un ORM ?

En Python, une librairie s'est imposée pour les ORM : SQLAlchemy. Elle vient de rentrer en version 2.0 et est disponible sur les serveurs du CASD.&#x20;

Pour l'installer, vous pouvez [suivre la procédure habituelle](../../paquets/python.md), en terminant par `pip install sqlalchemy`.

La documentation officielle est disponible ici : [https://docs.sqlalchemy.org/en/20/](https://docs.sqlalchemy.org/en/20/)

Les étapes les plus importantes sont :&#x20;

* La création d'un modèle de base de données adapté
* La création d'une partie de l'application responsable d'effectuer les transactions entre la base et l'application
* La création d'un fichier d'initialisation de la base de données qui met en place dans la base les objets du modèle
