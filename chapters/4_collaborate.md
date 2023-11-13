# Travail collaboratif

## Se partager des fichiers

Votre session est strictement personnelle. Même les autres personnes associées à votre projet ne peuvent accéder à votre espace de travail. Le CASD vous met donc à disposition un espace commun dans lequel les fichiers sont partagés entre les différents collaborateurs de votre projet. Cet espace commun peut être accédé via le dossier raccourcis sur votre bureau.

Dans le dossier des raccourcis, vous trouverez trois dossiers:

- Espace Commun : Il s'agit du dossier partagé avec les autres collaborateurs de votre projet.
- Espace Libre Accès : L'ensemble des documents publics (documentation des données et nomenclatures)
- Espace Projet : Les imports et les sources de données de votre projet.

Vous pourrez donc échanger des fichiers via l'espace commun.

## Clavarder et éditer un document commun avec Etherpad

Afin de pouvoir échanger directement dans la bulle, un chat écrit est disponible. Pour cela, voici la démarche à suivre:

- Un collaborateur doit lancer le script clavardage dans le dossier raccourcis du bureau. Il se connecte ensuite sur 127.0.0.1:9001/ et crée un bloc note avec un nom.
- Chaque collaborateur se connecte sur 127.0.0.1:9001/p/nom_du_pad, tout le monde peut alors collaborer au document et clavarder via la colonne de droite. Cela permet d'échanger des informations de façon rapide en restant dans la bulle.

## Gérer ses versions de code avec git

Git est le système de version de code (VCS) le plus connu. Il permet d’enregistrer les modifications apportées au code d’une application, rétablir une version en cas de problème. Ce logiciel possède beaucoup d’intérêt pour le travail collaboratif. A l’aide d’un système de synchronisation, il permet d’enregistrer son code sur un dépôt local et distant.
Dans le cadre de travail individuel sur une session CASD, il présente un fort intérêt pour enregistrer les différentes versions de son code que l'on travaille seul ou même à plusieurs. Cependant, il est impossible d’utiliser les fonctions distantes du logiciel dans les bulles CASD puisque internet n’est pas disponible. Git sera incapable de contacter un serveur distant et donc, aucune synchronisation vers un dépôt GitHub ou GitLab extérieur ne sera possible. Cependant, il est tout de même possible d'effectuer du travail collaboratif avec git au CASD. Pour cela il faut utiliser un bare repository.

<img src="./images/Git.png" alt="Git" style="width:100%;height:auto;"/>

Un bare repository est un répertoire git partagé qui sert de stockage distant. On l'installe généralement dans l'espace commun de telle sorte que tout le monde puisse le cloner et travailler dessus dans son espace local. Une fois satisfait des modifications, on peut alors effectuer la commande git push afin d'envoyer sur le répertoire partagé l'ensemble des modifications qui ont été enregistrer dans git. Les autres collaborateurs peuvent alors en disposer avec un git pull. Sur le schéma, vous avez sur la gauche le fonctionnement traditionnel d'une architecture git avec un dépôt distant hébergé sur Gitlab/Github. Sur la droite, le fonctionnement en mode multi-utilisateurs est expliqué dans une bulle projet. Pour mettre en place un tel système, la procédure et ses commandes sont expliquées dans la section suivante

**Conseil:** Réalisez des ajouts à la base de code (commande `git add .` et `git commit -m "nom du commit"`) aussi fréquemment que possible, avec des noms parlants. En cas d'apparition d'erreur, cela permettra de rechercher quelle est la modification qui a introduit l'erreur, au lieu de perdre l'ensemble des modifications apportées lors d'une nouvelle version. Une bonne pratique est: une modification pour ajouter une fonction ou corriger une erreur = un commit dans git.

Une fiche récapitulative avec les principales fonctions du logiciel est disponible [ici](https://education.github.com/git-cheat-sheet-education.pdf)

## Mettre en place un bare repository Git

D’abord le premier utilisateur va créer un répertoire bare dans l'espace commun. Pour effectuer cette manœuvre, rendez-vous avec votre explorateur de fichier dans C:\Utilisateurs\Public\Documents. Créez alors un dossier pour le projet. Toujours dans l'explorateur, rentrez dans le dossier et faites: clic droit, Git Bash here. Un terminal de commande devrait alors s'ouvrir, vous pouvez y saisir la commande suivante:

```bash
git init --bare
```

Le terminal devrait répondre: `Initialized empty git repository in C:/Users/Public/Documents/nom_de_votre_dossier/`. Cette adresse est maintenant celle du répertoire bare et vous pouvez fermer ce terminal. Le dépôt est créé pour l'ensemble des utilisateurs du projet. Personne ne peut l'éditer directement: pour y apporter des modifications, il faut le cloner et utiliser les commandes git add . / git commit / git push. Pour cloner le dépôt, rendez-vous à la section suivante.

## Cloner un dépôt déjà existant

Rendez-vous maintenant avec votre explorateur de fichiers dans votre espace personnel, à l'endroit où vous souhaitez cloner ce dépôt. Effectuez: clic droit, Git Bash Here. Dans le terminal, saissisez:

```bash
git clone C:/Users/Public/Documents/nom_du_dossier_à_cloner/
```

Vous pouvez maintenant éditer votre dépôt, et envoyer vos modifications comme vous le feriez hors de la bulle !