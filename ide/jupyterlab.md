# 🪐 Jupyter Lab

Jupyter est un outil qui permet de tester toute sorte de code. Il est particulièrement efficace dans l'exploration des données. Il est tout à fait adapté pour effectuer des calculs avec Spark, Python ou même R. Ce n'est pas tout à fait un éditeur au sens de VSCode ou RStudio, car il ne propose pas les mêmes fonctions pour le développement. Cependant, c'est un outil très performant.

## Installation de Jupyter

* Utiliser le raccourci « pip-install-packages » situé dans le dossier Raccourcis situé sur votre bureau et conserver le terminal ouvert pour la durée de l'opération
* Utiliser le raccourci « Miniconda prompt » situé dans le dossier Raccourcis situé sur votre bureau.
* Saisir la commande `conda activate nomenvironnement` pour activer l'environnement de votre choix
* Saisir la commande `pip install jupyterlab` afin d'installer le paquet Jupyter Lab
* Saisir la commande `python -m ipykernel install --user`

Votre installation de Jupyter est effectuée pour votre session. Il n'y a pas besoin d'effectuer cette installation de nouveau. Il faut juste être attentif à l'environnement conda que vous avez choisi pour effectuer cette installation.

## Lancement de jupyter

* Utiliser le raccourci « Miniconda prompt » situé dans le dossier Raccourcis situé sur votre bureau.
* Saisir `jupyter lab`
* Lorsque Windows vous demande de choisir un programme pour ouvrir la page web, choisir autre programme puis pointer sur « C:\Program Files\Chrome\chrome.exe »

<figure><img src="../chapters/images/jupyter.png" alt=""><figcaption><p>Un exemple d'utilisation de Jupyter Notebook</p></figcaption></figure>

## Utilisation de Jupyter Lab

Jupyter Lab est l'interface que vous pouvez observer ci-contre. Elle permet d'éditer et exécuter des fichiers. En particulier, les notebooks sont le format de fichier de prédilection dans un Jupyter Lab. Un Jupyter Notebook est composé de deux types d'éléments :

* les cellules de code (R, Python, PySpark ...)
* les cellules de texte (généralement, on utilise la syntaxe markdown)

L'intérêt de ce type de fichier, par rapport à un fichier python ou R standard, est de pouvoir visualiser les résultats des cellules de code au fur et à mesure qu'on les exécute. On peut donc produire des graphs, mesurer précisément quel est le temps mis pour exécuter une instruction, etc.
