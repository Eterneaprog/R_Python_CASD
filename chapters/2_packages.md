1. [Organiser votre projet](1_organise.md)
2. **Gérer les paquets associés au projet**
3. [Coder votre application avec R ou Python](3_code.md)
4. [Effectuer du travail collaboratif](4_collaborate.md)
5. [Optimiser les performances](5_performance.md)

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

En python, le gestionnaire de paquets à utiliser au CASD est pip car c’est un serveur PYPI qui est synchronisé. Le script install-package présent sur votre bureau doit être utilisé afin d'assurer que l'accès au serveur contenant les paquets est initialisé. L’environnement conda de votre choix doit être activé, et enfin, il faut utiliser la commande suivante dans le fenêtre conda ouverte par le script:

```bash
pip install package_name
```

Puis dans votre code python, utilisez cette instruction pour importer votre paquet, comme vous le feriez en dehors de l'espace de travail sécurisé:

```python
import package_name
```

Il est très fortement recommandé d’utiliser un fichier requirements.txt, et y consigner les paquets les uns sous les autres. La commande d’installation qui permet d’obtenir l’ensemble des paquets depuis le dépôt est alors:

```bash
pip install –r requirements.txt
```

**Attention:** Notez l'utilisation de l'argument -r qui précise que l'on doit installer les paquets depuis un fichier. Oublier le -r impliquera que pip essaiera d'installer un paquet nommé littéralement requirements.txt, et échouera donc.

Avec ce fichier, vous pourrez ainsi exécuter votre code sur une autre machine en créant un environnement python vierge, l’activant, et en exécutant la commande ci-dessus dans le terminal.

## Installer un paquet R

Les commandes R qui permet d’installer un paquet et de l’importer est strictement identique à celle dans votre environnement de travail habituel. Assurez-vous simplement de demander l’installation d’un paquet présent dans nos dépôts, autrement, une erreur s’affichera. Pour installer le paquet, exécutez simplement dans la console R:

```r
install.packages("package_name")
```

Puis dans votre code:

```r
library("package_name")
```

## Installer le package sparklyr pour travailler avec SparkR

Si vous souhaitez utiliser sparkR afin d'accélérer votre application, voici la marche à suivre.

Procédez d'abord à l'installation du package sparklyr à l'aide du dépôt, comme dans la section précédente, puis chargez le:

```r
install.packages("sparklyr")
library("sparklyr")
```

Dans un contexte avec internet, la commande correcte serait:

```r
spark_install(version = "3.3.2", hadoop_version = "2")
```

Cependant, cette tentative se soldera par un échec puisque cette commande tente de récupérer le binaire correspondant sur les serveurs Apache. Cependant, les archives nécessaires à cette installation sont disponibles dans votre espace de travail dans le dossier S:\spark. Exécutons donc la commande suivante:

```r
spark_install_tar("/chemin/vers/votre/binaire.tar")
```

Enfin, puisque nous travaillons sous environnement Windows, une installation complémentaire est nécessaire. Essayez d'abord d'exécuter la commande:

```r
sc <- spark_connect(master="local")
```

Cette commande doit échouer en indiquant une erreur de type : "Copy winutils.exe to C:\Users\projet_0_p_nom0000\AppData\Local\spark\spark-3.3.2-bin-hadoop2\tmp\hadoop\bin"

Le chemin indiqué par l'erreur est l'adresse à laquelle nous devons copier les fichiers contenus dans S:\Spark\Binaires. Une fois les fichiers copiés, exécutez de nouveau:

```r
sc <- spark_connect(master="local")
```

Vous possédez un serveur Spark adressable avec R pour votre application!

[Chapitre III: Coder une application basique](3_code.md)
