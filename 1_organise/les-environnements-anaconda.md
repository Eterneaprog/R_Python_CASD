---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 🐍 Les environnements Anaconda

> _Qu'est-ce qu'un environnement python?_
>
>
>
> C'est un espace dans lequel se trouve une version de l'interpréteur python (3.8, 3.9, ...) ainsi qu'un certain nombre de librairies Python, compatibles dans une certaine version (Numpy, Pandas, Matplotlib ...)

Conda est un outil très puissant : il permet de créer et gérer vos environnements Python pour chacune de vos applications. Ainsi, pas de mélange entre les dépendances et les versions entre vos différents projets (c’est ce que l’on appelle un conflit). Vous aurez également la possibilité d’exécuter votre code sur différentes machines avec beaucoup plus de simplicités (les environnements sont dits ‘reproductibles’). Cette section présente les rudiments de la gestion d’un environnement conda, mais vous trouverez dans les fiches suivantes les bonnes pratiques concernant les dépendances, qui apportent la véritable valeur ajoutée de l’outil conda.

## Création

D’abord nous allons créer un environnement nommé projet\_1 pour votre projet, en version 3.9 dans cet exemple. Il est recommandé de créer un environnement par projet, afin que chaque environnement soit isolé, il n’y aura ainsi pas de conflits:

Ouvrez le dossier raccourcis présents sur le bureau de votre SD-Box une fois connecté à votre session. Vous y trouverez un raccourci vers Minconda Prompt. Il s'agit tout simplement d'un terminal de commande où Anaconda est accessible:

```bash
conda create --name projet_1 python --offline
```

Cette commande utilise anaconda (conda) afin de créer un environnement (create), le nommer projet\_1 (option name) et demander l'installation de python (option python). Enfin, nous sommes dans un environnement sans internet d'où le paramètre --offline.

**Attention :** Python2 ainsi que les versions antérieures à la version 3.8 ne sont pas disponibles sur le CASD. Il est déconseillé d'utiliser ces versions même en dehors car peu de librairies modernes acceptent encore de travailler dans ces versions de Python.

Pour choisir une version de python spécifique, il suffit d'exécuter la commande présentée ci-dessus dans le terminal ouvert par miniconda dont le nom correspond. Par exemple, pour obtenir un environnement python 3.10, il suffit d'ouvrir le miniconda prompt 3.10 et d'exécuter le conda create.

## Activation

> _A quoi sert l'activation?_

> C'est le fait de préciser avec quel environnement on souhaite travailler. Cela permet de changer de l'environnement de base vers votre environnement spécifique pour le projet.

Maintenant, activons l’environnement afin de travailler dedans:

```bash
conda activate projet_1
```

**Attention :** Il faudra activer votre environnement avant l’exécution de votre code python ou d’effectuer des manipulations d’installation. Certains outils, tels que des environnements de développements, automatisent cette étape, mais ce n’est pas systématique. Les environnements de développements seront présentés dans une autre fiche.

Les autres commandes associées au système conda sont résumées sur [cette fiche](https://docs.conda.io/projects/conda/en/4.6.0/\_downloads/52a95608c49671267e40c689e0bc00ca/conda-cheatsheet.pdf).
