# Gérer les paquets associés à votre projet

> _Paquet / librairie / dépendance / module?_
> Si ces mots ne sont pas exactement équivalents, en python ou en R, ils signifient presque toujours avoir recours à une ou plusieurs fonctionnalités additionnelles du langage par l'import dans le code. Cela permet parfois de ne pas recoder soi-même ce qui existe déjà. Certaines librairies sont directement amenées avec python (sys ou os) ou R (stats), d'autres doivent être installées manuellement (pandas, tensorflow pour Python, deeplyr pour R).

Le CASD propose des environnements de travail sans internet pour des raisons de sécurité. Par conséquent, impossible de consulter une documentation Python ou R. Votre ordinateur personnel ou votre téléphone peut tout à fait vous aider dans ce cas. Il vous suffit de retranscrire la commande ou ligne de code obtenue en réponse à votre question.
Cependant, pour les paquets, ce n’est pas possible d’effectuer une telle manœuvre. Les serveurs auxquels vous avez l’habitude de vous connecter pour récupérer les paquets (PYPI ou le CRAN par exemple) ne sont pas joignables sans internet.
À gauche, dans le fonctionnement dans votre système personnel, votre ordinateur utilise sa connexion internet pour atteindre les serveurs PYPI ou CRAN et récupérer les paquets voulus.

<img src="/assets/images/serveurs.png" alt="serveurs" style="width:500px;"/>

Afin de vous permettre d’installer vous-même les packages, sans envoi de mail, le CASD vous met à disposition des serveurs internes pour Python et R (à droite sur le schéma). Ces serveurs ne contiennent pas l’ensemble des paquets disponibles sur les serveurs publics afin d’assurer la sécurité des environnements de travail. Ils sont synchronisés par nos équipes de façon manuelles. Ils contiennent les paquets les plus communs avec lesquels les utilisateurs travaillent. La liste est disponible ici.

Si vous souhaitez installer un paquet non présent dans nos dépôts, vous êtes invités à envoyer un email à [service@casd.eu](mailto:service@casd.eu) contenant les informations sur le package ainsi que le lien où le trouver. Nos équipes importeront alors le paquet et vous donneront les instructions nécessaires pour procéder à l’installation.

## Installer un paquet python

En python, le gestionnaire de paquets à utiliser au CASD est pip car c’est un serveur PYPI qui est synchronisé. Le CASD vous met a disposition un script qui permet d'assurer le lancement du serveur contenant les paquets :

- **Lancez le script pip-install-package depuis votre dossier raccourcis situé sur votre bureau**. Ne fermez pas la fenêtre obtenue tant que vos packages ne sont pas installés.

L’environnement conda de votre choix doit être créé et activé (voir chapitre 1). Il vous faudra ouvrir un Miniconda prompt depuis l'espace raccourci et utiliser la commande : 

- Dans l'anaconda prompt ouvert, saisissez:

```bash
conda activate nom_de_votre_environnement
```

puis :

```bash
pip install nom_du_package_souhaité
```

Dans votre code python, utilisez cette instruction pour importer votre paquet, comme vous le feriez en dehors de l'espace de travail sécurisé:

```python
import package_name
```

Il est très fortement recommandé d’utiliser un fichier requirements.txt, et y consigner les paquets que vous utilisez les uns sous les autres. La commande d’installation qui permet d’obtenir l’ensemble des paquets depuis le dépôt est alors:

```bash
pip install –r requirements.txt
```

**Attention:** Notez l'utilisation de l'argument -r qui précise que l'on doit installer les paquets depuis un fichier. Oublier le -r impliquera que pip essaiera d'installer un paquet nommé littéralement requirements.txt, et échouera donc.

Avec ce fichier, vous pourrez ainsi exécuter votre code sur une autre machine en créant un environnement python vierge, l’activant, et en exécutant la commande ci-dessus dans le terminal. Votre environnement sera reproductible, pas vous, ainsi que d'autre collaborateurs de votre projet (voir chapitre 4 : Travail collaboratif).

## Installer un paquet R

Les commandes R qui permet d’installer un paquet et de l’importer est strictement identique à celle dans votre environnement de travail habituel. Assurez-vous simplement de demander l’installation d’un paquet présent dans nos dépôts, autrement, une erreur s’affichera. Pour installer le paquet, exécutez simplement dans la console R:

```r
install.packages("package_name")
```

Puis dans votre code:

```r
library("package_name")
```
