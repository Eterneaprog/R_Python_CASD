# 🐍 Un exemple d'application Python

En règle générale, on cherche à maintenir le fichier principal d'une application python aussi succinct que possible. Un exemple de code permettant de renvoyer la tranche d'âge associée à un utilisateur pourrait être :

**functions:**

```python
def convert(age):
    """
    This function takes the age of a person and returns the age category it belongs to
    :param age: The age of the person
    :type age: int
    :return: la categorie d'age de la personne
    :rtype: str
    """
    if age < 18 :
        categorie = '[0-18]'
    elif age < 30 :
        categorie = '[18-35]'
    elif age < 50 :
        categorie = '[36-50]'
    else :
        categorie = '[51-110]'
    return categorie
```

**main :**

```python
# Imports
import os
import sys
from app.functions import convert

# Fonction principale
def main():
    print("Bienvenue !")

    age_utilisateur = input("Entrez votre age : ")
    categorie = convert(age_utilisateur)

    print(f"Votre catégorie d'age est {categorie} !")

# Execution du code
if __name__ == "__main__":
    main()
```

Dans cet exemple, j'ai mis les imports en en-têtes de fichiers, puis, j'ai défini la fonction principale de mon programme, qui exécute du code métier contenu dans un autre fichier, dans une fonction. Enfin, j'exécute ma fonction principale à l'aide de l'instruction `if __name__ = "__main__".`

**Conseil :** Tant que possible, il faut essayer d'appliquer les principes recommandés par le standard [PEP8](https://peps.python.org/pep-0008/) (Python Enhancement Proposals) qui définit le style de code applicable au code Python. Cela permet un code plus lisible et de meilleure qualité.

> _Docstring / Commentaires ?_
>
> Lorsque vous produisez le code, il est important de le documenter. Cependant, il n'existe pas une seule manière de faire cette documentation. Le docstring est la norme python pour documenter ce que fait une fonction (c'est le Quoi). Cela sert avant tout aux utilisateurs de votre code ainsi qu'aux développeurs. On retrouve cette documentation sous la fonction.
>
> Cependant, il est aussi important de documenter le Comment. C'est ce qui permet à un autre développeur de modifier votre code et d'assurer sa maintenabilité. Cela peut être fait à l'aide des commentaires dans le code. Cela ne remplace pas le fait d'avoir un code lisible (nom de variables parlants, conditions claires), mais cela permet de savoir ce que le code est en train d'effectuer. Il faut trouver le compromis entre trop de commentaires, et un code sans commentaire qui est illisible.
