# 🐍 Installer les paquets python

## Installer un paquet python

En python, le gestionnaire de paquets à utiliser au CASD est pip, car c’est un [serveur PYPI ](comprendre.md#comment-cet-ecosysteme-peut-fonctionner-sans-internet)qui est synchronisé.

{% hint style="warning" %}
Le serveur de paquets CASD ne contient pas l'ensemble des paquets disponibles sur PYPI pour des raisons de sécurité, si l'installation échoue, vous pouvez nous contacter par mail en précisant le paquet souhaité. Nous évaluerons alors s'il est élligible à entrer au dépot de paquets.
{% endhint %}

L’environnement conda de votre choix doit être créé et activé ([voir article dédié](conda-env.md)). Il vous faudra ouvrir un Miniconda prompt depuis l'espace raccourci :&#x20;

* Dans l'anaconda prompt ouvert, saisissez :

```bash
conda activate nom_de_votre_environnement
```

{% hint style="info" %}
Si vous avez oublié les environnements créés sur votre espace, utilisez `conda env list` pour les afficher.
{% endhint %}

Puis :

```bash
pip install nom_du_package_souhaité
```

<figure><img src="../.gitbook/assets/Install-package2.PNG" alt=""><figcaption><p>Ici, on observe que pip contacte le serveur local afin de procéder à l'installation de Pandas et de ses dépendances !</p></figcaption></figure>

Dans votre code python, utilisez cette instruction pour importer votre paquet, comme vous le feriez en dehors de l'espace de travail sécurisé :

```python
import package_name
```

Il est très fortement recommandé d’utiliser un fichier requirements.txt, et y consigner les paquets que vous utilisez les uns sous les autres. La commande d’installation qui permet d’obtenir l’ensemble des paquets depuis le dépôt est alors :

```bash
pip install –r requirements.txt
```

{% hint style="danger" %}
Notez l'utilisation de l'argument -r qui précise que l'on doit installer les paquets depuis un fichier. Oublier le -r impliquera que pip essaiera d'installer un paquet nommé littéralement requirements.txt, et échouera donc.
{% endhint %}

Avec ce fichier, vous pourrez ainsi exécuter votre code sur une autre machine en créant un environnement python vierge, l’activant, et en exécutant la commande ci-dessus dans le terminal. Votre environnement sera reproductible, pas vous, ainsi que d'autres collaborateurs de votre projet (voir [Travail collaboratif](../collaborer/)).
