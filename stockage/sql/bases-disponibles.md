# 💽 Les bases de données disponibles au CASD

## SQLite

SQLite est probablement la base la plus facile à mettre en place et utiliser au monde. Cette technologie se passe du traditionnel serveur pour ne travailler que sur un seul fichier. Cela permet une légèreté et une portabilité extrême.&#x20;

Il faut la choisir si :&#x20;

* Vous n'avez pas besoin d'accès concurrent
* Les volumétries sont raisonnables
* Vous cherchez de la portabilité
* Vous ne souhaitez pas déployer un SGBD complet

Elle peut être lue très facilement [en R](r.md#travailler-avec-sqlite) et [en Python](python.md#travailler-avec-sqlite) et créée en moins de deux minutes à l'aide de ces tutoriels.&#x20;

## MySQL

MySQL est un système de gestion de base de données mondialement connu. Depuis les années 2000, il est constamment parmi les bases les plus plébiscitées par les personnes utilisatrices de SGBD.&#x20;

Il faut la choisir si :&#x20;

* Vous possédez déjà du code SQL avec la syntaxe MySQL
* Vous cherchez de la stabilité&#x20;
* Vous appréciez la présence d'une forte communauté, avec beaucoup de support

## MariaDB

Système de gestion de base de données relationnelles open-source, MariaDB est un logiciel de référence, car il propose la compatibilité avec MySQL, est plus performant que celui-ci et gratuit.\
Initialement fondé par les créateurs de MySQL, suite au rachat de l'entreprise fondatrice par Oracle,&#x20;

Il faut la choisir si :

* Votre projet utilise du Code SQL standard
* Vous cherchez un haut niveau de performance
* Vous souhaitez une base de données relationnelles open-source et évolutive

Les différences entre MySQL et MariaDB sont très faibles pour la plupart des utilisateurs et les deux logiciels sont très compatibles. Par conséquent, le choix entre les deux s'effectue souvent sur les applications existantes et le niveau de connaissance dans l'un ou l'autre des logiciels.
